---
Title | Windows VSCode
-- | --
Created @ | `2023-12-11T03:41:54Z`
Updated @| `2024-06-26T07:57:04Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/299)

---
# Visual Studio Code

## 配置免密登录 Linux
- **Windows** 下命令行生成 `ssh key`

```
ssh-keygen.exe -t rsa
```
- 重命名生成的 `id_ras.pub` 为 `authorized_keys` 并复制到 **Linux** 下目录 `~/.ssh`
- 下面开始无密连接吧

## 一直卡在 download `vscode server`
- <kbd>File</kbd> -> <kbd>Preferences</kbd> -> <kbd>Setting</kbd>
- 搜索 `remote.SSH.LocalServerDownload`
- 设置为 `always`
- 重新连接

### 手动下载

####  获取 `Commit ID`
- 在 VSCode 的 <kbd>About</kbd> 获取

```
Version: 1.90.2 (user setup)
Commit: 5437499feb04f7a586f677b155b039bc2b3669eb
Date: 2024-06-18T22:34:26.404Z
Electron: 29.4.0
ElectronBuildId: 9728852
Chromium: 122.0.6261.156
Node.js: 20.9.0
V8: 12.2.281.27-electron.0
OS: Windows_NT x64 10.0.22631
```

#### 手动下载 `vscode server`

```
wget https://update.code.visualstudio.com/commit:COMMIT_ID/server-linux-x64/stable
```
> [!NOTE]
> 替换 COMMIT_ID

#### 解压到相应文件夹 
- 各个版本有可能改变 目前是 `~/.vscode-server/cli/servers`  `vscode@1.90.2`



```
tree Stable-5437499feb04f7a586f677b155b039bc2b3669eb/ -d -L 2
Stable-5437499feb04f7a586f677b155b039bc2b3669eb/
└── server
    ├── bin
    ├── extensions
    ├── node_modules
    └── out
```





