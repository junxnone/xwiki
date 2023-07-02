-----

| Title     | Tools Git Patch                                      |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-03-21T07:40:57Z`                               |
| Updated @ | `2023-03-21T07:42:21Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/226) |

-----

# Git Patch 生成与使用

## 生成 patch

### format-patch

  - 相比 `diff` 会保留 `commit` 记录消息

#### 生成最后一个 commit 的 patch

    git format-patch -1

#### 生成最后 `N` 个 patch

``` 
git format-patch -N 
```

#### 生成 commitID 之后的 patch

    git format-patch commitID

#### 生成 两个 `commit` 之间的 `patch`

    git format-patch commitID1 commitID2

### git diff

  - 可以用来比较很久之前的 commit, 生成一个 patch

<!-- end list -->

    git diff > your_patch_name.patch

## 使用 `patch`

### apply

    git apply  your_patch_name.patch

### am

    git am   your_patch_name.patch
