-----

| Title         | Programing regex                                     |
| ------------- | ---------------------------------------------------- |
| Created @     | `2020-05-14T08:15:09Z`                               |
| Last Modify @ | `2022-12-26T03:12:56Z`                               |
| Labels        | \`\`                                                 |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/206) |

-----

# Regex 正则表达式

## Reference

  - [Github - learn-regex](https://github.com/ziishaned/learn-regex)
  - [regex101](https://regex101.com/)

## Brief

  - Regular expression - regex/regexp
  - 元字符 - 特殊含义字符
  - 简写字符集

## 基本格式

![image](media/816b89f9392b217659af73eafce1a488fbb094cc.png)

|  元字符   | 描述                                                            |
| :----: | ------------------------------------------------------------- |
|   .    | 句号匹配任意单个字符除了换行符。                                              |
| \[ \]  | 字符种类。匹配方括号内的任意字符。                                             |
| \[^ \] | 否定的字符种类。匹配除了方括号里的任意字符                                         |
|   \*   | 匹配\>=0个重复的在\*号之前的字符。                                          |
|   \+   | 匹配\>=1个重复的+号前的字符。                                             |
|   ?    | 标记?之前的字符为可选.                                                  |
| {n,m}  | 匹配num个大括号之前的字符或字符集 (n \<= num \<= m).                         |
| (xyz)  | 字符集，匹配与 xyz 完全相等的字符串.                                         |
|   |    | 或运算符，匹配符号前或后的字符.                                              |
|   \\   | 转义字符,用于匹配一些保留的字符 <code>\[ \] ( ) { } . \* + ? ^ $ \\ |</code> |
|   ^    | 从开始行开始匹配.                                                     |
|   $    | 从末端开始匹配.                                                      |

| 简写  | 描述                                 |
| :-: | ---------------------------------- |
|  .  | 除换行符外的所有字符                         |
| \\w | 匹配所有字母数字，等同于 `[a-zA-Z0-9_]`        |
| \\W | 匹配所有非字母数字，即符号，等同于： `[^\w]`         |
| \\d | 匹配数字： `[0-9]`                      |
| \\D | 匹配非数字： `[^\d]`                     |
| \\s | 匹配所有空格字符，等同于： `[\t\n\f\r\p{Z}]`    |
| \\S | 匹配所有非空格字符： `[^\s]`                 |
| \\f | 匹配一个换页符                            |
| \\n | 匹配一个换行符                            |
| \\r | 匹配一个回车符                            |
| \\t | 匹配一个制表符                            |
| \\v | 匹配一个垂直制表符                          |
| \\p | 匹配 CR/LF（等同于 `\r\n`），用来匹配 DOS 行终止符 |