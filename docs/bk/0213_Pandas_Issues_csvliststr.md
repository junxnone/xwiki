-----

| Title     | Pandas Issues csvliststr                             |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-02-28T09:21:21Z`                               |
| Updated @ | `2026-11-16T09:40:20Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/213) |

-----

# 存储为 csv 再读入后, 单元格值 `list` 类型会变成 `str` 类型

## 现象

``` python
df = pd.DataFrame({'a': [[1, 2], [3]]})
df.to_csv('t.csv', index=False)
pd.read_csv('t.csv').a[0]   # '[1, 2]'  -> str
```

  - csv 是纯文本格式，`list` 被写成字符串 `"[1, 2]"`，读回来不会自动还原

## 方法一：使用 pickle 格式存储读写

    # Write
    data_df.to_pickle('your_filename.pickle')
    
    # Read
    data_df = pd.read_pickle('your_filename.pickle')

> pickle 只应读取可信来源的文件

## 方法二：读入 csv 后转换

``` python
import ast
df = pd.read_csv('t.csv', converters={'a': ast.literal_eval})
```

## 方法三：json 格式

``` python
df.to_json('t.json')
df = pd.read_json('t.json')
```
