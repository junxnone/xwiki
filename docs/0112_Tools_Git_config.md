---
Title | Tools Git config
-- | --
Created @ | `2018-12-14T07:45:42Z`
Updated @| `2023-04-10T02:32:44Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/112)

---
Target | Commands
-- | --
设置**默认编辑器** | `git config --global core.editor vi`
为单独仓库设置**用户名邮箱** |  **切换到 `.git` 所在目录** <br>`git config user.name "your_name"`<br>` git config user.email "your_email"`
忽略文件权限更改 | `git config core.filemode false`

- `--local` : 当前repo 设置
- `--global` : 全局设置

