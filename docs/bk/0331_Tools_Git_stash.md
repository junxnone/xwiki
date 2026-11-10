-----

| Title     | Tools Git stash                                      |
| --------- | ---------------------------------------------------- |
| Created @ | `2026-11-10T05:42:58Z`                               |
| Updated @ | `2026-11-10T05:42:58Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/331) |

-----

# git stash

`git stash` 把工作区和暂存区里**尚未提交的改动**临时存起来，让工作目录回到干净的 `HEAD`
状态，之后可以随时取回。典型场景：改到一半需要切分支修
bug、拉取远端更新前工作区不干净、想先验证一下干净状态下的行为。

stash 本质上是**一组特殊的 commit**，保存在 `refs/stash`，按栈（后进先出）管理，`stash@{0}`
是最新的一条。stash 是本地的，不会被 `push`。

## 基本用法

``` bash
git stash                       # 存起工作区和暂存区的改动（等价 git stash push）
git stash list                  # 查看栈
git stash pop                   # 取回最新一条并从栈中删除
git stash apply                 # 取回最新一条，但保留在栈中
git stash drop                  # 删除最新一条
git stash clear                 # 清空所有 stash
```

流程示例：

``` bash
# 正在 feature 分支上改代码，突然要修线上问题
git stash push -m "feature: 半成品登录页"
git switch main
# ...修复、提交...
git switch feature
git stash pop
```

## 常用命令速查

| 命令                                    | 说明                                        |
| ------------------------------------- | ----------------------------------------- |
| `git stash` / `git stash push`        | 存起已跟踪文件的改动（含暂存区）                          |
| `git stash push -m "msg"`             | 加说明，**强烈建议**，不然 `list` 里只有一堆 `WIP on ...` |
| `git stash push -u`                   | 同时存起**未跟踪**文件（`--include-untracked`）      |
| `git stash push -a`                   | 连被 `.gitignore` 忽略的文件也存（`--all`，慎用）       |
| `git stash push -k`                   | 存起改动，但**保留暂存区**不动（`--keep-index`）         |
| `git stash push -p`                   | 交互式挑选要存的代码块（`--patch`）                    |
| `git stash push -- path/a path/b`     | 只存指定路径的改动                                 |
| `git stash list`                      | 列出所有 stash                                |
| `git stash show`                      | 查看最新一条的文件级统计                              |
| `git stash show -p stash@{1}`         | 查看指定一条的完整 diff                            |
| `git stash apply stash@{2}`           | 应用指定的一条                                   |
| `git stash pop stash@{2}`             | 应用并删除指定的一条                                |
| `git stash drop stash@{2}`            | 删除指定的一条                                   |
| `git stash branch <name> [stash@{n}]` | 基于该 stash 产生时的提交新建分支并取回                   |
| `git stash clear`                     | 删除全部 stash                                |

> `stash@{n}` 里的 `{}` 在 PowerShell 中有特殊含义，需要加引号：`git stash apply
> 'stash@{1}'`。

## 细节与注意点

### 默认只存已跟踪文件

  - 新建的未跟踪文件不会被存起来，`git stash` 后它们仍留在工作区。要一起存用 `-u`。
  - `.gitignore` 忽略的文件只有 `-a` 才会存，通常不需要。

### `pop` 与 `apply`

  - `pop` = `apply` + `drop`。**如果 `pop` 时发生冲突，stash 不会被删除**，解决冲突后需手动
    `git stash drop`。
  - 不确定能否干净应用时，先 `apply`，确认没问题再 `drop`。

### 暂存状态默认不恢复

`pop` / `apply` 默认把原来已暂存的改动恢复成**未暂存**。想保持暂存状态加 `--index`：

``` bash
git stash pop --index
```

### 冲突处理

取回时若与当前代码冲突，会像合并冲突一样标记文件，手动解决后 `git add` 即可。取回的内容不会自动提交。

### 在不同分支上取回

stash 不绑定分支，可以在任意分支上 `pop`。如果当前代码与存入时差别很大，容易冲突；这时用 `git stash branch`
回到存入时的基点新建分支，更稳妥。

### 误删 / 误 `pop` 后找回

`drop`、`clear` 之后，stash commit 在垃圾回收前还在，可以找回：

``` bash
git fsck --unreachable | grep commit     # 找悬空 commit
git show <sha>                           # 确认内容
git stash store -m "recovered" <sha>     # 放回 stash 栈
```

## 实用技巧

### 只存部分改动

``` bash
git stash push -p                        # 逐块选择
git stash push -- src/foo.py             # 按文件
git stash push -u -- newfile.txt         # 含未跟踪文件，按路径
```

### 存起暂存区之外的改动，保留暂存内容

想先提交已暂存的内容，再处理其余改动：

``` bash
git stash push -k -u -m "wip: 其余改动"
git commit -m "..."                      # 此时提交的是暂存区
git stash pop
```

### 把 stash 当作临时快照而不清空工作区

``` bash
git stash create                         # 生成 stash commit 并输出 sha，不改动工作区、不入栈
git stash store -m "snapshot" <sha>      # 需要时再放入栈
```

### 查看某条 stash 与当前工作区的差异

``` bash
git diff stash@{0}
git diff stash@{0}^1 stash@{0}           # 该 stash 相对其基点的改动
```

### 批量或自动化

  - `git pull --autostash` / `git rebase --autostash`：操作前自动 stash，完成后自动
    pop。
  - 配置默认：`git config --global rebase.autoStash true`。

## stash 的内部结构

一次 `git stash` 会创建一个合并提交，包含：

  - 父 1：存入时的 `HEAD`
  - 父 2：暂存区（index）的快照
  - 带 `-u` 时还有父 3：未跟踪文件的快照

所以 `stash@{0}^1`、`stash@{0}^2`、`stash@{0}^3` 可以分别查看这三部分。栈的历史记录在
reflog（`.git/logs/refs/stash`）中。

## 使用建议

  - 总是写 `-m` 说明，stash 多了很难分辨。
  - stash 适合**短期**暂存；超过一两天的工作用临时分支提交更安全，stash 无远端备份，也容易被遗忘。
  - 切分支前如果只是想保存，也可以直接 `git commit -m "wip"`，之后再 `git commit --amend` 或
    `git reset --soft HEAD~1`。
  - 需要多份并行的半成品改动，优先用 `git worktree`，而不是反复 stash。

## Reference

  - [git-stash 官方文档](https://git-scm.com/docs/git-stash)
  - [Pro Git: Stashing and
    Cleaning](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)
  - [git-worktree 官方文档](https://git-scm.com/docs/git-worktree)
