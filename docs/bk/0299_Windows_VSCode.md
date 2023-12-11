-----

| Title     | Windows VSCode                                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-12-11T03:41:54Z`                               |
| Updated @ | `2023-12-11T03:41:54Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/299) |

-----

# Visual Studio Code

## 配置免密登录 Linux

  - Windows 下命令行生成 `ssh key`

<!-- end list -->

    ssh-keygen.exe -t rsa

  - 创建文件 `authorized_keys`，并复制 `id_rsa.pub` 内容

  - 复制 `authorized_keys` 到 Linux 下 `.ssh/` 下

  - 下面开始无密连接吧
