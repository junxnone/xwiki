---
Title | Programing Python Tools ruff
-- | --
Created @ | `2026-11-23T02:36:54Z`
Updated @| `2026-11-23T02:36:54Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/332)

---
# ruff

`ruff` 是 **Astral**（`uv` 的开发者）用 **Rust** 编写的 Python **代码检查（linter）+ 代码格式化（formatter）** 工具。一个二进制同时取代 `flake8`（及大量插件）、`isort`、`pyupgrade`、`autoflake`、`pydocstyle`、`black`，并覆盖部分 `pylint`、`bandit` 的规则。官方称速度比传统工具快 10-100 倍（厂商自报，实际取决于项目）。

> 本文基于 ruff 0.17.x（撰写时最新为 0.17.6，2026-11-19）。ruff 仍处于 0.x 阶段，**默认规则集在版本间会变化**，见文末「版本变化」。

## 能做什么

下表列出 ruff 的主要子命令，以及它们分别取代了哪些传统工具。

| 功能 | 命令 | 取代的工具 |
| -- | -- | -- |
| 代码检查 | `ruff check` | `flake8` + 插件、`pyupgrade`、`autoflake`、`pydocstyle`，部分 `pylint` / `bandit` |
| 自动修复 | `ruff check --fix` | `autoflake`、`pyupgrade` 等 |
| 导入排序 | `ruff check --select I --fix` | `isort` |
| 代码格式化 | `ruff format` | `black`（兼容度很高）、`yapf` |
| 查询规则 | `ruff rule` / `ruff linter` | 翻文档 |
| 编辑器支持 | `ruff server` | 旧的 `ruff-lsp` |

表中「命令」列是实际要敲的命令；「取代的工具」列表示原来需要分别安装和配置的工具，现在由 ruff 一个工具完成。注意 ruff 只做静态检查和格式化，**不做类型检查**（类型检查请用 mypy、pyright 等）。

## 安装

```bash
# 推荐：用 uv 安装成独立命令行工具
uv tool install ruff
uvx ruff check .            # 或者不安装，直接临时运行

# 作为项目开发依赖
uv add --dev ruff

# 其他方式
pip install ruff
pipx install ruff
brew install ruff

# 升级 / 查看版本
uv tool upgrade ruff
pip install -U ruff
ruff version
```

> `uv` 的用法见 [uv](0315_Programing_Python_Tools_uv)。从 0.17 起，conda-forge 版本不再依赖 Python，`python -m ruff` 和 `import ruff` 不再可用，直接用 `ruff` 命令；PyPI 和官方独立安装器不受影响。

## 快速上手

最常用的日常流程只有两步：先 `check --fix` 修复问题，再 `format` 统一格式。下面的流程图展示了从写代码到合并的完整过程。

```mermaid
flowchart LR
    A[编写代码] --> B["ruff check --fix ."]
    B --> C["ruff format ."]
    C --> D[提交代码]
    D --> E["CI: ruff check . 和 ruff format --check ."]
    E -- 通过 --> F[合并]
    E -- 失败 --> A
