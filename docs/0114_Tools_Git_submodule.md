---
Title | Tools Git submodule
-- | --
Created @ | `2018-12-10T05:55:39Z`
Updated @| `2026-11-10T06:06:38Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/114)

---
# Git Submodule
 
- git 包含嵌套的概念, 仓库中可以包含另一个仓库
- 父仓库**只记录子仓库的地址（`.gitmodules`）和所指向的具体 commit**，不保存子仓库的文件历史。所以子仓库的更新不会自动出现在父仓库里，需要在父仓库中提交一次新的指针。

## 相关文件

文件 | 说明
-- | --
`.gitmodules` | 在父仓库根目录，记录每个子模块的路径和 url，**需要提交**
`.git/config` | 本地配置，`submodule init` 时会把 `.gitmodules` 中的信息拷贝过来
`.git/modules/<name>` | 子仓库实际的 `.git` 数据存放处
子模块目录下的 `.git` 文件 | 内容是 `gitdir: ../.git/modules/<name>`，指向上一行的目录

`.gitmodules` 示例：

```ini
[submodule "subdir"]
    path = subdir
    url = https://xxxx.git
    branch = main
```

## 新建包含子仓库的仓库

```
cd workdir
git init
git submodule add https://xxxx.git subdir
```

- 指定分支：`git submodule add -b main https://xxxx.git subdir`
- 执行后会修改 `.gitmodules` 并在暂存区加入 `subdir`（指向某个 commit），需要 `git commit` 提交。

## 克隆含子模块的仓库

```bash
git clone --recursive <url>                  # 克隆时一并拉取子模块
# 或者已经 clone 之后：
git submodule update --init --recursive
```

- 不加 `--recursive` 克隆后，子模块目录是空的。

## update 所有仓库

```
git submodule update --init --recursive
```

- `update` 会把子模块检出到**父仓库记录的那个 commit**，因此子模块会处于游离 HEAD（detached HEAD）状态，这是正常的。

## 更新子模块到远端最新

```bash
git submodule update --remote                # 更新到子模块所跟踪分支的最新提交
git submodule update --remote --merge        # 更新并合并到当前分支
git pull --recurse-submodules                # 拉取父仓库的同时更新子模块
```

- 更新之后，父仓库里子模块指针变了，需要在父仓库提交这个变化：

```bash
git add subdir
git commit -m "update subdir"
```

## 在子模块里修改并提交

```bash
cd subdir
git switch main                  # 先离开游离 HEAD，切到分支
# 修改、git add、git commit
git push                         # 先推送子模块
cd ..
git add subdir
git commit -m "bump subdir"
git push                         # 再推送父仓库
```

- **一定要先推送子模块，再推送父仓库**，否则别人拉取父仓库后找不到那个 commit。
- 保险做法：`git push --recurse-submodules=check`（检查子模块是否已推送）或 `=on-demand`（自动推送）。

## 常用命令

```bash
git submodule status                         # 查看子模块当前 commit
git submodule foreach 'git pull origin main' # 对每个子模块执行命令
git submodule sync --recursive               # 把 .gitmodules 里的 url 同步到 .git/config
git config submodule.recurse true            # 让 pull/checkout 等命令默认递归子模块
git diff --submodule                         # 在 diff 中显示子模块的提交变化
```

## Git 更改submodule 的地址


分别更改如下文件中的子模块地址
- `.gitmodules`
- `.git/config`

> 在运行 `git submodule update --init --recursive` 时，`.gitmodules` 中的 submodule 会更新到 `.git/config` 中，所以运行此命令之前可以只更新 `.gitmodules` 文件

也可以用命令一步完成：

```bash
git submodule set-url <子模块路径> <新url>     # Git 2.25+ ，同时更新 .gitmodules
git submodule sync --recursive                # 同步到 .git/config 和子仓库的 remote
```

> 原文写的 `.submodule` 是笔误，文件名是 `.gitmodules`。

## 移除子模块

按顺序执行（旧版 git 需要手动删除，新版 `git rm` 会自动清理 `.gitmodules` 中的条目）：

### 停止跟踪子模块
- 取消子模块的初始化（从 `.git/config` 中移除，并清空工作区的子模块目录内容）
```
git submodule deinit -f <子模块路径>
```

### 从项目中移除子模块的记录
- 从 `.gitmodules` 文件和项目的暂存区中移除子模块的相关信息

```
git rm -f <子模块路径>
```

### 提交更改

```
git commit -m "Remove submodule"
```

### 彻底清理（可选）

子模块的仓库数据仍保存在 `.git/modules` 下，需要的话手动删除：

```bash
rm -rf .git/modules/<子模块名>
```

## 常见问题

- 子模块目录是空的：没有执行 `git submodule update --init`。
- 拉取父仓库后 `git status` 显示子模块 `modified`：子模块的 commit 与父仓库记录的不一致，执行 `git submodule update` 即可恢复。
- `fatal: no submodule mapping found in .gitmodules`：目录被当作子模块记录但 `.gitmodules` 里没有对应条目，用 `git rm --cached <路径>` 清理后重新添加。
- 子模块使用 SSH 地址而 CI 里没有密钥：把 `.gitmodules` 的 url 改成 HTTPS，或在 CI 里配置 `url.<base>.insteadOf`。
- 经常嫌麻烦的话，可以考虑 `git subtree` 或包管理器作为替代。

## Reference
- [git-submodule 官方文档](https://git-scm.com/docs/git-submodule)
- [Pro Git: 子模块](https://git-scm.com/book/zh/v2/Git-工具-子模块)

