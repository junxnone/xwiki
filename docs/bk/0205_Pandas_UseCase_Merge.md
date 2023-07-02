-----

| Title         | Pandas UseCase Merge                                 |
| ------------- | ---------------------------------------------------- |
| Created @     | `2022-12-22T09:35:34Z`                               |
| Last Modify @ | `2022-12-22T09:35:34Z`                               |
| Labels        | \`\`                                                 |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/205) |

-----

# 合并

    pe = [df1,df2, df3]
    df4 = pd.concat(pe,keys=['0417','0725','0802'], sort=False)