```

图中：

- **A → B**：先做 lint 并自动修复。修复可能会改动导入顺序、删除未使用的导入，所以必须放在格式化之前。
- **B → C**：再格式化，把前一步改动过的代码整理成统一风格。
- **D → E**：CI 里只检查、不修改文件：`ruff check .` 报告违规，`ruff format --check .` 在有文件需要格式化时返回非零退出码。
- **E → A**：检查失败就回到本地修复；通过才合并。

```bash
ruff check .            # 检查当前目录下所有 Python 文件
ruff check --fix .      # 检查并自动修复
ruff format .           # 格式化
ruff format --check .   # 只检查格式，不修改（CI 用）
```

## ruff check：代码检查

### 基本用法

```bash
ruff check                       # 检查当前目录（递归）
ruff check src/ tests/           # 指定目录
ruff check app.py                # 指定文件
cat app.py | ruff check -        # 从标准输入读取
cat app.py | ruff check --stdin-filename app.py -   # 标准输入，同时告诉 ruff 文件名（用于匹配配置）
```

输出示例：

```text
app.py:1:8: F401 [*] `os` imported but unused
app.py:5:5: F841 [*] Local variable `x` is assigned to but never used
Found 2 errors.
[*] 2 fixable with the `--fix` option.
```

每一行的格式是 `文件:行:列: 规则码 [*] 说明`，`[*]` 表示该问题可以自动修复。

### 常用选项

| 选项 | 作用 | 示例 |
| -- | -- | -- |
| `--fix` | 应用**安全**的自动修复 | `ruff check --fix` |
| `--unsafe-fixes` | 与 `--fix` 一起用，连**不安全**的修复也应用 | `ruff check --fix --unsafe-fixes` |
| `--diff` | 只显示修复会产生的差异，不写文件 | `ruff check --diff` |
| `--select` | 只启用指定规则（覆盖配置里的 `select`） | `ruff check --select E,F,I` |
| `--extend-select` | 在已有规则基础上追加规则 | `ruff check --extend-select B,UP` |
| `--ignore` | 忽略指定规则 | `ruff check --ignore E501` |
| `--statistics` | 按规则统计违规数量 | `ruff check --statistics` |
| `--show-fixes` | 列出已应用的修复 | `ruff check --fix --show-fixes` |
| `--watch` | 监听文件变化，保存即重新检查 | `ruff check --watch` |
| `--output-format` | 输出格式，如 `full`、`concise`、`json`、`github`、`gitlab`、`junit`、`sarif` | `ruff check --output-format=github` |
| `--add-noqa` | 给所有现存违规自动加上 `# noqa` 注释 | `ruff check --add-noqa` |
| `--config` | 指定配置文件，或临时覆盖单个配置项 | `ruff check --config ruff.toml` |
| `--isolated` | 忽略所有配置文件，用默认设置 | `ruff check --isolated` |
| `--preview` | 启用预览（实验性）规则和行为 | `ruff check --preview` |
| `--exit-zero` | 即使发现违规也返回退出码 0 | `ruff check --exit-zero` |
| `--exit-non-zero-on-fix` | 只要自动修复过任何东西就返回非零 | 用于 pre-commit |

表中「选项」列是命令行开关；「作用」列说明含义；「示例」列给出典型写法。其中最容易混淆的是三个与规则选择有关的开关：`--select` 会**替换**配置文件里的 `select`，`--extend-select` 是在其基础上**追加**，`--ignore` 用来从已选规则中**排除**。

### 修复的安全等级

ruff 把自动修复分为两类：

- **安全修复（safe）**：不会改变代码语义，`--fix` 默认只应用这一类，例如删除未使用的导入、排序导入。
- **不安全修复（unsafe）**：可能改变语义或删除注释，需要 `--unsafe-fixes` 才会应用，例如把 `if x == True` 改写成 `if x`。

从 0.17 起，默认的 `full` 输出会**显示**所有修复的差异（含不安全修复和需要人工处理的建议），但仍然只有加了 `--unsafe-fixes`（或在配置里启用 `unsafe-fixes`）才会**应用**不安全修复。建议先用 `--diff` 预览再应用。

### 退出码

| 退出码 | 含义 |
| -- | -- |
| 0 | 没有发现违规（或违规都已被 `--fix` 修复，且没加 `--exit-non-zero-on-fix`） |
| 1 | 发现了违规 |
| 2 | ruff 本身出错（配置错误、文件无法读取等） |

「退出码」列是进程返回值，CI 就是靠它判断是否通过；「含义」列说明各值对应的情况。`--exit-zero` 可以强制把 1 变成 0，用于「只提示、不拦截」。

### 常用场景

```bash
# 只整理导入顺序（替代 isort）
ruff check --select I --fix .

# 把旧语法升级到目标 Python 版本的写法（替代 pyupgrade）
ruff check --select UP --fix .

# 删除未使用的导入和变量（替代 autoflake）
ruff check --select F401,F841 --fix .

# 先看看项目里哪类问题最多，再决定先治理哪些规则
ruff check --select ALL --statistics .

# 存量项目接入：先把现有违规全部加上 noqa，之后只约束新增代码
ruff check --add-noqa .
```

## ruff format：代码格式化

`ruff format` 是 `black` 的直接替代品，风格与 black 高度兼容，速度快得多。

