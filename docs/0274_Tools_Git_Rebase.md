---
Title | Tools Git Rebase
-- | --
Created @ | `2023-06-26T01:34:29Z`
Updated @| `2026-11-10T06:07:00Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/274)

---
# Git Rebase

`rebase` 把一串提交**在另一个基点上重新应用一遍**，用来让历史保持线性，或者整理本地尚未推送的提交（改顺序、改说明、合并、删除）。

## 两种用途

用途 | 命令
-- | --
把当前分支变基到另一个分支之上（保持线性历史） | `git rebase main`
交互式整理最近的提交 | `git rebase -i HEAD~N`

### 变基到另一个分支

![image](https://github.com/junxnone/xwiki/assets/2216970/801ca277-58fb-454f-957e-ab04afe6b8e3)

↓ `git switch feature && git rebase main`

![image](https://github.com/junxnone/xwiki/assets/2216970/8d94378b-0e69-42f9-a3b2-a921b3140442)

- feature 上的提交被**重新生成**（sha 会变），接到 main 最新提交之后。
- 之后切到 main 做 `git merge feature` 就是快进合并，历史是一条直线。

## 交互式 rebase

```bash
git rebase -i HEAD~3          # 整理最近 3 个提交
git rebase -i <commit>        # 整理 <commit> 之后的所有提交（不含 <commit>）
git rebase -i --root          # 从第一个提交开始
```

执行后编辑器里列出提交（**最旧的在最上面**），每行开头是动作，修改动作后保存退出即可：

```
pick a1b2c3d add login page
pick e4f5a6b fix typo
pick 7c8d9e0 add logout

# Commands:
# p, pick   = 使用该提交
# r, reword = 使用该提交，但修改提交说明
# e, edit   = 使用该提交，但停下来让你修改内容
# s, squash = 合并到前一个提交，并保留双方说明供编辑
# f, fixup  = 合并到前一个提交，丢弃本提交的说明
# d, drop   = 删除该提交
# x, exec   = 执行一条 shell 命令
```

### 常见操作

目标 | 做法
-- | --
调整提交顺序 | 直接上下移动行
删除某个提交 | 把 `pick` 改成 `drop`，或删掉那一行
修改提交说明 | `pick` → `reword`（或 `r`）
把多个提交合并成一个 | 保留第一行 `pick`，其余改为 `squash`（`s`）或 `fixup`（`f`）
拆分一个提交 | `pick` → `edit`，停下后 `git reset HEAD^`，再分多次 `git add` + `git commit`，最后 `git rebase --continue`

### 合并最近 3 个提交示例

```
pick a1b2c3d add login page
squash e4f5a6b fix typo
squash 7c8d9e0 add logout
```

保存后会再打开一次编辑器，让你编辑合并后的提交说明。

### fixup 工作流

修复之前某个提交的小问题时，不必手动整理：

```bash
git commit --fixup <commit>              # 生成 "fixup! ..." 提交
git rebase -i --autosquash <commit>^     # 自动把 fixup 提交排到目标之后并标记 fixup
```

## 过程中的控制命令

```bash
git rebase --continue         # 解决冲突并 git add 之后继续
git rebase --skip             # 跳过当前这个提交
git rebase --abort            # 放弃，恢复到 rebase 之前
```

## 与 merge 的区别

 | merge | rebase
-- | -- | --
历史 | 保留分叉，产生合并提交 | 线性
是否改写提交 | 否 | 是（sha 改变）
适合 | 共享分支合并 | 本地整理、更新自己的 feature 分支

## 注意

- **不要对已经推送、别人可能已在使用的提交做 rebase**，会造成他人历史冲突。必须强推时用 `git push --force-with-lease`，比 `--force` 安全。
- rebase 出问题别慌，`git reflog` 能找到 rebase 之前的 HEAD，`git reset --hard <sha>` 回去。
- `git pull --rebase` 等价于 fetch 之后 rebase，可避免产生多余的 merge 提交；`git config --global pull.rebase true` 设为默认。
- 变基到别的分支：`git rebase --onto <newbase> <oldbase> <branch>` 可以把一段提交移植到新基点上。

## Reference
- [git-rebase 官方文档](https://git-scm.com/docs/git-rebase)
- [Pro Git: Rebasing](https://git-scm.com/book/zh/v2/Git-分支-变基)

