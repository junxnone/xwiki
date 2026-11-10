---
Title | Programing Python Tools pipx
-- | --
Created @ | `2026-11-10T03:31:51Z`
Updated @| `2026-11-10T03:31:51Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/330)

---
# pipx

`pipx` 用来**安装和运行带命令行入口的 Python 应用**（如 `black`、`ruff`、`httpie`、`poetry`），每个应用装在**独立的虚拟环境**里，只把命令暴露到 `PATH`。这样既不污染系统/项目的 Python 环境，也避免不同工具之间的依赖冲突。

可以把它理解为 Python 版的 `npx` / `npm -g` + 隔离：`pip` 负责装**库**，`pipx` 负责装**应用**。

## 解决什么问题

- `pip install black` 装到全局：和别的包依赖冲突，卸载不干净；新版 Linux 发行版（PEP 668）还会直接报 `externally-managed-environment`。
- 装进项目 venv：工具与项目依赖混在一起，每个项目都要重复装一遍。
- pipx：一个工具一个 venv，命令全局可用，互不影响，升级、卸载都按应用为单位。

## 安装

```bash
# Windows
python -m pip install --user pipx
python -m pipx ensurepath

# macOS
brew install pipx
pipx ensurepath

# Debian / Ubuntu
sudo apt install pipx
pipx ensurepath

# 其他：任意平台
python -m pip install --user pipx
python -m pipx ensurepath
```

`ensurepath` 会把 `~/.local/bin`（Windows 为 `%USERPROFILE%\.local\bin`）加入 `PATH`，执行后需要重开终端。

## 常用命令

```bash
pipx install black              # 安装应用（独立 venv）
pipx install "black==24.4.2"    # 指定版本
pipx install --python python3.11 poetry   # 指定 Python 版本
pipx install git+https://github.com/psf/black.git   # 从 git 安装

pipx list                       # 已安装的应用及其命令
pipx upgrade black              # 升级一个
pipx upgrade-all                # 升级全部
pipx reinstall-all              # 升级 Python 后重建所有 venv
pipx uninstall black            # 卸载
pipx uninstall-all

