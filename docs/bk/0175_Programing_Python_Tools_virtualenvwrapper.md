-----

| Title     | Programing Python Tools virtualenvwrapper            |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-02-19T10:21:28Z`                               |
| Updated @ | `2024-06-26T06:05:35Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/175) |

-----

# virtualenvwrapper

  - virtualenv 的扩展
      - 组织所有的虚拟环境，放在一起管理
      - 包装了一些命令 `create/delete/copy/...`
      - 自动补全虚拟环境
      - ...

## Install

### Linux

    pip install virtualenvwrapper

### Auto Setup

  - Add setup script to bashrc

<!-- end list -->

    vi ~/.bashrc

    source ~/.local/bin/virtualenvwrapper.sh

### Windows Install

    pip install virtualenvwrapper-win

  - **Powershell Issue**: command line 可以运行，但是 powershell 不可以，需要设置脚本执行权限

管理员身份运行 powershell，执行以下操作, 选择 `Y`

    Set-ExecutionPolicy RemoteSigned

此时可以在 powershell 下 进入 虚拟环境目录执行 `activate.ps1`

## UseCase

### 创建虚拟环境

    mkvirtualenv venv_name

#### 创建特定 python 的虚拟环境

    mkvirtualenv env  --python=python3.8

### 打开/切换虚拟环境

    workon venv_name

### 退出虚拟环境

    deactivate

### 删除虚拟环境

    rmvirtualenv venv_name

### 列出所有虚拟环境

    lsvirtualenv

## Reference

  - [Docs](https://virtualenvwrapper.readthedocs.io/en/latest/index.html)
  - [windows下安装Virtualenvwrapper](https://blog.csdn.net/a549416598/article/details/80881235)
  - [virtualenvwrapper-powershell](https://github.com/regisf/virtualenvwrapper-powershell)
  - [virtualenvwrapper-win](https://pypi.org/project/virtualenvwrapper-win/)
