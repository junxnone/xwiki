-----

| Title     | Programing Python Tools uv                           |
| --------- | ---------------------------------------------------- |
| Created @ | `2025-07-31T02:49:57Z`                               |
| Updated @ | `2025-07-31T02:49:57Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/315) |

-----

# uv

`uv` 是一款由 **Astral Software** 开发的现代化 Python 工具，集 **包管理**、**虚拟环境管理** 和
**构建功能** 于一体，旨在解决传统工具（如
`pip`、`virtualenv`、`setuptools`）的速度慢、流程繁琐等问题。其核心优势是
**极致性能** 和 **一体化工作流**，目前已成为 Python 生态中备受关注的工具。

### **核心功能与优势**

1.  **超快速的包管理**
    
      - 底层基于 Rust 语言开发，依赖解析和安装速度远超 `pip`（官方测试显示比 `pip` 快 10-100 倍）。
      - 支持常见的包操作：安装（`uv install`）、卸载（`uv uninstall`）、升级（`uv
        upgrade`）、查看依赖（`uv show`）等，命令风格与 `pip` 兼容，学习成本低。
    
    示例：
    
    ``` bash
    # 安装第三方包
    uv install requests
    # 卸载包
    uv uninstall pandas
    # 升级包到最新版本
    uv upgrade numpy
    ```

2.  **一体化虚拟环境管理**
    
      - 内置虚拟环境功能，无需单独安装 `venv` 或 `virtualenv`。
      - 支持创建、激活、删除虚拟环境，且切换速度极快。
    
    示例：
    
    ``` bash
    # 创建虚拟环境
    uv venv myenv
    # 激活环境（Linux/macOS）
    source myenv/bin/activate
    # 激活环境（Windows PowerShell）
    .\myenv\Scripts\Activate.ps1
    ```

3.  **精确的依赖锁定**
    
      - 生成 `uv.lock` 文件（类似
        `package-lock.json`），精确记录所有依赖的版本和来源，确保不同环境安装的依赖完全一致，解决“在我这能跑”的问题。
      - 支持通过 `uv lock` 生成锁文件，通过 `uv sync` 从锁文件同步依赖。
    
    示例：
    
    ``` bash
    # 生成依赖锁文件（基于 pyproject.toml 或 requirements.txt）
    uv lock
    # 根据锁文件安装所有依赖（确保环境一致）
    uv sync
    ```

4.  **项目构建支持**
    
      - 兼容 Python 打包标准（如 `pyproject.toml`），可替代 `setuptools` 或 `flit` 构建
        wheel 包或源码包。
      - 支持本地包安装（如 `uv install .` 安装当前目录项目，`uv install -e .` 以可编辑模式安装）。

### **与传统工具的对比**

| 功能场景   | 传统工具组合                            | `uv` 对应操作              | 优势             |
| ------ | --------------------------------- | ---------------------- | -------------- |
| 安装包    | `pip install <package>`           | `uv install <package>` | 速度提升 10-100 倍  |
| 创建虚拟环境 | `python -m venv myenv`            | `uv venv myenv`        | 无需额外依赖，创建速度更快  |
| 生成依赖清单 | `pip freeze > requirements.txt`   | `uv lock`（生成 uv.lock）  | 依赖解析更精确，避免版本冲突 |
| 同步环境依赖 | `pip install -r requirements.txt` | `uv sync`              | 按锁文件精确安装，速度更快  |

### **安装方式**

  - **Linux/macOS**：通过 curl 一键安装
    ``` bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```
  - **Windows**：通过 PowerShell 安装
    ``` powershell
    Invoke-WebRequest -Uri https://astral.sh/uv/install.ps1 -UseBasicParsing | Invoke-Expression
    ```
  - **其他方式**：支持通过 Homebrew（`brew install uv`）、AUR 等包管理器安装，或从 [GitHub
    Releases](https://github.com/astral-sh/uv/releases) 下载二进制文件。

### **适用场景**

  - 日常开发中替代 `pip` 管理包，提升安装效率；
  - 管理项目依赖，通过 `uv lock` 和 `uv sync` 确保团队环境一致性；
  - 快速创建和切换虚拟环境，简化开发流程；
  - 构建和发布 Python 包（替代 `setuptools` 等工具）。

如果需要具体场景的使用技巧（如配置镜像源、批量操作依赖、与 CI/CD 集成等），可以进一步说明需求\~

## Reference

  - [uv github](https://github.com/astral-sh/uv)
  - [uv docs](https://docs.astral.sh/uv/)