pipx run pycowsay hello         # 临时运行，不安装（缓存的临时 venv）
pipx run --spec "httpie" http httpbin.org/get   # 包名与命令名不同时用 --spec
```

### 注入额外依赖

给某个应用的 venv 里加包（例如插件）：

```bash
pipx install ansible
pipx inject ansible paramiko
pipx uninject ansible paramiko
```

### 运行脚本（PEP 723）

```bash
pipx run script.py   # 读取脚本头部的内联依赖声明
```

## 目录与工作原理

| 内容 | 默认位置 | 环境变量 |
| -- | -- | -- |
| 各应用的 venv | `~/.local/share/pipx/venvs/<app>` | `PIPX_HOME` |
| 命令入口（符号链接/脚本） | `~/.local/bin` | `PIPX_BIN_DIR` |
| `pipx run` 的临时 venv 缓存 | `~/.local/share/pipx/.cache` | `PIPX_HOME` |

（不同系统/版本默认路径可能不同，用 `pipx environment` 查看。）

`pipx install foo` 的过程：
1. 在 `venvs/foo` 创建 venv。
2. 在该 venv 里 `pip install foo`。
3. 读取包声明的 `console_scripts`，把对应命令链接到 `bin` 目录。

所以 `pipx` 本身是个薄封装：底层用的仍是 `venv` + `pip`。

## pipx 与 uv

| 需求 | pipx | uv |
| -- | -- | -- |
| 安装命令行工具 | `pipx install x` | `uv tool install x` |
| 临时运行 | `pipx run x` | `uvx x` |
| 升级 | `pipx upgrade x` | `uv tool upgrade x` |
| 速度 | 依赖 pip，较慢 | Rust 实现，快很多 |
| 管理 Python 版本 | 不管，需自备 | `uv python install` |
| 项目依赖管理 | 不涉及 | `uv add/sync/lock` |

如果已经在用 uv，可直接用 `uv tool` / `uvx` 取代 pipx，参见 [#315](https://github.com/junxnone/xwiki/issues/315)、[#320](https://github.com/junxnone/xwiki/issues/320)；pipx 的优势是更成熟、各发行版仓库里普遍可直接安装。

## 常用工具

包名与命令名不同的，在“命令”列单独标出。

### 开发与质量

| 包名 | 命令 | 用途 |
| -- | -- | -- |
| `ruff` | `ruff` | 极快的 linter + formatter（Rust 实现），可替代 flake8 / isort / black |
| `black` | `black` | 代码格式化 |
| `mypy` | `mypy` | 静态类型检查 |
| `pylint` / `flake8` / `bandit` | 同名 | 代码检查 / 风格检查 / 安全扫描 |
| `pre-commit` | `pre-commit` | 管理 git hooks |
| `tox` / `nox` | 同名 | 多 Python 版本测试自动化 |
| `cookiecutter` | `cookiecutter` | 从模板生成项目骨架 |
| `poetry` / `hatch` / `pdm` | 同名 | 项目与依赖管理、打包 |
| `twine` | `twine` | 上传包到 PyPI |
| `pipdeptree` | `pipdeptree` | 查看依赖树（配合 `--python` 查看某个环境） |
| `pip-audit` | `pip-audit` | 扫描依赖中的已知漏洞 |
| `pyinstrument` / `py-spy` / `scalene` | 同名 | 性能分析 |
| `mkdocs` | `mkdocs` | Markdown 文档站点生成 |

### 日常效率

| 包名 | 命令 | 用途 |
| -- | -- | -- |
| `httpie` | `http` / `https` | 友好的命令行 HTTP 客户端，输出带高亮 |
| `yt-dlp` | `yt-dlp` | 下载在线视频/音频 |
| `glances` | `glances` | 跨平台系统监控（CPU、内存、磁盘、网络、进程） |
| `bpytop` | `bpytop` | 好看的终端资源监视器 |
| `visidata` | `vd` | 终端里的表格数据探索，支持 CSV / JSON / Excel 等 |
| `csvkit` | `csvlook`、`csvstat` 等 | 一组处理 CSV 的命令行工具 |
| `pgcli` / `mycli` / `litecli` | 同名 | 带补全和高亮的 PostgreSQL / MySQL / SQLite 客户端 |
| `mitmproxy` | `mitmproxy` / `mitmweb` | 抓包、调试 HTTP/HTTPS 流量 |
| `ranger-fm` | `ranger` | 终端文件管理器 |
| `tldr` | `tldr` | 命令的简化示例手册，比 `man` 好读 |
| `howdoi` | `howdoi` | 在命令行里直接搜索编程问题的答案 |
| `speedtest-cli` | `speedtest-cli` | 命令行测网速 |
| `rich-cli` | `rich` | 在终端渲染 Markdown、JSON、代码高亮、表格 |
| `markitdown` | `markitdown` | 把 PDF、Word、PPT、Excel 等转成 Markdown |
| `huggingface_hub[cli]` | `huggingface-cli`（新版为 `hf`） | 下载/管理 Hugging Face 模型和数据集 |
| `jupyterlab` / `ipython` | `jupyter-lab` / `ipython` | 交互式环境，装成独立应用避免污染项目环境 |

### 有趣的工具

| 包名 | 命令 | 用途 |
| -- | -- | -- |
| `pycowsay` | `pycowsay` | 让奶牛说话，也是 pipx 官方文档里 `pipx run` 的示例 |
| `cowsay` | `cowsay` | 同类的字符画对话 |
| `terminaltexteffects` | `tte` | 终端文字动画特效（打字、雨滴、爆炸、燃烧……），可用管道输入任意文本 |
| `asciinema` | `asciinema` | 录制终端会话并回放/分享，不是视频而是文本，体积很小 |
| `magic-wormhole` | `wormhole` | 用一次性短口令在两台机器间安全传文件，如 `7-crossover-clockwork` |
| `lolcat` | `lolcat` | 把输出变成彩虹色 |
| `llm` | `llm` | 命令行调用大模型，可与 shell 管道组合 |

试玩示例（不用安装，`pipx run` 临时运行）：

```bash
pipx run pycowsay "hello pipx"
echo "hello pipx" | pipx run terminaltexteffects decrypt
pipx run --spec httpie http httpbin.org/get
pipx run --spec rich-cli rich --markdown README.md
```

> 以上包都是 PyPI 上的命令行应用，但部分较新的工具（`tte`、`markitdown`、`hf` 等）参数和命令名变化较快，用法以各自的 `--help` 或文档为准。

## 使用建议

- 适合 pipx 的：`black`、`ruff`、`pre-commit`、`httpie`、`poetry`、`tox`、`cookiecutter` 等**命令行应用**。
- 不适合 pipx 的：要在代码里 `import` 的库（`numpy`、`requests`），这些应该装在项目的虚拟环境里。
- Python 大版本升级后，用 `pipx reinstall-all` 重建各应用的 venv。

## Reference
- [pipx github](https://github.com/pypa/pipx)
- [pipx docs](https://pipx.pypa.io/stable/)
- [PEP 668 – Marking Python base environments as externally managed](https://peps.python.org/pep-0668/)
- [uv tools](https://docs.astral.sh/uv/concepts/tools/)

