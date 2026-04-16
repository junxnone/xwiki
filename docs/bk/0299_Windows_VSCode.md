-----

| Title     | Windows VSCode                                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-12-11T03:41:54Z`                               |
| Updated @ | `2026-04-16T02:11:02Z`                               |
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

### 手动下载

#### 获取 `Commit ID`

  - 在 VSCode 的 <kbd>About</kbd> 获取

<!-- end list -->

    Version: 1.90.2 (user setup)
    Commit: 5437499feb04f7a586f677b155b039bc2b3669eb
    Date: 2024-06-18T22:34:26.404Z
    Electron: 29.4.0
    ElectronBuildId: 9728852
    Chromium: 122.0.6261.156
    Node.js: 20.9.0
    V8: 12.2.281.27-electron.0
    OS: Windows_NT x64 10.0.22631

#### 手动下载 `vscode server`

    wget https://update.code.visualstudio.com/commit:COMMIT_ID/server-linux-x64/stable

> \[\!NOTE\] 替换 COMMIT\_ID

#### 解压到相应文件夹

  - 各个版本有可能改变 目前是 `~/.vscode-server/cli/servers` `vscode@1.90.2`

<!-- end list -->

    tree Stable-5437499feb04f7a586f677b155b039bc2b3669eb/ -d -L 2
    Stable-5437499feb04f7a586f677b155b039bc2b3669eb/
    └── server
        ├── bin
        ├── extensions
        ├── node_modules
        └── out

## 公式加空格

  - 有些 `markdown` 渲染器(例如 github) 必须在公式 `$` 前后加空格
  - 使用 `vscode` 批量编辑：
  - 打开替换对话框，打开正则表达式模式输入: `\$(.*?)\$` , 可以查找所有以 `$` 开始并结束的公式。
  - 替换为 `  $&  `

> \[\!NOTE\] `$&` 前后各一个空格

> \[\!NOTE\] **`$` 可以表示的其他变量**
> 在正则表达式的替换操作中，除了`$1`用于引用第一个捕获组匹配到的内容外，还有以下变量（假设存在多个捕获组）：
> - `$2`：引用第二个捕获组匹配到的内容。 - `$3`：引用第三个捕获组匹配到的内容。 - …… -
> `$n`：引用第`n`个捕获组匹配到的内容。
> 例如，正则表达式`(\d+)-(\w+)`可以匹配类似`123-abc`这样的字符串，其中有两个捕获组，在替换时，`$1`会被替换为`123`，`$2`会被替换为`abc`。
> 此外，在某些情况下还可能会用到以下特殊变量： -
> `$&`：表示整个匹配到的字符串。例如，对于字符串`abc`，使用正则表达式`b`进行匹配，在替换时`$&`会被替换为`b`。
> - `$``：表示匹配到的字符串之前的部分。例如，对于字符串`abc`，使用正则表达式`b`进行匹配，`$\`\`会被替换为`a`。 -
> \`$'\`：表示匹配到的字符串之后的部分。例如，对于字符串\`abc\`，使用正则表达式\`b\`进行匹配，\`$'\`会被替换为\`c\`。
> 需要注意的是，不同的文本编辑器或编程语言对正则表达式变量的支持和使用方式可能会略有不同。在VS
> Code中，主要就是使用\`$n\`（\`n\`为数字，表示捕获组的序号）来引用捕获组的内容进行替换操作。

## 替换空格为换行符

  - 选中待替换内容 -\> <kbd>Ctrl</kbd> + <kbd>c</kbd> 复制
  - <kbd>Ctrl</kbd> + <kbd>f</kbd> 查找
  - 选中 `.*` 进入正则匹配模式
  - 替换内容为 `\n`

## 访问远程 Windows

### 远程 windows 安装 sshd

    # 安装服务器
    Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
    # 安装客户端（本地也需要）
    Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

  - 启动 SSH 服务并设为开机自启

<!-- end list -->

    # 启动服务
    Start-Service sshd
    # 设为开机自启
    Set-Service -Name sshd -StartupType 'Automatic'
    # 验证状态（Running 即成功）
    Get-Service sshd

  - 防火墙 22 端口

<!-- end list -->

    New-NetFirewallRule -Name 'OpenSSH-Server-In-TCP' -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22

> 现在应该可以通过 ssh 连接到改机器了 可能 vscode 的 文件夹浏览功能不能用，需如下设置 sftp 功能

### 设置 sftp

  - 编辑远程 windows sshd 配置文件 `C:\ProgramData\ssh\sshd_config`

<!-- end list -->

``` 
Subsystem sftp sftp-server.exe
# 允许用户目录访问
AllowUsers 你的用户名
# 禁用严格权限（Win11 常见坑）
StrictModes no

```

  - 重启 sshd 服务

<!-- end list -->

    Restart-Service sshd

### 免密登录

#### 1\. 本地电脑：生成密钥（不需要密码）

打开 **PowerShell** 执行：

``` powershell
ssh-keygen -t ed25519
```

一路回车，**不要设置密码**。

生成位置默认：

    C:\Users\你的用户名\.ssh\
    id_ed25519      （私钥，自己留着）
    id_ed25519.pub  （公钥，要传到远程Windows）

-----

#### 2\. 把公钥放到远程 Win11（关键步骤）

  - **远程 Win11 操作：**

<!-- end list -->

1.  新建文件（必须这个路径和名字）

<!-- end list -->

    C:\ProgramData\ssh\administrators_authorized_keys

2.  把你本地 `id_ed25519.pub` 里的**一长串内容**复制进去，保存。

3.  管理员 PowerShell 执行**权限修复命令**（必须执行，否则免密无效）：

<!-- end list -->

``` powershell
icacls "C:\ProgramData\ssh\administrators_authorized_keys" /inheritance:r /grant "Administrators:F" /grant "SYSTEM:F"
```

4.  重启 sshd

<!-- end list -->

``` powershell
Restart-Service sshd
```

-----

#### 3\. 本地 VSCode 配置免密连接

打开本地：

    C:\Users\你\.ssh\config

写入：

    Host my-win11
      HostName 192.168.xxx.xxx    # 远程Windows IP
      User 远程Windows用户名      # 比如 admin / zhangsan
      IdentityFile C:\Users\你\.ssh\id_ed25519
      StrictHostKeyChecking no

保存。

-----

#### 4\. 测试免密

本地 PowerShell 直接输：

``` powershell
ssh my-win11
```

**不需要密码直接进去** = 成功。

然后 VSCode 点 `Connect Host` → `my-win11`，也不会要密码。

-----
