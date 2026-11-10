-----

| Title     | Tools Git config proxy                               |
| --------- | ---------------------------------------------------- |
| Created @ | `2018-12-10T06:05:14Z`                               |
| Updated @ | `2026-11-10T06:14:49Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/113) |

-----

# Git Proxy Setup

Git 访问远端有两类协议，代理的设置方式不同：

| 协议            | 远端地址形式                             | 代理设置                             |
| ------------- | ---------------------------------- | -------------------------------- |
| http / https  | `https://github.com/user/repo.git` | `http.proxy` 配置或环境变量             |
| ssh           | `git@github.com:user/repo.git`     | `~/.ssh/config` 的 `ProxyCommand` |
| git（`git://`） | `git://host/repo.git`              | `core.gitProxy`（基本已不再使用）         |

先用 `git remote -v` 看远端用的是哪种协议，再选对应的方式。

## http/https proxy

    git config --global http.proxy  http://proxy_ip:port

  - git 没有 `https.proxy` 这个配置项，**`http.proxy` 同时作用于 http 和 https
    远端**，所以只需要设置这一项。
  - 建议写上协议前缀，不同协议的写法：

| 类型              | 示例                                                    |
| --------------- | ----------------------------------------------------- |
| HTTP 代理         | `http://proxy_ip:port`                                |
| 带认证的 HTTP 代理    | `http://user:password@proxy_ip:port`（密码会明文写入配置，见下方注意） |
| SOCKS5 代理       | `socks5://127.0.0.1:1080`                             |
| SOCKS5，由代理端解析域名 | `socks5h://127.0.0.1:1080`                            |

### 只对某个站点设置代理

很多时候只有 github 需要代理，内网的 gitlab 不需要，用 URL 作用域限定：

    git config --global http.https://github.com.proxy http://proxy_ip:port

对应 `~/.gitconfig` 中的内容：

``` ini
[http "https://github.com"]
    proxy = http://proxy_ip:port
```

内网站点显式不走代理（空值）：

    git config --global http.https://gitlab.company.com.proxy ""

### 查看 http/https proxy

    git config --global --get http.proxy
    git config --list --show-origin | grep -i proxy       # 看所有来源

### unset http/https proxy

    git config --global --unset http.proxy
    git config --global --unset http.https://github.com.proxy

### 只对单条命令临时生效

``` bash
git -c http.proxy=http://proxy_ip:port clone https://github.com/user/repo.git
```

### 使用环境变量

git 也识别通用的代理环境变量（优先级低于 `http.proxy` 配置）：

``` bash
export http_proxy=http://proxy_ip:port
export https_proxy=http://proxy_ip:port
export no_proxy=localhost,127.0.0.1,.company.com     # 不走代理的地址
```

PowerShell：

``` powershell
$env:https_proxy = "http://proxy_ip:port"
```

### 证书与认证问题

  - 公司代理做 HTTPS 中间人解密时，会出现 `SSL certificate
    problem`。**正确做法**是把公司根证书加入信任：

<!-- end list -->

    git config --global http.sslCAInfo /path/to/company-ca.pem

  - 不要长期使用 `git config --global http.sslVerify
    false`，这会关闭证书校验，有被中间人攻击的风险；确需临时跳过，用单条命令的
    `-c http.sslVerify=false`。
  - 代理带账号密码时，避免把明文密码写进 `~/.gitconfig`，可以用环境变量或凭据管理工具。
  - 使用 Windows 的 `credential.helper=manager`
    保存了旧的凭据，代理认证失败时需要在“凭据管理器”里清理。

## ssh proxy

ssh 协议不走 `http.proxy`，需要给 ssh 配置代理，写在 `~/.ssh/config` 中，只对 `github.com`
生效：

### connect-proxy

    sudo apt install -y connect-proxy

  - `~/.ssh/config`

<!-- end list -->

    host github.com
        ProxyCommand connect -a none -S your_proxy_ip:port %h %p

  - `connect` 的参数：`-S` 表示 SOCKS 代理；**如果是 HTTP 代理要改成 `-H`**：

<!-- end list -->

    host github.com
        ProxyCommand connect -H your_proxy_ip:port %h %p

### nc / ncat

不想装 `connect-proxy` 时，可用 netcat（需要 OpenBSD 版 `nc`，Git Bash 里可用
`connect.exe`，见下）：

    host github.com
        ProxyCommand nc -X connect -x your_proxy_ip:port %h %p      # HTTP 代理
        # ProxyCommand nc -X 5 -x your_proxy_ip:port %h %p          # SOCKS5 代理

### Windows（Git Bash）

Git for Windows 自带 `connect.exe`，`~/.ssh/config` 中：

    host github.com
        ProxyCommand connect -H your_proxy_ip:port %h %p

### ssh 走 443 端口

有的网络封锁了 22 端口，但能访问 HTTPS 代理或直连 443，Github 提供了 443 端口的 ssh 服务：

    host github.com
        HostName ssh.github.com
        Port 443
        User git

### 测试

    ssh -T git@github.com
    ssh -vT git@github.com      # 打开调试，观察是否经过代理

### socat

  - Create `/usr/bin/git-proxy`

<!-- end list -->

    #!/bin/sh
    exec /usr/bin/socat stdio SOCKS:[your_ip_or_url]:$1:$2

> 原来的脚本里 `if [ $? -eq 0 ]` 判断的是上一条命令的退出码，没有实际意义；这里改为直接 `exec socat`。
> `SOCKS:` 地址的完整写法是
> `SOCKS4A:<代理地址>:<目标主机>:<目标端口>,socksport=<代理端口>`，以实际使用的
> socat 版本文档为准。

    sudo chmod +x /usr/bin/git-proxy

  - Setup `gitproxy`

<!-- end list -->

    git config --global core.gitProxy git-proxy

  - `core.gitProxy` 只作用于 `git://` 协议，对 ssh 和 https 无效；现在 `git://`
    很少使用，多数场景用上面的 http 或 ssh 方式即可。

## 常见问题

| 现象                                                                  | 可能原因 / 处理                                                              |
| ------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `Failed to connect to github.com port 443` / `Connection timed out` | 没设置代理，或代理地址端口不对                                                        |
| `Proxy CONNECT aborted` / 407                                       | 代理需要认证                                                                 |
| `Could not resolve proxy`                                           | 代理地址写错，或带了不识别的协议前缀                                                     |
| `SSL certificate problem`                                           | 公司代理做了 HTTPS 解密，需要信任公司根证书                                              |
| 设置了全局代理后内网仓库访问失败                                                    | 改用按站点的 `http.<url>.proxy`，或用 `no_proxy`                                |
| `git clone` 突然很慢                                                    | 代理速度问题；可先 `git clone --depth 1` 浅克隆                                    |
| 改了代理没生效                                                             | `git config --list --show-origin` 检查是否有其他层级（system/local）的配置覆盖，或环境变量覆盖 |

## Reference

  - [一文让你了解如何为 Git
    设置代理](https://ericclose.github.io/git-proxy-config.html)
  - [git-config:
    http.proxy](https://git-scm.com/docs/git-config#Documentation/git-config.txt-httpproxy)
  - [Github 文档: 在 HTTPS 端口使用
    SSH](https://docs.github.com/zh/authentication/troubleshooting-ssh/using-ssh-over-the-https-port)
  - [Git 配置](/0112_Tools_Git_config)
