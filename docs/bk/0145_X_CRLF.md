-----

| Title     | X CRLF                                               |
| --------- | ---------------------------------------------------- |
| Created @ | `2020-04-23T09:44:34Z`                               |
| Updated @ | `2023-11-02T03:42:14Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/145) |

-----

# 文件换行 Windows Linux CRLF LF

  - CR - Carriage-Return - 回车 - `ASCII 13` - `\r`
  - LF - Line-Feed - 换行 - `ASCII 10` - `\n`

| OS          | 换行符  |
| ----------- | ---- |
| Windows     | CRLF |
| Linux/Unix  | LF   |
| \< Mac OS 9 | CR   |
| \> Mac OS X | LF   |

## Tools

### 检查文件格式

#### file

  - 检查是不是 `CRLF` format

<!-- end list -->

    file your_file
    your_file: Bourne-Again shell script, ASCII text executable, with CRLF line terminators

### cat

  - `$` 为 Linux
  - `^M$` 为 windows

<!-- end list -->

    cat -A [your_file]

    111$
    222$
    333$
    444$
    555$
    666$
    777$
    111^M$
    222^M$
    333^M$
    444^M$
    555^M$
    666^M$
    777^M$

### vim

    vim -b your_file

> `^M` 结尾 的为 `CRLF` `$` 默认不显示，设置 `:set list` 后显示

### 转换格式

#### dos2unix

  - `CRLF --> LF`

<!-- end list -->

    dos2unix  your_file

#### tofrodos

    fromdos your_file
    todos your_file

#### vim

    vim your_file

    :set ff=unix

## History

| 打字机按键 | 行为          |
| ----- | ----------- |
| LF    | 换行，但是列位置不变  |
| CR    | 不换行，回到纸张最左侧 |

## Reference

  - [tofrodos -
    ubuntu](http://manpages.ubuntu.com/manpages/focal/man1/fromdos.1.html)
