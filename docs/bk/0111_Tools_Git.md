-----

| Title     | Tools Git                                            |
| --------- | ---------------------------------------------------- |
| Created @ | `2018-12-14T07:40:51Z`                               |
| Updated @ | `2023-05-19T15:33:07Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/111) |

-----

# Git

  - 代码版本管理工具，源于 Linux 需求

## 简单的开发流程

``` mermaid
gitGraph:
    commit
    commit
    commit
    commit
    commit tag:" V x.x1"
    branch dev
    checkout dev
    commit id:"-fix bug"
    checkout main
    commit
    commit
    merge dev
    commit
    commit tag:" V x.x2"
```

## Issues

  - [Git 移除 stage 错误添加的文件](/Git_remove_file_from_stage)
  - [No newline at end of file](/git_diff_no_newline_at_end_of_file)

## TODO

  - 简单使用
      - commit
      - push
      - pull
      - tag
      - remote url
      - revert
      - stage
  - 配置选项
      - name/email/编辑器
      - ssh key
      - proxy
  - 子模块
  - 内部原理

## gitlab 手动迁移到 github

  - 默认添加 remote --\> push 只会 迁移 default branch

### 迁移所有分支

  - 添加 remote

<!-- end list -->

    git remote add github_remote xxxxxx

  - checkout 所有分支

<!-- end list -->

``` 
 git branch -a |grep remote | grep -v master | awk -F '/' '{print "git checkout "$3}'|bash
```

  - push

<!-- end list -->

    git push github_remote --all

### 迁移所有 tag

    git tag|awk '{print "git push github_remote "$1}'|bash

## Reference

  - [Git内部原理介绍](https://cloud.tencent.com/developer/article/1369947)
  - [git-tips](https://github.com/jaywcjlove/git-tips)
