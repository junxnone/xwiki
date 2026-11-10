---
Title | Programing Python Tools uv Internals
-- | --
Created @ | `2026-03-24T05:55:57Z`
Updated @| `2026-11-10T02:33:08Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/320)

---
# uv Internals

`uv` 是一个静态链接的 Rust 单二进制，不依赖 Python 解释器本身运行。它快不是靠某一个技巧，而是几件事叠加：**元数据尽量不下载整个包**、**依赖解析用 PubGrub 且并发预取**、**全局缓存 + 链接安装代替复制**、**一个进程内完成全流程**。本文按一次 `uv add` / `uv run` 的执行顺序，梳理这些机制。使用方法见 [#315](https://github.com/junxnone/xwiki/issues/315)。

> 说明：uv 迭代很快，缓存目录名、默认值等细节会随版本变化，以下以机制为主，具体行为以 [官方文档](https://docs.astral.sh/uv/) 为准。

## 整体流程

```
uv run / uv add / uv sync
 │
 ├─ 1. 发现 Python 解释器      （找已有的，或下载 python-build-standalone）
 ├─ 2. 读取项目               （pyproject.toml / uv.lock / requirements）
 ├─ 3. 依赖解析 (Resolver)     （PubGrub，输出 uv.lock）
 │      └─ 取元数据            （Simple API → wheel METADATA → 必要时构建 sdist）
 ├─ 4. 规划安装 (Planner)      （对比 site-packages，得出：保留 / 卸载 / 安装）
 ├─ 5. 准备包 (Preparer)       （并发下载、校验哈希、解压到全局缓存）
 ├─ 6. 安装 (Installer)        （从缓存 link 到 .venv/site-packages）
 └─ 7. exec 目标命令           （仅 uv run：设置 VIRTUAL_ENV / PATH 后启动）
