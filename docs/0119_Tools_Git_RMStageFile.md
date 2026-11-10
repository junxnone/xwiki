---
Title | Tools Git RMStageFile
-- | --
Created @ | `2019-02-18T17:16:56Z`
Updated @| `2026-11-10T06:06:51Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/119)

---
# 移除 stage 文件

- 使用 `git add file` ，发现添加错文件，从 stage 中移除文件

场景 | 命令
-- | --
该文件**不在** repository 内（新文件，从未提交过），想取消暂存 | `git rm --cached filename`
该文件**已经在** repository 内，想取消暂存 | `git reset HEAD filename`
任意文件，取消暂存（Git 2.23+ 推荐） | `git restore --staged filename`
取消暂存所有文件 | `git restore --staged .`（或 `git reset`）

## 说明

- `git restore --staged` 只把文件移出暂存区，**工作区的修改保留**。
- 要连工作区的修改也丢弃，用 `git restore filename`（**不可恢复**，慎用）。
- `git rm --cached` 的含义是“从版本控制中移除，但保留磁盘上的文件”：
  - 对已跟踪的文件执行后提交，等于以后不再跟踪它；
  - 常用于把已经提交的文件加入 `.gitignore` 之后，让 git 停止跟踪：

  ```bash
  git rm --cached filename
  git rm -r --cached dir/        # 目录
  echo "filename" >> .gitignore
  git commit -m "stop tracking filename"
  ```

## 误 add 了敏感文件

- 还没 commit：按上表取消暂存，并加入 `.gitignore`。
- 已经 commit 但没 push：`git reset --soft HEAD~1` 撤回提交后再取消暂存。
- 已经 push：把它视为已经泄露，**先轮换密钥/密码**，再用 `git filter-repo` 之类的工具清理历史。

## Reference
- [git-restore 官方文档](https://git-scm.com/docs/git-restore)
- [git-rm 官方文档](https://git-scm.com/docs/git-rm)

