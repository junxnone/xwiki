---
Title | Programing Python Tools uv
-- | --
Created @ | `2025-07-31T02:49:57Z`
Updated @| `2026-11-10T02:19:42Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/315)

---
# uv

`uv` 是 **Astral**（`ruff` 的开发者）用 **Rust** 编写的 Python 包与项目管理工具，一个工具覆盖 `pip`、`pip-tools`、`virtualenv`、`pyenv`、`pipx`、`poetry` 等的常见功能。核心特点：**快**（官方称比 `pip` 快 10-100 倍，全局缓存 + 硬链接复用）、**一体化**、**兼容现有生态**（`pyproject.toml`、`requirements.txt`）。

**优点**
- 极速：依赖解析、安装、创建虚拟环境都远快于 `pip`
- 极简：一条命令完成环境创建 + 包安装
- 兼容：兼容 PyPI、`requirements.txt`、`pyproject.toml`
- 跨平台：Windows / macOS / Linux
- 无依赖：单二进制文件，无需预装 Python 也能使用（可用 `uv python install` 自动获取）

## 能力一览

| 能力 | 替代的工具 | uv 命令 |
| -- | -- | -- |
| Python 版本管理 | `pyenv` | `uv python install/list/pin` |
| 项目依赖管理 | `poetry` / `pdm` | `uv init/add/remove/lock/sync/run` |
| 虚拟环境 | `venv` / `virtualenv` | `uv venv` |
| pip 兼容接口 | `pip` / `pip-tools` | `uv pip install/compile/sync` |
| 命令行工具安装 | `pipx` | `uv tool install` / `uvx` |
| 单文件脚本 | - | `uv run script.py`（PEP 723） |
| 构建与发布 | `build` / `twine` | `uv build` / `uv publish` |

> 注意：uv 没有 `uv install` / `uv uninstall` / `uv upgrade` 命令。pip 风格操作要加 `pip` 子命令（`uv pip install`），项目依赖用 `uv add`。

## 安装

```bash
# Linux / macOS
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows PowerShell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# 其他方式
pip install uv
brew install uv
winget install --id=astral-sh.uv -e

# 升级自身 / 查看版本
uv self update
uv --version
```

## Python 版本管理

```bash
uv python list              # 查看可用/已装版本
uv python install 3.12      # 下载安装 Python（无需系统预装）
uv python pin 3.12          # 写入 .python-version
```

## 项目工作流（推荐）

```bash
uv init myproj && cd myproj     # 生成 pyproject.toml、.python-version 等
uv add requests                 # 添加依赖，自动建 .venv 并更新 uv.lock
uv add --dev pytest             # 开发依赖
uv add "numpy>=1.26"            # 指定版本约束
uv remove requests              # 移除依赖
uv lock --upgrade-package numpy # 升级某个包
uv lock --upgrade               # 升级全部依赖（在约束范围内）
uv sync                         # 按 uv.lock 同步环境
uv sync --frozen                # 不更新 lock，严格按 lock 安装（CI 常用）
uv run python main.py           # 在项目环境中运行，无需手动激活
uv run pytest
uv tree                         # 查看依赖树
```

- `uv.lock` 是跨平台的通用锁文件，记录精确版本与哈希，应提交到版本库。
- `uv run` / `uv sync` 会自动创建并同步 `.venv`，通常不需要手动 `activate`。

## 虚拟环境

```bash
uv venv                         # 在当前目录创建 .venv
uv venv --python 3.11 myenv     # 指定 Python 版本和目录
source .venv/bin/activate       # Linux/macOS 激活
.venv\Scripts\activate          # Windows 激活
```

## pip 兼容接口

用于不想迁移到项目模式的存量项目：

```bash
uv pip install requests
uv pip install requests==2.31.0                      # 指定版本
uv pip install -r requirements.txt
uv pip install -e .                                  # 可编辑安装
uv pip uninstall pandas
uv pip list / uv pip show numpy / uv pip freeze
uv pip compile requirements.in -o requirements.txt   # 类似 pip-compile
uv pip sync requirements.txt                         # 精确同步
```

## 工具与脚本

```bash
uvx ruff check .                # 临时运行工具（等价 uv tool run），不污染环境
uv tool install ruff            # 全局安装命令行工具（隔离环境，类似 pipx）
uv tool list
uv tool upgrade --all

# 单文件脚本，依赖写在脚本头部（PEP 723）
uv add --script demo.py requests
uv run demo.py
```

## 构建与发布

```bash
uv build                        # 生成 sdist 和 wheel 到 dist/
uv publish                      # 上传到 PyPI
```

## 常用配置

- **镜像源**：国内/内网环境可在 `pyproject.toml` 或 `uv.toml` 配置：

  ```toml
  [[tool.uv.index]]
  url = "https://pypi.tuna.tsinghua.edu.cn/simple"
  default = true
  ```

  或使用环境变量 `UV_DEFAULT_INDEX`；Python 下载镜像可用 `UV_PYTHON_INSTALL_MIRROR`。
- **代理**：遵循 `HTTP_PROXY` / `HTTPS_PROXY` 环境变量。
- **缓存**：`uv cache dir` 查看位置，`uv cache clean` 清理；`UV_CACHE_DIR` 可改路径。
- **PyTorch 等特殊索引**：用 `[tool.uv.sources]` 为指定包绑定索引。
- **CI**：可使用 `astral-sh/setup-uv` Action，配合 `uv sync --frozen`。

## 迁移对照

| 原来 | 现在 |
| -- | -- |
| `python -m venv .venv` | `uv venv` |
| `pip install x` | `uv add x`（项目）/ `uv pip install x` |
| `pip freeze > requirements.txt` | `uv lock` 或 `uv pip freeze` |
| `pip install -r requirements.txt` | `uv sync` / `uv pip install -r requirements.txt` |
| `pipx run x` / `pipx install x` | `uvx x` / `uv tool install x` |
| `pyenv install 3.12` | `uv python install 3.12` |

## Reference
- [uv github](https://github.com/astral-sh/uv)
- [uv docs](https://docs.astral.sh/uv/)
- [uv pip 接口文档](https://docs.astral.sh/uv/pip/)
- [PEP 723 – Inline script metadata](https://peps.python.org/pep-0723/)

