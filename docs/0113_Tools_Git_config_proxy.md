---
Title | Tools Git config proxy
-- | --
Created @ | `2018-12-10T06:05:14Z`
Updated @| `2025-10-27T00:55:47Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/113)

---
# Proxy Setup

- http/https proxy
- git proxy

## http/https proxy

```
git config --global http.proxy  proxy_ip:port
git config --global https.proxy proxy_ip:port
```

### unset http/https proxy

```
git config --global --unset http.proxy
git config --global --unset https.proxy
```


## ssh proxy

### connect-proxy

```
sudo apt install -y connect-proxy
```

- `~/.ssh/config`

```
host github.com
    ProxyCommand connect -a none -S your_proxy_ip:port %h %p
```

### socat

- Create `/usr/bin/git-proxy`
```
#!/bin/sh
if [ $? -eq 0 ]; then
    /usr/bin/connect $@
else
    exec /usr/bin/socat stdio SOCKS:[your_ip_or_url]:$1:$2
fi
```

```
sudo chmod +x /usr/bin/git-proxy
```

- Setup `gitproxy`

```
git config --global core.gitProxy git-proxy
```

## Reference
- [一文让你了解如何为 Git 设置代理](https://ericclose.github.io/git-proxy-config.html)


