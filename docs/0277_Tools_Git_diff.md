---
Title | Tools Git diff
-- | --
Created @ | `2023-07-05T14:56:23Z`
Updated @| `2026-11-10T06:07:03Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/277)

---
# Git diff

`git diff` 比较两个“状态”之间的差异。不带参数时比较的是**工作区**与**暂存区**。

## 比较对象一览

目标 | 命令
-- | --
工作区 vs 暂存区（尚未 `git add` 的改动） | `git diff`
暂存区 vs 最近一次提交（已 `git add` 将要提交的改动） | `git diff --staged`（同 `--cached`）
工作区 vs 最近一次提交（暂存和未暂存的全部改动） | `git diff HEAD`
某个文件 | `git diff file`
两个提交之间 | `git diff commit1 commit2`
某次提交相对其父提交 | `git show <commit>` 或 `git diff <commit>^ <commit>`
两个分支 | `git diff main dev`
两个分支（只看某目录/文件） | `git diff main dev -- path`

> 路径前加 `--` 可以和分支名区分，避免歧义。

## 查看当前文件更改部分

```bash
git diff file
git diff --staged file
```

## 查看 commit 之间的区别

```bash
git diff commit-id commit-id
git diff HEAD~3 HEAD                  # 最近 3 次提交的总改动
git diff HEAD~1 HEAD -- file          # 某个文件相对上一次提交的变化
```

## 查看两个分支的不同

```bash
git diff main dev
git diff main dev path
git diff main dev file
git diff main...dev                   # 三个点：dev 相对两者共同祖先的改动（相当于 PR 页面看到的）
git diff main..dev                    # 两个点：等价于 git diff main dev
```

## 常用选项

选项 | 说明
-- | --
`--stat` | 只看每个文件改动的行数统计
`--name-only` | 只列出变动的文件名
`--name-status` | 文件名 + 状态（A 新增 / M 修改 / D 删除 / R 重命名）
`--shortstat` | 只输出总的增删行数
`-w` | 忽略空白字符差异（`--ignore-all-space`）
`--word-diff` | 按单词而不是按行显示差异，适合文档
`--color-words` | 同上，用颜色标出变化的单词
`-U<n>` | 上下文行数，如 `-U0` 不显示上下文
`--diff-filter=M` | 只看某类变更（如 `M` 修改，`A` 新增，`D` 删除）
`-S"text"` | 找出新增/删除了 `text` 的提交（用于 `git log -S`）

```bash
git diff --stat main dev
git diff --name-status HEAD~5 HEAD
git diff --word-diff README.md
```

## 外部工具

```bash
git difftool                          # 用外部工具比较
git config --global diff.tool vimdiff
git config --global difftool.prompt false
git diff --no-index a.txt b.txt       # 比较两个不在仓库里的文件
```

## 生成与应用补丁

```bash
git diff > my.patch                   # 保存为补丁
git apply my.patch                    # 应用补丁
```

提交形式的补丁（含作者、说明）见 [Git Patch](/0226_Tools_Git_Patch)。

## 常见问题

- 提示 `\ No newline at end of file`：见 [No newline at end of file](/0120_Tools_Git_NoNewline)。
- Windows 上整份文件都显示改动：多半是换行符 CRLF/LF 不一致，检查 `core.autocrlf`，用 `git diff --ignore-space-at-eol` 辅助确认。
- 文件权限变化也会出现在 diff 中：`git config core.filemode false` 可忽略。

## Reference
- [git-diff 官方文档](https://git-scm.com/docs/git-diff)

