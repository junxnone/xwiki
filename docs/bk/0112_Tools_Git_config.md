-----

| Title     | Tools Git config                                     |
| --------- | ---------------------------------------------------- |
| Created @ | `2018-12-14T07:45:42Z`                               |
| Updated @ | `2026-11-10T06:06:36Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/112) |

-----

# Git Configs

## 配置的三个级别

| 参数         | 作用范围     | 文件位置                                                 | 优先级 |
| ---------- | -------- | ---------------------------------------------------- | --- |
| `--system` | 整台机器所有用户 | Git 安装目录下的 `etc/gitconfig`                           | 低   |
| `--global` | 当前用户     | `~/.gitconfig`（Windows 为 `%USERPROFILE%\.gitconfig`） | 中   |
| `--local`  | 当前仓库（默认） | 仓库内 `.git/config`                                    | 高   |

  - 后者覆盖前者。`git config` 不带级别参数时写入 `--local`，所以要在仓库目录里执行。

## 常用配置

| Configs                      | Commands                                                                                                         |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| 设置**默认编辑器**                  | `git config --global core.editor vi`                                                                             |
| 设置**用户名邮箱**                  | `git config --global user.name "your_name"`<br>`git config --global user.email "your_email"`                     |
| 为单独仓库设置**用户名邮箱**             | 在仓库目录下执行（无需 `--global`）：<br>`git config user.name "your_name"`<br>`git config user.email "your_email"`           |
| 忽略文件权限更改                     | `git config core.filemode false`                                                                                 |
| 默认分支名                        | `git config --global init.defaultBranch main`                                                                    |
| `pull` 默认使用 rebase           | `git config --global pull.rebase true`                                                                           |
| 自动转换换行符（Windows）             | `git config --global core.autocrlf true`                                                                         |
| 自动转换换行符（Linux/macOS）         | `git config --global core.autocrlf input`                                                                        |
| 中文文件名不转义                     | `git config --global core.quotepath false`                                                                       |
| 保存凭据                         | `git config --global credential.helper store`（明文）或 `manager`（Windows 凭据管理器）                                      |
| 设置别名                         | `git config --global alias.st status`<br>`git config --global alias.lg "log --oneline --graph --all --decorate"` |
| 忽略文件名大小写变化（Windows/macOS 默认） | `git config core.ignorecase false`                                                                               |

## 查看与删除

``` bash
git config --list                     # 所有生效的配置
git config --list --show-origin       # 同时显示来自哪个文件
git config user.name                  # 查看单项
git config --global --unset user.name # 删除单项
git config --global -e                # 用编辑器打开全局配置文件
```

## 按目录自动切换身份

多账号（如公司/个人）时，在 `~/.gitconfig` 里用 `includeIf`，目录下的仓库自动加载另一份配置：

``` ini
[user]
    name = personal
    email = me@example.com

[includeIf "gitdir:~/work/"]
    path = ~/.gitconfig-work
```

`~/.gitconfig-work`：

``` ini
[user]
    name = work_name
    email = me@company.com
```

  - `gitdir/i:` 表示路径不区分大小写（Windows 常用），路径结尾的 `/` 表示匹配该目录下的所有仓库。
  - 这只影响 git 的提交署名等配置，不影响 `gh` 命令行所用的账号，详见
    [多账号切换](/0329_Tools_Github_多账号切换)。

## 相关

  - [代理配置](/0113_Tools_Git_config_proxy)
  - [Github SSH Key](/0123_Tools_Github_SSHKey)

## Reference

  - [git-config 官方文档](https://git-scm.com/docs/git-config)
  - [Pro Git: 自定义 Git - 配置
    Git](https://git-scm.com/book/zh/v2/自定义-Git-配置-Git)
