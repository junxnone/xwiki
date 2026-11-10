-----

| Title     | Tools Git precommit                                  |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-11-14T02:36:49Z`                               |
| Updated @ | `2026-11-10T06:06:46Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/117) |

-----

# Git pre-commit

pre-commit 是 git 的钩子（hook）之一，在 `git commit` **创建提交之前**运行；脚本以非 0
退出时，提交会被中止。常用于在提交前自检：格式、语法、简单的安全检查等。

  - pre-commit 更倾向于 commit 之前自我审查。
  - push 之后 merge 时还是需要 review。
  - 因为 security 原因，`.git/hooks` 不会随仓库一起被克隆，不会默认作为新 clone 的 repo 的
    hooks，需要每个人自己安装。

**优点**

  - 优化 CI 之前的自检查，更早发现问题
  - formatting check
  - build test

## Git 原生 hook

hook 脚本放在 `.git/hooks/` 下，文件名固定、需要可执行权限：

``` bash
# .git/hooks/pre-commit
#!/bin/sh
# 例：禁止提交包含 TODO_REMOVE 的内容
if git diff --cached | grep -q "TODO_REMOVE"; then
    echo "found TODO_REMOVE, commit aborted"
    exit 1
fi
```

``` bash
chmod +x .git/hooks/pre-commit
git commit --no-verify        # 临时跳过 pre-commit / commit-msg hooks（不要滥用）
```

常见的客户端 hook：

| hook                 | 触发时机                 |
| -------------------- | -------------------- |
| `pre-commit`         | 输入提交说明之前             |
| `prepare-commit-msg` | 生成默认说明之后，编辑器打开之前     |
| `commit-msg`         | 提交说明写完之后，可用于校验格式     |
| `post-commit`        | 提交完成之后               |
| `pre-push`           | `git push` 之前，常用来跑测试 |
| `pre-rebase`         | rebase 之前            |

共享 hook：把脚本放进仓库（如 `.githooks/`），再执行：

``` bash
git config core.hooksPath .githooks
```

## pre-commit 框架（Python）

[pre-commit](https://pre-commit.com/) 是一个管理多语言 hook 的框架，在仓库根目录用
`.pre-commit-config.yaml` 声明要用哪些检查：

``` yaml
repos:
  - repo: https://github.com/pre-commit/pre-commit-hooks
    rev: v4.6.0
    hooks:
      - id: trailing-whitespace
      - id: end-of-file-fixer
      - id: check-yaml
      - id: check-added-large-files
  - repo: https://github.com/astral-sh/ruff-pre-commit
    rev: v0.5.0
    hooks:
      - id: ruff
        args: [--fix]
      - id: ruff-format
```

> `rev` 只是示例，实际使用时用 `pre-commit autoupdate` 更新到最新版本。

``` bash
pip install pre-commit           # 或 pipx install pre-commit / uv tool install pre-commit
pre-commit install               # 在 .git/hooks 里安装钩子（每个克隆执行一次）
pre-commit run --all-files       # 对所有文件手动跑一遍
pre-commit autoupdate            # 更新 hook 版本
pre-commit run <hook-id> -a      # 只跑某个 hook
```

  - 提交时只检查**暂存的文件**；若 hook 自动修改了文件（如格式化），提交会失败，需要重新 `git add` 后再提交。
  - 在 CI 中执行 `pre-commit run --all-files`，保证没安装 hook 的人也被检查。
  - 其他生态：JS 项目常用 `husky` + `lint-staged`。

## 相关

  - [pipx](/0330_Programing_Python_Tools_pipx)：`pipx install pre-commit`

## Reference

  - [pre-commit 官网](https://pre-commit.com/)
  - [Github - pre-commit](https://github.com/pre-commit)
  - [Git 官方文档: githooks](https://git-scm.com/docs/githooks)
  - [git
    commit前检测husky与pre-commit](https://www.jianshu.com/p/f0d31f92bfab)
  - [Pre-commit and post-deploy code reviews are
    dead](https://about.gitlab.com/blog/2019/01/31/pre-commit-post-deploy-is-dead/)
  - [Pre-commit is
    awesome](https://blog.jerrycodes.com/pre-commit-is-awesome/)
  - [Custom server-side Git
    hooks](https://github.com/gitlabhq/gitlabhq/blob/master/doc/administration/custom_hooks.md)
