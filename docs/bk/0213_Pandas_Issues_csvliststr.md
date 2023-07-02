-----

| Title     | Pandas Issues csvliststr                             |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-02-28T09:21:21Z`                               |
| Updated @ | `2023-02-28T09:21:21Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/213) |

-----

# 存储为 csv 再读入后, 单元格值 `list` 类型会变成 `str` 类型

## 可以使用 pickle 格式存储读写

    # Write
    data_df.to_pickle('your_filename.pickle')
    
    # Read
    data_df = pd.read_pickle('your_filename.pickle')
