-----

| Title     | Tools Git NoNewline                                  |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-07-05T03:05:04Z`                               |
| Updated @ | `2026-11-10T06:06:53Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/120) |

-----

# No newline at end of file

  - **Issue** - `git diff \ No newline at end of file`
  - when use `git diff somefile`, it says `  \ No newline at end of
    file ` in the end

## 原因

  - POSIX 约定文本文件的**每一行都以换行符 `\n` 结尾**，包括最后一行。
  - 文件最后一行没有换行符时，`git diff` 会在该行后面提示 `\ No newline at end of file`。
  - 只是在文件末尾加上或去掉换行，也会被 git 认为那一行被修改了：

<!-- end list -->

``` diff
-last line
\ No newline at end of file
+last line
```

## 影响

  - 让 diff 变得嘈杂，合并时也容易产生无谓的冲突。
  - 某些工具（如 `cat` 连接多个文件、`wc -l`、部分编译器/脚本解析）处理最后一行时行为异常。
  - 与 CRLF 无关，但 Windows 下经常和 CRLF 问题一起出现，需要区分。

## Solution

| Target                             | command                                                                              |
| ---------------------------------- | ------------------------------------------------------------------------------------ |
| 查找 CRLF 结尾的文件                      | `file * \| grep CRLF`                                                                |
| 把文件从 `dos format` 转到 `unix format` | `dos2unix  your_file`                                                                |
| 把所有文件转换格式                          | `file *\|grep CRLF\|awk -F ":" '{print $1}'\|xargs -i dos2unix {}`                   |
| 添加 `\n`                            | `sed -i -e '$a\' your_file`                                                          |
| 检查文件末尾是否有换行                        | `tail -c1 your_file \| xxd`（结果为 `0a` 表示有）                                            |
| 找出所有末尾缺换行的文本文件                     | `git ls-files -z \| xargs -0 -I{} sh -c 'tail -c1 "{}" \| read -r _ \|\| echo "{}"'` |

  - `sed -i -e '$a\'` 的含义：在最后一行（`$`）之后追加（`a`）空内容；sed
    在输出时会为最后一行补上缺失的换行，如果已经有换行则保持不变，所以可以安全地重复执行。

## 预防

  - 编辑器设置：保存时自动在文件末尾插入换行（VS Code：`"files.insertFinalNewline": true`）。
  - 用 [EditorConfig](https://editorconfig.org/) 统一团队设置：

<!-- end list -->

``` ini
# .editorconfig
root = true

[*]
end_of_line = lf
insert_final_newline = true
trim_trailing_whitespace = true
```

  - 用 pre-commit 在提交前自动修复：`end-of-file-fixer` 和 `mixed-line-ending`
    hook，见 [Git precommit](/0117_Tools_Git_precommit)。
  - 用 `.gitattributes` 规范换行符：

<!-- end list -->

    * text=auto
    *.sh text eol=lf
    *.bat text eol=crlf

## Reference

  - [No Newline at End of
    File](https://thoughtbot.com/blog/no-newline-at-end-of-file)
  - [How to add a newline to the end of a
    file?](https://unix.stackexchange.com/questions/31947/how-to-add-a-newline-to-the-end-of-a-file)
  - [pre-commit-hooks](https://github.com/pre-commit/pre-commit-hooks)