```bash
ruff format .                    # 格式化当前目录
ruff format app.py               # 格式化单个文件
ruff format --check .            # 不修改，有文件需要格式化则返回 1
ruff format --diff .             # 只显示将要产生的差异
ruff format --line-length 100 .  # 临时指定行宽
cat app.py | ruff format -       # 标准输入 → 标准输出
```

要点：

- **默认风格**：行宽 88、4 空格缩进、双引号、保留 magic trailing comma（末尾逗号会让集合/调用保持多行）。
- **docstring 里的代码**：设置 `docstring-code-format = true` 后，docstring 里的示例代码也会被格式化。
- **Markdown 里的代码块**：从 0.16 起，`ruff format` 默认也会格式化 Markdown 文件里的 Python 代码块。
- **与 lint 规则冲突**：格式化器会改变引号、尾随逗号、缩进等，所以不要同时启用与它冲突的 lint 规则（如 `COM812`、`ISC001`、`Q` 系列的引号规则、`W191`）。ruff 在你同时选了冲突规则时会给出警告。
- **导入排序不属于 format**：`ruff format` 不排序导入，需要用 `ruff check --select I --fix`。

## 配置

### 配置文件

ruff 会从被检查文件所在目录向上查找配置文件，**最近的一个生效**；同一目录下的优先级是 `ruff.toml` > `.ruff.toml` > `pyproject.toml`（`pyproject.toml` 里必须有 `[tool.ruff]` 段才会被当作 ruff 配置）。要继承别的配置，用 `extend = "../ruff.toml"`。

一份常用的 `pyproject.toml` 配置：

```toml
[tool.ruff]
line-length = 100                 # 行宽，默认 88
target-version = "py311"          # 目标 Python 版本；不写则读 project.requires-python
extend-exclude = ["migrations"]   # 在默认排除目录之外再排除

[tool.ruff.lint]
select = [
    "E", "W",   # pycodestyle：风格错误 / 警告
    "F",        # pyflakes：未使用导入、未定义名称等
    "I",        # isort：导入排序
    "B",        # flake8-bugbear：常见 bug 模式
    "UP",       # pyupgrade：旧语法升级
    "SIM",      # flake8-simplify：简化写法
]
ignore = ["E501"]                 # 行太长交给 formatter 处理

[tool.ruff.lint.per-file-ignores]
"__init__.py" = ["F401"]          # __init__ 里允许"只导入不使用"
"tests/**" = ["S101"]             # 测试里允许 assert

[tool.ruff.lint.isort]
known-first-party = ["mypkg"]

[tool.ruff.format]
quote-style = "double"            # 引号风格
indent-style = "space"            # 缩进用空格
docstring-code-format = true      # 格式化 docstring 里的代码
```

同样的内容写成 `ruff.toml` 时，去掉 `tool.ruff` 前缀即可（`[lint]`、`[format]`，顶层键直接写）。

### 常用配置项

| 配置项 | 位置 | 说明 |
| -- | -- | -- |
| `line-length` | `[tool.ruff]` | 行宽，默认 88，formatter 和部分规则共用 |
| `target-version` | `[tool.ruff]` | 目标 Python 版本，决定哪些语法升级可用 |
| `exclude` / `extend-exclude` | `[tool.ruff]` | 排除的文件；`extend-` 是在默认排除基础上追加 |
| `select` / `extend-select` | `[tool.ruff.lint]` | 启用的规则；`extend-` 是追加 |
| `ignore` | `[tool.ruff.lint]` | 排除的规则 |
| `fixable` / `unfixable` | `[tool.ruff.lint]` | 允许 / 禁止自动修复的规则 |
| `per-file-ignores` | `[tool.ruff.lint]` | 按文件通配符忽略规则 |
| `quote-style` | `[tool.ruff.format]` | `double`（默认）、`single`、`preserve` |
| `docstring-code-format` | `[tool.ruff.format]` | 是否格式化 docstring 里的代码，默认关闭 |

表中「位置」列是 `pyproject.toml` 里的段名；`ruff.toml` 中 `[tool.ruff]` 对应顶层、`[tool.ruff.lint]` 对应 `[lint]`、`[tool.ruff.format]` 对应 `[format]`。完整配置项可以用 `ruff config` 列出，或 `ruff config lint.select` 查看某一项。

