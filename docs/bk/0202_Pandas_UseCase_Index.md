-----

| Title     | Pandas UseCase Index                                 |
| --------- | ---------------------------------------------------- |
| Created @ | `2022-12-22T09:32:50Z`                               |
| Updated @ | `2026-11-16T09:40:12Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/202) |

-----

# Index 操作

## 重置 index

    dfn = df.reset_index(drop=True) ->重置 index
    df.reset_index()  -> 原 index 变为一列

## index 排序

    df.sort_values(by='B')  -> 按值(列)排序
    df.sort_index(axis=1, ascending=False)  -> 按轴排序

## 设置 index

    df.set_index('defect')
    df.set_index(['a', 'b'])  -> 多级索引

## 重命名列名

``` 
df2 = df.rename(columns={'level_0':'date'}) 
```

    cls_df = cls_df.rename(columns = lambda c:"cls" + str(c))

  - 直接整体赋值：`df.columns = ['a', 'b', 'c']`

## 读取 CSV 文件时设置 `columns`

    df = pd.read_csv(csv_path, header=None, names=['xxx','xxx'])

  - 指定某列作为 index：`pd.read_csv(csv_path, index_col=0)`

## Reference

  - [reset\_index](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.reset_index.html)
  - [set\_index](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.set_index.html)
