-----

| Title     | Pandas UseCase string                                |
| --------- | ---------------------------------------------------- |
| Created @ | `2022-12-22T09:34:31Z`                               |
| Updated @ | `2026-11-16T09:40:16Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/204) |

-----

# 字符串处理

通过 `.str` 访问器对字符串列做向量化处理

| API                                  | Description                                    |
| ------------------------------------ | ---------------------------------------------- |
| `df2.id.str.lower()`                 | 'id' 列中字符转换小写                                  |
| `df2.id.str.upper()`                 | 转换大写                                           |
| `df.id.str.strip()`                  | 去除首尾空白                                         |
| `df.id.str.len()`                    | 字符串长度                                          |
| `df.id.str.replace('a', 'b')`        | 替换                                             |
| `df.id.str.contains('abc')`          | 是否包含，见 [条件操作](/0201_Pandas_UseCase_condition)  |
| `df.id.str.startswith('a')`          | 是否以某前缀开头                                       |
| `df.name.str.split('_', n=1).str[0]` | 拆分并取第一部分，见 [列操作](/0198_Pandas_UseCase_columns) |
| `df.T`                               | 行列转置（非字符串操作）                                   |

## Reference

  - [Working with text
    data](https://pandas.pydata.org/docs/user_guide/text.html)
