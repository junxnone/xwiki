-----

| Title     | Tools Git Patch                                      |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-03-21T07:40:57Z`                               |
| Updated @ | `2026-11-10T06:06:56Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/226) |

-----

# Git Patch

patch（补丁）是把一组代码改动保存成文本文件，方便通过邮件、IM
或在没有共同远端的仓库之间传递改动，也常用于给开源项目提交修改、移植某个修复到另一个分支。

## 两种补丁

| `git diff` | `git format-patch` -- | -- | -- 内容 | 只有 diff | 每个 commit
一个文件，含作者、日期、提交说明 应用后保留提交信息 | 否（需自己再 commit） | 是（`git am`） 适合 |
未提交的改动、临时分享 | 已提交的改动、跨仓库传递提交

## 生成 patch

### format-patch

  - 相比 `diff` 会保留 `commit` 记录消息，每个 commit 生成一个 `0001-xxx.patch` 文件

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

> 注意 `git format-patch commitID1 commitID2` 的范围是 `commitID1` **之后**到
> `commitID2`（不含 `commitID1`）。

#### 常用选项

``` bash
git format-patch -1 -o out/           # 输出到指定目录
git format-patch -1 --stdout > x.patch    # 输出到标准输出（多个 commit 合并成一个文件）
git format-patch main                 # 当前分支相对 main 多出来的所有提交
git format-patch -1 <commit> -- path  # 只包含某个路径的改动
git format-patch --root               # 从第一个提交开始
```

### git diff

  - 可以用来比较很久之前的 commit, 生成一个 patch

<!-- end list -->

    git diff > your_patch_name.patch
    git diff --staged > staged.patch         # 只导出暂存区
    git diff commit1 commit2 > range.patch   # 两个 commit 之间
    git diff --binary > with_bin.patch       # 包含二进制文件的改动

## 使用 `patch`

### apply

  - 只应用**文件改动**，不创建提交；既可以用于 `git diff` 也可以用于 `format-patch` 生成的补丁

<!-- end list -->

    git apply  your_patch_name.patch

``` bash
git apply --check x.patch             # 只检查能否应用，不修改文件
git apply --stat x.patch              # 查看补丁涉及的文件统计
git apply --3way x.patch              # 不能直接应用时尝试三方合并，冲突会标记在文件中
git apply --reverse x.patch           # 反向应用（撤销补丁）
git apply --ignore-whitespace x.patch # 忽略空白差异
```

### am

  - 应用 `format-patch` 生成的补丁，并**按原作者、原说明创建提交**

<!-- end list -->

    git am   your_patch_name.patch

``` bash
git am *.patch                        # 按顺序应用多个
git am --3way x.patch                 # 允许三方合并
git am --signoff x.patch              # 添加 Signed-off-by
git am --continue                     # 解决冲突并 git add 之后继续
git am --skip                         # 跳过当前补丁
git am --abort                        # 放弃，恢复到应用之前
```

### 补丁应用失败时

  - 提示 `error: patch failed` / `does not apply`：基线代码和生成补丁时不一致。先 `git
    apply --check` 看看冲突位置，或加 `--3way`。
  - 实在不行用 `git apply --reject x.patch`：能应用的部分应用，失败的部分写入 `*.rej` 文件，手动处理。
  - 提示空白错误（`trailing whitespace`）：加 `--whitespace=fix`（修复）或
    `--ignore-whitespace`。
  - Windows 与 Linux 之间换行符不同导致失败：检查文件是否为 CRLF（见 [No newline at end of
    file](/0120_Tools_Git_NoNewline)）。

## 更改前一个 patch

    # 更改内容 并使用 git add 添加
    git commit --amend

  - 已生成的 `.patch` 文件需要在 `git commit --amend` 之后重新 `git format-patch` 生成。

## 其他工具

``` bash
patch -p1 < x.patch                   # 不在 git 仓库里时，用系统的 patch 命令
diff -u old.txt new.txt > x.patch     # 用 diff 生成统一格式的补丁
```

  - `-p1` 表示去掉路径前缀的第一层（去掉 `a/`、`b/`）。

## Patch 描述

``` 
From 2fd011b6ff5b96a1b6bf2c449dfa0d26fce59103 Mon Sep 17 00:00:00 2001
From: Giorgos Karagounis <giorgos.karagounis@oqton.com>
Date: Mon, 18 Mar 2024 16:37:26 +0100
Subject: [PATCH] Fix for jpegturbo Windows build

---
 3rdparty/libjpeg-turbo/CMakeLists.txt | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

diff --git a/3rdparty/libjpeg-turbo/CMakeLists.txt b/3rdparty/libjpeg-turbo/CMakeLists.txt
index ac0aaf63e1..6e508c8860 100644
--- a/3rdparty/libjpeg-turbo/CMakeLists.txt
+++ b/3rdparty/libjpeg-turbo/CMakeLists.txt
@@ -16,7 +16,7 @@ endif()
 message(STATUS "libjpeg-turbo: VERSION = ${VERSION}, BUILD = ${BUILD}")

 math(EXPR BITS "${CMAKE_SIZEOF_VOID_P} * 8")
-string(TOLOWER ${CMAKE_SYSTEM_PROCESSOR} CMAKE_SYSTEM_PROCESSOR_LC)
+string(TOLOWER "${CMAKE_SYSTEM_PROCESSOR}" CMAKE_SYSTEM_PROCESSOR_LC)

 if(CMAKE_SYSTEM_PROCESSOR_LC MATCHES "x86_64" OR
   CMAKE_SYSTEM_PROCESSOR_LC MATCHES "amd64" OR
--
2.34.1

```

  - `From 2fd011b6ff5b96a1b6bf2c449dfa0d26fce59103` commit id
  - `From: Giorgos Karagounis <giorgos.karagounis@oqton.com>` 作者及邮箱
  - `Subject: [PATCH] Fix for jpegturbo Windows build` 描述信息
  - `---` 之后到 `diff` 之前是改动的文件统计
  - `diff --git a/3rdparty/libjpeg-turbo/CMakeLists.txt
    b/3rdparty/libjpeg-turbo/CMakeLists.txt` 修改了哪个文件
  - `@@ -16,7 +16,7 @@` 修改标志（hunk 头），格式为 `@@ -旧起始行,旧行数 +新起始行,新行数
    @@`：这里表示旧文件从第 16 行起的 7 行，对应新文件从第 16 行起的 7 行；`-`
    开头的行是删除的，`+` 开头的行是新增的
  - 最后的 `2.34.1` 是生成补丁的 git 版本

## Reference

  - [git-format-patch 官方文档](https://git-scm.com/docs/git-format-patch)
  - [git-apply 官方文档](https://git-scm.com/docs/git-apply)
  - [git-am 官方文档](https://git-scm.com/docs/git-am)
  - [Git diff](/0277_Tools_Git_diff)
