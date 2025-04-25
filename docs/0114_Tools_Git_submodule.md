---
Title | Tools Git submodule
-- | --
Created @ | `2018-12-10T05:55:39Z`
Updated @| `2025-04-25T03:37:22Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/114)

---
# Git Submodule
 
- git 包含嵌套的概念, 仓库中可以包含另一个仓库


## 新建包含子仓库的仓库

```
cd workdir
git init
git submodule add https://xxxx.git subdir
```

## update 所有仓库

```
git submodule update --init --recursive
```

## Git 更改submodule 的地址


分别更改如下文件中的子模块地址
- .submodule
- .git/config



> 在运行 git submodule update --init --recursive 时，.submodule 中的 submodule 会更新到.git/config 中，所以运行此命令之前可以只更新.submodule 文件


## 移除子模块
### 停止跟踪子模块
- 从 Git 的跟踪中移除，但不删除本地文件
```
git submodule deinit -f <子模块路径>
```

### 从项目中移除子模块的记录
- 从.gitmodules文件和项目的暂存区中移除子模块的相关信息

```
git rm -f <子模块路径>
```

### 提交更改

```
git commit -m "Remove submodule"
```
