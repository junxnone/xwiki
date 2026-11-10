-----

| Title     | Tools Git tag                                        |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-10-25T07:32:34Z`                               |
| Updated @ | `2026-11-10T06:06:43Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/116) |

-----

# Git tag

tag（标签）给某个提交起一个固定的名字，通常用来标记发布版本（如 `v1.4.0`）。与分支不同，tag 不会随新提交移动。

## 类型

| 类型                 | 说明                           | 创建                         |
| ------------------ | ---------------------------- | -------------------------- |
| 轻量标签 (lightweight) | 只是指向提交的一个引用                  | `git tag v1.0`             |
| 附注标签 (annotated)   | 一个独立的 Git 对象，含打标签者、日期、说明，可签名 | `git tag -a v1.0 -m "msg"` |

发布版本建议用附注标签。

## UseCase

| Usecase          | cmd                                                                 |
| ---------------- | ------------------------------------------------------------------- |
| 查看所有tag          | `git tag`                                                           |
| 查看匹配某些类型的标签      | `git tag -l 'v1.4.2.*'`                                             |
| 创建一个含附注类型的标签     | `git tag -a v1.4 -m 'my version 1.4'`                               |
| 给某一个commit 打 tag | `git tag -a v1.2 9fceb02`                                           |
| 查看 tag 信息        | `git show v1.4`                                                     |
| push 特定tag       | `git push origin v1.5`                                              |
| 一次push所有本地新增的标签  | `git push origin --tags`                                            |
| 删除本地tag          | `git tag -d v1.1`                                                   |
| 删除远程tag          | `git push origin --delete v1.1`                                     |
| 切换到某个 tag        | `git switch --detach v1.4`（处于游离 HEAD，改动前先 `git switch -c <branch>`） |
| 基于 tag 新建分支      | `git switch -c fix-1.4 v1.4`                                        |
| 列出 tag 对应的提交     | `git rev-list -n 1 v1.4`                                            |
| 按版本号排序列出         | `git tag --sort=-v:refname`                                         |
| 查看最近的 tag        | `git describe --tags --abbrev=0`                                    |
| 查看包含某提交的 tag     | `git tag --contains <commit>`                                       |

> 默认情况下，git push 并不会把标签传送到远端服务器上，只有通过显式命令才能分享标签到远端仓库。

## 移动 / 重命名 tag

tag 本身不应该移动，确需修改（尚未广泛使用时）：

``` bash
git tag -f v1.4 <new-commit>             # 强制改指向
git push origin v1.4 --force             # 覆盖远程（别人已拉取的话会不一致，慎用）

# 重命名
git tag new old
git tag -d old
git push origin new :refs/tags/old
```

## 签名 Tag

  - 如果你有自己的私钥，还可以用 GPG 来签署标签，只需要把之前的 `-a` 改为 `-s`（signed）即可：

<!-- end list -->

``` bash
git tag -s v1.5 -m 'my signed 1.5 tag'
```

### 验证 Tag

  - 此命令会调用 GPG 来验证签名，所以你需要有签署者的公钥，存放在 keyring 中，才能验证

<!-- end list -->

``` bash
git tag -v v1.4.2.1
```

## 删除远程 tag

``` bash
git tag -d v1.1                          # 先删除本地
git push origin --delete v1.1            # 推荐写法（需要 git 1.7+）
git push origin :refs/tags/v1.1          # 旧写法，效果相同
```

  - 本地 tag 和远程 tag 相互独立，要分别删除。
  - 若其他人已经拉取了该 tag，他们本地仍然存在，需要自行 `git tag -d`；`git fetch --prune
    --prune-tags` 可同步清理（会删除本地有而远程没有的 tag）。

## 与发布相关

  - Github 上基于 tag 创建 Release，会自动提供源码压缩包；本地打包见 [Git
    archive](/0118_Tools_Git_archive)。
  - 版本号推荐使用 [语义化版本](https://semver.org/lang/zh-CN/)：`主版本.次版本.修订号`。

## Reference

  - [git-tag 官方文档](https://git-scm.com/docs/git-tag)
  - [Pro Git: 打标签](https://git-scm.com/book/zh/v2/Git-基础-打标签)
