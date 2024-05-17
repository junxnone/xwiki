-----

| Title     | Windows VSCode                                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-12-11T03:41:54Z`                               |
| Updated @ | `2024-05-17T08:17:15Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/299) |

-----

# Visual Studio Code

## 配置免密登录 Linux

  - **Windows** 下命令行生成 `ssh key`

<!-- end list -->

    ssh-keygen.exe -t rsa

  - 重命名生成的 `id_ras.pub` 为 `authorized_keys` 并复制到 **Linux** 下目录 `~/.ssh`
  - 下面开始无密连接吧

## 一直卡在 download `vscode server`

  - <kbd>File</kbd> -\> <kbd>Preferences</kbd> -\> <kbd>Setting</kbd>
  - 搜索 `remote.SSH.LocalServerDownload`
  - 设置为 `always`
  - 重新连接