```

## 1. Python 解释器发现与管理

- 查找顺序大致为：`UV_PYTHON` / `--python` 指定 → uv 自己管理的版本 → `PATH` 中的 `python` → Windows 下的 `py` 启动器。项目里的 `.python-version`、`requires-python` 会参与筛选。
- 发现候选解释器后，uv 会**运行一小段探测脚本**取回版本、平台标签、`sys.path`、`sysconfig` 等信息，并**缓存**结果，避免重复启动解释器。
- `uv python install` 下载的是 [python-build-standalone](https://github.com/astral-sh/python-build-standalone) 预编译发行版，解压到 uv 的数据目录，所以无需系统预装 Python。

## 2. 虚拟环境：为什么 `uv venv` 很快

- venv 本质是：一个目录 + `pyvenv.cfg` + 指向基础解释器的 `python` 链接/拷贝 + 空的 `site-packages` + 激活脚本。
- 标准 `python -m venv` 慢，主要是因为默认还会运行 `ensurepip` 装 pip。uv **不装 pip/setuptools**（除非 `--seed`），直接用 Rust 写出这些文件，几乎是纯文件系统操作。
- 激活脚本只是改 `VIRTUAL_ENV` 和 `PATH`。`uv run` 不需要激活：它在启动子进程前自己设置这两个环境变量。

## 3. 依赖解析

### 3.1 算法：PubGrub

- uv 使用 [PubGrub](https://nex3.medium.com/pubgrub-2fb6470504f)（Dart `pub` 采用的版本求解算法）。冲突时它能由不兼容性推导出**可读的冲突原因**，并做冲突驱动的回溯，比 pip 的朴素回溯在复杂依赖图上稳定得多。
- uv 的解析结果**默认取每个依赖满足约束的最高版本**；可用 `--resolution lowest` 等策略验证下限。
- `uv.lock` 使用**通用解析（universal resolution）**：解析时按 PEP 508 环境标记（平台、Python 版本）**分叉**，得到一份可覆盖多个平台和 Python 版本的锁，而不是只对当前机器有效。

### 3.2 元数据获取：尽量不下载整个包

解析只需要每个候选版本的**依赖元数据**，不需要安装它。uv 按代价从低到高尝试：

1. **Simple API**：请求 `/simple/<pkg>/` 获取文件列表（支持 PEP 691 JSON），按 HTTP 缓存语义（ETag 等）缓存。
2. **PEP 658**：PyPI 把 wheel 的 `METADATA` 单独暴露为 `<wheel>.metadata`，只下几 KB。
3. **HTTP Range 请求**：服务器不支持 PEP 658 时，只读 wheel（zip）末尾的中央目录，抽出 `METADATA`。
4. **下载整个 wheel** 作为兜底。
5. **sdist（源码包）**：没有预构建元数据时，需要在隔离环境里调用构建后端 hook（PEP 517 的 `prepare_metadata_for_build_wheel`）才能知道依赖。这是最慢的路径，结果会被缓存。
   - 构建隔离：创建临时 venv，安装 `build-system.requires`，再通过子进程调用后端。

### 3.3 并发

- 基于 `tokio` 异步运行时；解析器在做决策的同时，**预取**可能需要的包的元数据，网络等待与计算重叠。
- 版本选择、文件列表解析等 CPU 工作在 Rust 中完成，没有 Python 解释器启动和 GIL 的开销。

## 4. 常见文件与目录

### 4.1 项目内文件

`uv init myproj` 生成的典型结构：

```
myproj/
├── pyproject.toml     # 项目元数据 + 依赖声明 + uv 配置（人工维护）
├── uv.lock            # 锁文件（uv 生成，勿手改，需提交）
├── .python-version    # 默认 Python 版本（uv python pin 写入，建议提交）
├── .venv/             # 虚拟环境（uv 管理，不提交）
├── .gitignore         # uv init 生成，已忽略 .venv 等
├── README.md
└── main.py            # 示例入口（app 模板；--lib 模板则是 src/ 布局）
```

| 文件/目录 | 谁维护 | 是否提交 | 说明 |
| -- | -- | -- | -- |
| `pyproject.toml` | 人 + `uv add/remove` | 是 | 标准 PEP 621 元数据。`[project].dependencies` 是运行依赖；`[dependency-groups]`（PEP 735）放 dev 等分组，`uv add --dev` 写入 `dev` 组；`[tool.uv]` 放 uv 专属配置 |
| `uv.lock` | uv | 是 | 精确版本 + 哈希，见 4.2 |
| `.python-version` | 人 + `uv python pin` | 是 | 一行版本号，如 `3.12`；uv 与 pyenv 等工具都会读取 |
| `.venv/` | uv | 否 | 项目环境，可随时删掉用 `uv sync` 重建；位置可用 `UV_PROJECT_ENVIRONMENT` 修改 |
| `uv.toml` | 人 | 视情况 | 与 `pyproject.toml` 里的 `[tool.uv]` 等价的独立配置文件；两者同时存在时 `uv.toml` 优先 |
| `requirements.txt` / `requirements.in` | 人 / `uv pip compile` | 视情况 | pip 兼容工作流使用；`uv export -o requirements.txt` 可由 `uv.lock` 导出 |
| `dist/` | `uv build` | 否 | 构建产物（sdist、wheel） |

`pyproject.toml` 示例：

```toml
[project]
name = "myproj"
version = "0.1.0"
requires-python = ">=3.10"
dependencies = [
    "requests>=2.31",
]

[dependency-groups]
dev = ["pytest>=8"]

[tool.uv]
# 例：自定义索引、覆盖依赖、冲突声明等
index-url = "https://pypi.org/simple"

