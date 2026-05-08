-----

| Title     | Programing Python usersite                           |
| --------- | ---------------------------------------------------- |
| Created @ | `2026-05-08T05:49:32Z`                               |
| Updated @ | `2026-05-08T05:49:32Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/324) |

-----

# Python user site 详解

## 一、什么是 Python user site？

user site 全称 user-specific site-packages directory，是 Python
为普通用户（非管理员）预留的第三方包安装目录，无需 root/sudo 权限即可安装包。

### 核心路径

  - Linux / Mac：`~/.local/lib/pythonX.Y/site-packages`（X.Y 为 Python 版本，如
    3.10、3.11）
  - Windows：`C:\Users\用户名\AppData\Roaming\Python\PythonXY\site-packages`

### 查看自身 user site 路径

    python -m site --user-site

## 二、user site 的默认行为

Python 默认 开启 user site 加载，即：

1.  启动 Python 时，会自动搜索并加载 user site 目录下的包
2.  使用 `pip install 包名` 时，若没有管理员权限，默认将包安装到 user site
3.  验证是否开启：执行 `python -m site`，若显示 `ENABLE_USER_SITE = True`，即为开启状态

## 三、为什么设计 user site？（历史背景）

Python 最初设计 user site 的核心目的：解决普通用户无管理员权限安装第三方包的问题。
在虚拟环境（venv/conda）出现之前，Python
只有“系统级”和“用户级”两个安装维度：

  - 系统级 site-packages：管理员通过 sudo 安装，所有用户共用
  - 用户级 site-packages：普通用户自行安装，仅当前用户可用
    这种设计在当时解决了“权限不足无法装包”的痛点，但给现代开发留下了隐患。

## 四、默认开启 user site 的坑（现代开发痛点）

如今开发者普遍使用虚拟环境（venv/conda/uv/poetry），而 Python 虚拟环境默认不会屏蔽 user
site，导致以下问题：

1.  依赖污染：虚拟环境中明明未安装某包，却能 import（因为加载了 user site 的包）
2.  版本冲突：user site 中的包版本与虚拟环境所需版本不一致，导致代码运行报错
3.  环境不可复现：本地运行正常，部署时因缺少 user site 中的包而失败（部署环境通常无用户级包）
4.  调试困难：无法判断包来自虚拟环境还是 user site，排查依赖问题耗时

## 五、PYTHONNOUSERSITE=1 作用与用法

### 核心作用

设置环境变量 `PYTHONNOUSERSITE=1`，可强制 Python 忽略 user site
目录，仅加载系统级或虚拟环境中的包，彻底解决依赖污染问题。

### 三种使用方式（按常用程度排序）

1.  临时生效（当前终端会话）

<!-- end list -->

    # Linux / Mac
    export PYTHONNOUSERSITE=1
    
    # Windows cmd
    set PYTHONNOUSERSITE=1
    
    # Windows PowerShell
    $env:PYTHONNOUSERSITE=1

说明：仅对当前终端有效，关闭终端后失效，适合临时测试干净环境。

2.  单次运行 Python 时生效

<!-- end list -->

    # 运行脚本时，临时屏蔽 user site
    PYTHONNOUSERSITE=1 python your_script.py
    
    # 进入 Python 交互环境时生效
    PYTHONNOUSERSITE=1 python

3.  永久生效（一劳永逸）

<!-- end list -->

``` 
# Linux / Mac（zsh 终端，最常用）
echo 'export PYTHONNOUSERSITE=1' >> ~/.zshrc
source ~/.zshrc

# Linux / Mac（bash 终端）
echo 'export PYTHONNOUSERSITE=1' >> ~/.bashrc
source ~/.bashrc
`
# Windows PowerShell（用户级永久生效）
[Environment]::SetEnvironmentVariable("PYTHONNOUSERSITE", "1", "User")

```

说明：设置后，所有新终端启动的 Python 都会自动屏蔽 user site，适合长期开发。 验证是否生效

    python -m site

若输出 `ENABLE_USER_SITE = False`，则表示成功屏蔽 user site。

## 六、关键疑问解答

1.  为什么 Python 不默认关闭 user site？ 核心原因：向后兼容。 Python
    不敢轻易修改默认行为——大量老脚本、老系统依赖
    user site 才能正常运行，一旦默认关闭，会导致这些程序直接崩溃。因此选择“保持历史默认，让开发者自行控制”。
2.  哪些场景必须关闭 user site？

<!-- end list -->

  - 使用虚拟环境开发（venv/conda/uv/poetry）
  - 开发可复现的项目（需干净依赖）
  - 使用 Claude Code、VS Code 等 IDE 运行 Python 代码（避免本地包干扰）
  - 部署项目（确保环境一致，无多余依赖）

<!-- end list -->

3.  关闭 user site 后，如何安装用户级包？ 若确实需要安装用户级包，可临时取消屏蔽，安装完成后再开启：

<!-- end list -->

    # Linux / Mac 临时取消屏蔽
    unset PYTHONNOUSERSITE
    # 安装用户级包
    pip install --user 包名
    # 重新开启屏蔽
    export PYTHONNOUSERSITE=1

七、总结

  - user site 是 Python 历史遗留设计，初衷是解决普通用户无权限装包的问题；
  - 现代开发中，默认开启 user site 会导致依赖污染、版本冲突，需手动关闭；
  - `PYTHONNOUSERSITE=1` 是最简洁的解决方案，推荐永久设置；
  - 仅在需要安装用户级包时，临时取消屏蔽即可。
