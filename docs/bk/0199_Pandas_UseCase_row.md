-----

| Title     | Pandas UseCase row                                   |
| --------- | ---------------------------------------------------- |
| Created @ | `2022-12-22T09:28:35Z`                               |
| Updated @ | `2023-06-15T16:35:32Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/199) |

-----

# 行操作

## 选择行

    df[0:3]  -> 切片
    df.loc[0:10,['id', 'coef']] -> 选择两列的切片

| 操作        | 语法              | 结果        |
| --------- | --------------- | --------- |
| 按标签选择行    | df.loc\[label\] | Series    |
| 按整数位置选择行  | df.iloc\[loc\]  | Series    |
| 对行切片      | df\[5:10\]      | DataFrame |
| 通过布尔向量选择行 | df\[bool\_vec\] | DataFrame |

## 添加新行

    df.loc[len(df)] = [ 'xxx', 'yyy', 'xxz']
    df.loc[len(df), 'name'] = 'xxx'

## 删除行

    df.drop([0,1],inplace=True) 删除 行

## 遍历行

    for index, row in df.iterrows():
      print(row)
