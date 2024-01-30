---
Title | Tools Github actions
-- | --
Created @ | `2019-11-16T06:07:58Z`
Updated @| `2024-01-30T14:58:59Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/122)

---
# Github Actions
- CI/CD
- 持续集成由很多操作组成，比如抓取代码、运行测试、登录远程服务器，发布到第三方服务等等。GitHub 把这些操作就称为 actions。


![image](https://github.com/junxnone/xwiki/assets/2216970/8d4e5613-9692-4d7b-99bb-d7ce16c42e13)

## ReUse Workflow

- 创建重用 `workflow` 时需指定可 `workflow_call`

```
on:
  workflow_call:
```

- 使用方法

```
  call-workflow-1-in-local-repo:
    uses: octo-org/this-repo/.github/workflows/workflow-1.yml@commit-id
  call-workflow-2-in-local-repo:
    uses: ./.github/workflows/workflow-2.yml
  call-workflow-in-another-repo:
    uses: octo-org/another-repo/.github/workflows/workflow.yml@v1
```

## Issues
###   jobs 未使用最新的 repo commit
- 多个 jobs workflow,  后面的 jobs 未使用最新的 repo commit
- 在 checkout action 中添加 参数 `ref: ${{ github.ref }}`

```
- uses: actions/checkout@v3
  with:
    ref: ${{ github.ref }}
```

## Reference
- [GitHub Actions 入门教程](http://www.ruanyifeng.com/blog/2019/09/getting-started-with-github-actions.html)
- [Github marketplace - action](https://github.com/marketplace?type=actions)
- [bandit check](https://github.com/jpetrucciani/bandit-check)
- [pylint check](https://github.com/marketplace/actions/github-action-for-pylint)
- [重新使用工作流](https://docs.github.com/zh/actions/using-workflows/reusing-workflows)


