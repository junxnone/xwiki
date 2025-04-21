---
Title | Windows VSCode
-- | --
Created @ | `2023-12-11T03:41:54Z`
Updated @| `2025-04-21T06:53:59Z`
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

## 公式加空格

- 有些 `markdown` 渲染器(例如 github) 必须在公式 `$` 前后加空格
- 使用 `vscode` 批量编辑：
- 打开替换对话框，打开正则表达式模式输入: `\$(.*?)\$` , 可以查找所有以 `$` 开始并结束的公式。
- 替换为 `   $&  ` 

> [!NOTE]
> `$&` 前后各一个空格



>[!NOTE]
> 在正则表达式的替换操作中，除了`$1`用于引用第一个捕获组匹配到的内容外，还有以下变量（假设存在多个捕获组）：
    - `$2`：引用第二个捕获组匹配到的内容。
    - `$3`：引用第三个捕获组匹配到的内容。
    - ……
    - `$n`：引用第`n`个捕获组匹配到的内容。
   例如，正则表达式`(\d+)-(\w+)`可以匹配类似`123-abc`这样的字符串，其中有两个捕获组，在替换时，`$1`会被替换为`123`，`$2`会被替换为`abc`。
  此外，在某些情况下还可能会用到以下特殊变量：
    - `$&`：表示整个匹配到的字符串。例如，对于字符串`abc`，使用正则表达式`b`进行匹配，在替换时`$&`会被替换为`b`。
    - `$``：表示匹配到的字符串之前的部分。例如，对于字符串`abc`，使用正则表达式`b`进行匹配，`$``会被替换为`a`。
    - `$'`：表示匹配到的字符串之后的部分。例如，对于字符串`abc`，使用正则表达式`b`进行匹配，`$'`会被替换为`c`。
  > 需要注意的是，不同的文本编辑器或编程语言对正则表达式变量的支持和使用方式可能会略有不同。在VS Code中，主要就是使用`$n`（`n`为数字，表示捕获组的序号）来引用捕获组的内容进行替换操作。
  
  