### 规则选择器

规则码由「前缀 + 数字」组成，`select` 里可以写完整规则码（`F401`）、前缀（`F`、`E4`）或 `ALL`。

| 前缀 | 来源 | 内容 |
| -- | -- | -- |
| `E` / `W` | pycodestyle | 代码风格错误 / 警告（缩进、空白、行长等） |
| `F` | pyflakes | 未使用的导入、变量，未定义的名称 |
| `I` | isort | 导入排序 |
| `B` | flake8-bugbear | 容易出 bug 的写法 |
| `UP` | pyupgrade | 旧语法 → 新语法 |
| `SIM` | flake8-simplify | 可简化的写法 |
| `N` | pep8-naming | 命名规范 |
| `D` | pydocstyle | docstring 规范 |
| `S` | flake8-bandit | 安全问题（部分取代 `bandit`） |
| `PL` | pylint | 部分 pylint 规则 |
| `C4` | flake8-comprehensions | 推导式写法 |
| `RUF` | ruff 自有 | ruff 自己实现的规则 |

表中「前缀」是写在 `select` 里的缩写；「来源」是规则原本所属的工具或插件；「内容」是该类规则检查的对象。`select = ["ALL"]` 会启用全部规则，通常需要配合大量 `ignore`，适合新项目；存量项目建议从 `E`、`F`、`I` 起步，逐步放开。

## 抑制告警

| 方式 | 写法 | 作用范围 |
| -- | -- | -- |
| 行内 `noqa` | `import os  # noqa: F401` | 当前行；不写规则码则忽略该行所有规则（不推荐） |
| 行内 `ruff: ignore` | `import os  # ruff: ignore[F401]` | 当前行；也可写在违规行的上一行（0.16 起支持） |
| 文件级 | 文件里写 `# ruff: noqa: F401` | 整个文件的指定规则 |
| 配置里的 `per-file-ignores` | `"tests/**" = ["S101"]` | 匹配的一批文件 |
| 批量加注释 | `ruff check --add-noqa` | 给当前所有违规统一加上 `noqa` |

表中「方式」是抑制手段；「写法」是具体语法；「作用范围」说明影响多大。推荐用法是：个别例外用行内注释并写明规则码，成批的例外（如测试目录）用 `per-file-ignores`，存量项目接入时用 `--add-noqa`。启用 `RUF100` 后，ruff 会提示「已经不再需要的 noqa 注释」，可以用 `--fix` 自动清理。

## 查看规则与帮助

```bash
ruff rule F401          # 查看某条规则的说明、示例和修复情况
ruff rule --all         # 列出所有规则
ruff linter             # 列出所有规则来源（flake8 插件等）及前缀
ruff config             # 列出所有配置项
ruff config lint.select # 查看单个配置项的说明
ruff clean              # 清除缓存（默认在项目下的 .ruff_cache/）
ruff --help
```

## 集成

### pre-commit

```yaml
repos:
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.17.6              # 换成需要的版本
    hooks:
      - id: ruff-check
        args: [--fix]         # 先修复
      - id: ruff-format       # 再格式化
```

`ruff-check` 要写在 `ruff-format` 前面，原因与前面的流程图一致：先修复、后格式化。

### GitHub Actions

```yaml
jobs:
  ruff:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: astral-sh/ruff-action@v3       # 版本号以 Marketplace 最新为准
      - run: ruff format --check .
```

`astral-sh/ruff-action` 默认会执行 `ruff check`，所以这里只需要再补一条格式检查。

### 编辑器

- **VS Code**：安装官方扩展 **Ruff**（`charliermarsh.ruff`），可在保存时自动修复和格式化。从 0.17 起扩展只使用 ruff 自带的原生语言服务器，旧的 `ruff-lsp` 已移除。
- **其他编辑器**：支持 LSP 的编辑器可以直接运行 `ruff server`。

## 从其他工具迁移

