-----

| Title     | Tools Git Patch                                      |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-03-21T07:40:57Z`                               |
| Updated @ | `2025-03-15T09:49:22Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/226) |

-----

# Git Patch

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

## 更改前一个 patch

    # 更改内容 并使用 git add 添加
    git commit --amend

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
  - `diff --git a/3rdparty/libjpeg-turbo/CMakeLists.txt
    b/3rdparty/libjpeg-turbo/CMakeLists.txt` 修改了哪个文件
  - `@@ -16,7 +16,7 @@` 修改标志，显示从 第16行截取显示7行，`-/+` 代表patch 前/后
    不同的行数或截取显示行数
