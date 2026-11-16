-----

| Title     | Pandas UseCase Merge                                 |
| --------- | ---------------------------------------------------- |
| Created @ | `2022-12-22T09:35:34Z`                               |
| Updated @ | `2026-11-16T09:40:18Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/205) |

-----

# 合并

## concat 拼接

    pe = [df1,df2, df3]
    df4 = pd.concat(pe,keys=['0417','0725','0802'], sort=False)

  - `keys` 为每个 df 增加一层 index 标识来源
  - `axis=0`（默认）纵向拼接；`axis=1` 横向拼接
  - `ignore_index=True` 重新生成 index

## merge 按列关联（类似 SQL join）

    pd.merge(df1, df2, on='id', how='inner')
    pd.merge(df1, df2, left_on='id1', right_on='id2', how='left')

| how          | 说明          |
| ------------ | ----------- |
| inner        | 交集（默认）      |
| left / right | 保留左 / 右表所有行 |
| outer        | 并集          |

## join 按 index 关联

    df1.join(df2, how='left')

## Reference

  - [Merge, join,
    concatenate](https://pandas.pydata.org/docs/user_guide/merging.html)
