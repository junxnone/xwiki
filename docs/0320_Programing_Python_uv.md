---
Title | Programing Python uv
-- | --
Created @ | `2026-03-24T05:55:57Z`
Updated @| `2026-03-24T05:55:57Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/320)

---
# uv 
- 目前最快、最轻量、最现代的 Python 包管理和虚拟环境工具，由 Rust 编写，完全替代 pip + venv + pip-tools，速度比传统工具快 10~100 倍，是 Python 生态的下一代标准工具
- **优点**
  - 极速：安装、解析依赖、创建虚拟环境速度碾压 pip/conda
  - 极简：一条命令完成环境创建 + 包安装
  - 兼容：100% 兼容 PyPI、requirements.txt、pyproject.toml
  - 跨平台：Windows/macOS/Linux 全支持
  - 无依赖：单二进制文件，无需预装 Python 也能使用

## Install

### Windwos powershell

```
irm https://astral.sh/uv/install.ps1 | iex
```

### MacOS/Linux

```
curl -LsSf https://astral.sh/uv/install.sh | sh
```

## 使用

Cmd | Description
-- | --
`uv venv` | 创建虚拟环境（自动命名 .venv，推荐）
`uv venv --python 3.11` | 指定 Python 版本
`.venv\Scripts\Activate.ps1` |  Windows (PowerShell) 激活环境
`source .venv/bin/activate` |  macOS/Linux 激活环境
`uv install requests` | 安装单个包
`uv install requests==2.31.0` | 安装指定版本
`uv install --dev pytest black` | 安装开发依赖
`uv install -r requirements.txt` | 从 requirements.txt 安装
`uv uninstall requests` | 卸载包
`uv pip list` | 查看已安装包
`uv pip freeze > requirements.txt` | 导出依赖
`uv run main.py` | 直接运行 Python 脚本（无需手动激活环境）