[tool.uv.sources]
# 例：为某个包指定来源（git / path / 指定 index / workspace 成员）
# mypkg = { git = "https://github.com/xxx/mypkg" }
```

> 配置的优先级大致为：命令行参数 > 环境变量（`UV_*`）> 项目级（`uv.toml` / `pyproject.toml`）> 用户级 > 系统级。

**Workspace**：`[tool.uv.workspace]` 的 `members` 声明多个子项目，整个 workspace 共享**同一个** `uv.lock` 和 `.venv`，成员之间用 `{ workspace = true }` 互相引用。

### 4.2 锁文件 `uv.lock`

典型片段（节选，字段随版本可能有变化）：

```toml
version = 1
requires-python = ">=3.10"

[[package]]
name = "requests"
version = "2.32.3"
source = { registry = "https://pypi.org/simple" }
dependencies = [
    { name = "certifi" },
    { name = "urllib3" },
]
sdist = { url = "...", hash = "sha256:...", size = 131218 }
wheels = [
    { url = "...", hash = "sha256:...", size = 64928 },
]

[[package]]
name = "myproj"
version = "0.1.0"
source = { virtual = "." }
dependencies = [
    { name = "requests" },
]
```

- 每个 `[[package]]` 是一个包的一个版本，`source` 标明来源（`registry` / `git` / `path` / `virtual`、`editable` 等）。
- 同一个包因平台或 Python 版本不同选了不同版本时，会出现多条记录，并以 `resolution-markers` / `marker` 区分（通用解析的结果）。
- 文件很大是正常的：它把每个包所有可用文件的哈希都记下来，使同一份锁能在不同平台上使用。

锁文件的作用与行为：

- TOML 格式，记录每个包的**精确版本、来源（registry / git / path）、文件哈希（sha256）、依赖及其环境标记**。
- `uv run` / `uv sync` 会检查 `pyproject.toml` 与锁是否一致，不一致则先重新解析（`--frozen` 跳过检查，`--locked` 不一致则报错，适合 CI）。
- 锁里带哈希，安装时会校验下载的文件，防止被篡改或索引上的文件被替换。

### 4.3 用户级目录与配置

uv 把全局数据放在用户目录下（路径随系统不同，用命令查最准）：

| 内容 | 查看方式 | 典型位置 |
| -- | -- | -- |
| 缓存 | `uv cache dir` | Linux/macOS `~/.cache/uv`；Windows `%LOCALAPPDATA%\uv\cache` |
| uv 管理的 Python | `uv python dir` | Linux/macOS `~/.local/share/uv/python`；Windows `%APPDATA%\uv\python` |
| 全局工具环境（`uv tool install`） | `uv tool dir` | `~/.local/share/uv/tools` |
| 工具命令入口（可执行文件） | `uv tool dir --bin` | `~/.local/bin` |
| 用户级配置 | - | Linux/macOS `~/.config/uv/uv.toml`；Windows `%APPDATA%\uv\uv.toml` |
| 系统级配置 | - | `/etc/uv/uv.toml` |

对应环境变量：`UV_CACHE_DIR`、`UV_PYTHON_INSTALL_DIR`、`UV_TOOL_DIR`、`UV_TOOL_BIN_DIR`、`UV_CONFIG_FILE`。

## 5. 安装：全局缓存 + 链接

### 5.1 缓存分层

缓存根目录用 `uv cache dir` 查看，主要包含几类内容：

| 内容 | 作用 |
| -- | -- |
| Simple API / 元数据缓存 | 避免重复请求索引，加速解析 |
| 下载的 wheel | 避免重复下载 |
| **解压后的 wheel 目录** | 安装时直接从这里链接，免去每次解压 |
| 从 sdist/git 构建出的 wheel | 避免重复构建 |
| 解释器探测结果 | 避免重复启动 Python |

### 5.2 Planner：只做必要的改动

- 扫描目标环境的 `site-packages`（读取各 `*.dist-info` 的 `RECORD`、`direct_url.json`、`INSTALLER` 等），与解析结果对比。
- 已满足的包保留，版本/来源不符的先卸载再装，缺少的才安装。所以**第二次 `uv sync` 几乎是空操作**。

### 5.3 Installer：链接而不是复制

- 把缓存中解压好的 wheel 内容，按 wheel 规范放到 `site-packages`（`purelib`/`platlib`、`scripts`、`data` 等），并生成 `RECORD`、可执行入口脚本。
- 文件放置方式（`--link-mode` / `UV_LINK_MODE`）：
  - `clone`：写时复制（reflink），在支持的文件系统（macOS APFS、部分 Linux 文件系统）上是默认值。
  - `hardlink`：硬链接，在 Linux 上通常是默认值。多个虚拟环境共享同一份磁盘数据，**既省空间又省时间**。
  - `copy` / `symlink`：兜底或按需选择。
  - 缓存和 venv 位于不同文件系统时，硬链接不可用，会回退为复制并给出警告；可以把 `UV_CACHE_DIR` 放到同一磁盘，或显式设置 `--link-mode`。
- 硬链接的副作用：改动某个 venv 里的包文件会影响缓存和其他共享它的环境，所以不要手动修改 site-packages 里的文件。
- `.pyc` 默认不预编译（`--compile-bytecode` 可开启），以进一步缩短安装时间，首次导入时再生成。

## 6. `uv run` 做了什么

1. 向上查找 `pyproject.toml` / workspace，确定项目与 `.venv`。
2. 确保解释器满足 `requires-python`，必要时创建/重建 `.venv`。
3. 检查/更新 `uv.lock`，再同步环境（上面第 3~5 步）。
4. 设置 `VIRTUAL_ENV`、把 `.venv/bin`（Windows 为 `Scripts`）放到 `PATH` 最前，然后 **exec** 目标命令（Unix 上是替换当前进程）。
5. 带 PEP 723 内联元数据的脚本：为该脚本的依赖建立**独立的临时/缓存环境**，不污染项目环境。

`uvx` / `uv tool run` 与之类似：按「工具名 + 版本约束」生成一个被缓存的隔离环境并运行，之后同样的命令直接复用。

## 7. 性能来源小结

| 来源 | 机制 |
| -- | -- |
| 少下载 | PEP 658 / Range 请求只取元数据；wheel 与构建结果全局缓存 |
| 少计算 | PubGrub；Planner 只处理差异；解释器探测结果缓存 |
| 少 IO | 解压一次，硬链接/reflink 到各环境，不重复拷贝 |
| 少等待 | tokio 并发下载 + 元数据预取；多线程解压 |
| 少启动开销 | 单个 Rust 二进制，不启动 Python、不装 pip |

## 8. 与 pip 的主要差异

- **没有 pip 的 wheel 缓存格式**：uv 缓存的是解压后的目录并直接链接，pip 每次安装都要从 wheel 解压。
- **解析与安装解耦、并发**：pip 是「解析一个、下载一个」偏串行；uv 把元数据获取并发化。
- **通用锁文件**：pip 没有原生锁文件；`pip freeze` 只记录当前环境。
- **索引策略更保守**：默认 `first-index`（只在首个有该包的索引里找），用于降低依赖混淆攻击的风险；可通过 `--index-strategy` 调整。这与 pip 的 `--extra-index-url` 合并所有索引的行为不同。

## Reference
- [uv docs: Concepts](https://docs.astral.sh/uv/concepts/)
- [uv docs: Resolution](https://docs.astral.sh/uv/concepts/resolution/)
- [uv docs: Caching](https://docs.astral.sh/uv/concepts/cache/)
- [uv github](https://github.com/astral-sh/uv)
- [PubGrub: Next-generation version solving](https://nex3.medium.com/pubgrub-2fb6470504f)
- [PEP 658 – Serve distribution metadata in the Simple API](https://peps.python.org/pep-0658/)
- [PEP 517 – A build-system independent format for source trees](https://peps.python.org/pep-0517/)
- [PEP 723 – Inline script metadata](https://peps.python.org/pep-0723/)
- [python-build-standalone](https://github.com/astral-sh/python-build-standalone)