| 原来的工具 | 在 ruff 里怎么做 | 注意 |
| -- | -- | -- |
| `flake8` + 插件 | `ruff check`，`select` 对应插件前缀 | 并非所有第三方插件都有对应实现 |
| `isort` | `select = ["I"]` + `--fix` | 配置迁到 `[tool.ruff.lint.isort]` |
| `black` | `ruff format` | 极少数边角情况与 black 输出不同 |
| `pyupgrade` | `select = ["UP"]` + `--fix` | 受 `target-version` 影响 |
| `autoflake` | `F401`、`F841` + `--fix` | 无 |
| `pydocstyle` | `select = ["D"]` | 用 `[tool.ruff.lint.pydocstyle] convention = "google"` 选风格 |
| `pylint` | `select = ["PL"]` | 只覆盖一部分规则，不能完全替代 |
| `bandit` | `select = ["S"]` | 只覆盖一部分规则，不能完全替代 |
| `yapf` | `ruff format` | 风格不同，会造成大规模格式变更 |

表中「原来的工具」是被取代的对象；「在 ruff 里怎么做」是对应做法；「注意」说明差异。已有 [pylint](0092_Programing_Python_Tools_pylint)、[bandit](0091_Programing_Python_Tools_bandit)、[yapf](0093_Programing_Python_Tools_yapf) 的文章可对照阅读：ruff 对 pylint、bandit 只是部分覆盖，需要完整检查时仍可保留原工具。

## 版本变化

ruff 的规则和默认行为在 0.x 版本里会调整，升级前建议读 [BREAKING_CHANGES](https://github.com/astral-sh/ruff/blob/main/BREAKING_CHANGES.md)。

| 版本 | 变化 |
| -- | -- |
| 0.16.0 | 默认启用的规则大幅扩充（官方说明 413 条，此前 59 条，即 `E4`、`E7`、`E9`、`F`），同时从默认集合里移除了 18 条较有争议的 `E` / `F` 规则；`ruff format` 默认格式化 Markdown 里的 Python 代码块；新增 `# ruff: ignore[...]` 注释 |
| 0.17.0 | 未配置 Python 版本时默认按 3.11；DTZ 系列部分规则（`DTZ001`、`DTZ005`、`DTZ006`、`DTZ007`、`DTZ011`、`DTZ012`、`DTZ901`）不再默认启用；`F406` 默认启用；默认 `full` 输出显示不安全修复的差异；格式化器和 `E501`、`I001` 计算行长时忽略行尾 pragma 注释；移除 `ruff-lsp` 支持 |

表中「版本」是发布号；「变化」是与日常使用相关的行为差异。因为默认规则会变，**项目里最好显式写出 `select`**，并在 CI 里固定 ruff 版本（例如 `uv.lock`、pre-commit 的 `rev`），避免升级后突然出现大量新告警。

## 常见问题

- **`ruff check --fix` 之后又需要 `ruff format`**：修复会改动代码结构，所以顺序是先 `check --fix`、再 `format`。
- **`E501`（行太长）要不要开**：formatter 已经负责折行，很多项目会把 `E501` 放进 `ignore`，只用 formatter 控制长度；formatter 无法折断的长字符串、URL 才会残留。
- **改了配置却没生效**：确认是不是更近目录下有另一个 `ruff.toml`，用 `ruff check --show-settings 某文件.py` 可以查看该文件实际使用的完整配置。
- **缓存**：ruff 默认缓存结果到 `.ruff_cache/`，一般不需要手动处理，需要时 `ruff clean`；记得把 `.ruff_cache/` 加进 `.gitignore`。

## Reference
- [Ruff 官方文档](https://docs.astral.sh/ruff/)
- [Ruff Linter](https://docs.astral.sh/ruff/linter/)
- [Ruff Formatter](https://docs.astral.sh/ruff/formatter/)
- [Configuring Ruff](https://docs.astral.sh/ruff/configuration/)
- [Ruff Rules](https://docs.astral.sh/ruff/rules/)
- [GitHub - astral-sh/ruff](https://github.com/astral-sh/ruff)
- [Breaking Changes](https://github.com/astral-sh/ruff/blob/main/BREAKING_CHANGES.md)
- [Changelog](https://github.com/astral-sh/ruff/blob/main/CHANGELOG.md)
- [astral-sh/ruff-pre-commit](https://github.com/astral-sh/ruff-pre-commit)
- [astral-sh/ruff-action](https://github.com/astral-sh/ruff-action)

