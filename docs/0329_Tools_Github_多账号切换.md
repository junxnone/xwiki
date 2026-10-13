---
Title | Tools Github 多账号切换
-- | --
Created @ | `2026-10-13T03:21:09Z`
Updated @| `2026-10-13T06:18:08Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/329)

---
# GitHub / Git CLI 多账号切换

## 1. 基本概念

Git 对 HTTPS 远程仓库的认证依赖 **credential helper** 机制，`gh` CLI 可以托管这个机制来实现多账号管理：

```bash
gh auth login        # 登录一个账号(可重复执行登录多个)
gh auth switch       # 切换当前 active 账号
gh auth status        # 查看所有已登录账号及哪个是 active
gh auth setup-git     # 让 git 的 credential helper 指向 gh
```

## 2. `gh auth switch` 如何影响 git

前提：执行过 `gh auth setup-git`。

原理：`gh auth setup-git` 会在 `~/.gitconfig` 里针对 `github.com` / `gist.github.com` 写入 **URL-scoped** 的 credential helper：

```
credential.https://github.com.helper=
credential.https://github.com.helper=!'C:\Program Files\GitHub CLI\gh.exe' auth git-credential
```

第一行空值表示"重置"该 host 之前继承的 helper 列表(比如系统级的 `manager`)，第二行再指定用 gh 的 helper。

这个 helper 每次被 git 调用时，都会**动态查询当前 active 账号**，所以 `gh auth switch` 切换后，下一次 `git clone/push/pull`(HTTPS)会自动用新账号，无需重新配置。

**例外**：只对 HTTPS 远程生效；SSH 远程(`git@github.com:...`)走的是 SSH key 认证，和 gh 账号切换无关。

## 3. `.gitconfig` 里的 `user.name` / `user.email` 不参与认证

- `user.name`/`user.email` 只影响 **commit 作者信息**(写入 commit 对象)，不参与 clone/push 的权限校验。
- 但 GitHub 网页把 commit 关联到哪个账号头像，是靠 **commit email 是否匹配该账号下已验证的邮箱**，和你用哪个 token 推送无关。混用多账号时，建议用 `includeIf "gitdir:..."` 按目录自动切换对应的 `user.name`/`user.email`。

## 4. 踩过的坑：凭据优先级冲突导致切换"没生效"

### 现象
`gh auth switch` 切到账号 A 后，`git clone` 私有仓库仍然报：
```
remote: Repository not found.
fatal: repository '...' not found
```
但 `gh repo view owner/repo` (走 gh 自己的 API 客户端)能正常查到仓库。

### 根因排查顺序

1. **检查 credential.helper 配置是否有冲突**：
   ```bash
   git config --list --show-origin | grep -i credential
   ```
   发现系统级(`C:\Program Files\Git\etc\gitconfig`)配置了 `credential.helper=manager`(Git Credential Manager)，可能和 gh 的 helper 抢先。

2. **直接测试 gh 的 credential helper 返回值**，排除是不是 gh 本身返回错了：
   ```cmd
   echo protocol=https> cred.txt
   echo host=github.com>> cred.txt
   echo.>> cred.txt
   gh auth git-credential get < cred.txt
   ```
   如果返回的 `username`/`password` 是对的，说明 gh 这一层没问题，问题出在更上游。

3. **真正的根因：`.netrc` / `_netrc` 文件**(Windows 下通常是 `%USERPROFILE%\_netrc`)。

   `.netrc` 是 **curl 库原生支持**的自动登录凭据文件，git 的 HTTP 传输基于 libcurl，curl 在发请求时会**先读取 netrc 并自动认证**，这个过程**完全绕过 git 自己的 credential.helper 链**(manager / store / gh 都不会被调用)。

   如果 netrc 里写死了某个账号(比如被某个 CI 脚本或历史操作写入过)：
   ```
   machine github.com
   login xxxx
   password ghp_xxxx
   ```
   那么不管 `gh auth switch` 切到哪个账号、credential.helper 配置得多正确，git 实际发出去的请求**永远用 netrc 里这个固定账号**认证。如果这个账号没有目标仓库的访问权限，GitHub 会返回 "Repository not found"(私有仓库权限不足时的标准回应，不会暴露"权限不够"还是"真不存在")。

### 解决

查看并清理 netrc 里的 github 条目：
```cmd
type %USERPROFILE%\_netrc
type %USERPROFILE%\.netrc
```
删除(或改成要用的账号对应的) `machine github.com` / `machine api.github.com` 段，把认证完全交给 `gh` 的动态 credential helper 管理，这样 `gh auth switch` 才能真正联动 git 操作。

## 5. 常用排查命令速查

| 目的 | 命令 |
|---|---|
| 查看所有已登录账号 & active 状态 | `gh auth status` |
| 切换 active 账号 | `gh auth switch --user <username>` |
| 让 git 使用 gh 托管认证 | `gh auth setup-git` |
| 查看所有层级(system/global/local)的 credential 配置及来源文件 | `git config --list --show-origin \| grep -i credential` |
| 手动测试 git 实际会拿到什么凭据 | 见上方 `cred.txt` 示例，喂给 `gh auth git-credential get` |
| 用 gh 自身 API 校验仓库是否对某账号可见 | `gh repo view <owner>/<repo>` (注意：这个不经过 git 的认证链，不能代表 git clone 一定成功) |
| 开启 http 请求级别调试 | `set GIT_CURL_VERBOSE=1` + `set GIT_TRACE=1` 再执行 git 命令 |
| 检查是否有 netrc 写死了固定账号 | `type %USERPROFILE%\_netrc` / `type %USERPROFILE%\.netrc` |

## 6. 多账号场景下的 CI 脚本模式(背景知识)

部分 CI 脚本会用这种方式写 netrc 实现免交互认证(不依赖 `gh` CLI)：

```bash
cat << EOF > ~/.netrc
machine github.com
  login not-used
  password $git_repo_token
machine api.github.com
  login not-used
  password $git_repo_token
EOF
```

- `machine github.com` 覆盖 git 的 clone/push/fetch
- `machine api.github.com` 覆盖脚本里直接 `curl https://api.github.com/...` 的 REST API 调用
- `login` 字段内容基本无意义，GitHub 的 PAT Basic Auth 只校验 password 是否为合法 token

这种一次性 CI 脚本在单账号场景下没问题，但如果同一台机器也用于日常多账号开发，残留的 netrc 条目就会导致"账号切换不生效"的问题(即第 4 节的坑)。

