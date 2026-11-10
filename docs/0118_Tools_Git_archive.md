---
Title | Tools Git archive
-- | --
Created @ | `2022-01-05T03:06:00Z`
Updated @| `2026-11-10T06:06:48Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/118)

---
# Git archive

`git archive` 把仓库中**某个提交/分支/tag 的内容**打包成 `zip` 或 `tar`，**不包含 `.git` 目录**，常用于制作发布包。

```bash
git archive --prefix=flann-$VERSION-src/ -o flann-$VERSION-src.zip $VERSION-src
```

- `--prefix`：压缩包内统一的顶层目录，解压后不会散落一地。注意要以 `/` 结尾。
- `-o`：输出文件，格式按扩展名推断（`.zip`、`.tar`、`.tar.gz`/`.tgz`）。
- 最后的 `$VERSION-src` 是要打包的 tag（也可以是分支名或 commit）。

## 常用示例

```bash
git archive -o latest.zip HEAD                          # 打包当前提交
git archive --format=tar.gz -o v1.0.tar.gz v1.0         # 打包某个 tag
git archive --prefix=proj/ -o proj.tar.gz main          # 加顶层目录
git archive -o sub.zip HEAD src/ docs/                  # 只打包指定目录
git archive HEAD | tar -x -C /tmp/export                # 导出到目录（不含 .git）
git archive --remote=<url> HEAD | tar -x                # 从远程导出（需服务端允许）
```

## 控制哪些文件被打包

在 `.gitattributes` 里用 `export-ignore` 排除不需要发布的文件，用 `export-subst` 替换版本信息：

```
tests/        export-ignore
.github/      export-ignore
.gitignore    export-ignore
.gitattributes export-ignore
```

## 注意

- 只打包**已提交**的内容，工作区未提交的改动、未跟踪文件都不会包含。
- **子模块的内容不会被包含**，需要自己处理（如 `git submodule foreach` 分别打包后合并）。
- 若要把版本号写进压缩包：可用 `git describe --tags` 生成 `$VERSION`。

```bash
VERSION=$(git describe --tags --abbrev=0)
git archive --prefix=proj-$VERSION/ -o proj-$VERSION.tar.gz HEAD
```

## Reference
- [git-archive 官方文档](https://git-scm.com/docs/git-archive)
- [flann make release with `git archive`](https://github.com/junxnone/flann/blob/master/bin/make_release.sh#L6)

