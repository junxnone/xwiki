---
Title | Pandas UseCase Index
-- | --
Created @ | `2022-12-22T09:32:50Z`
Last Modify @| `2022-12-22T09:32:50Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/202)

---

# Index 操作

## 重置 index

```
dfn = df.reset_index(drop=True) ->重置 index
```

##  index 排序

```
df.sort_values(by='B')  -> 按值(列)排序
df.sort_index(axis=1, ascending=False)  -> 按轴排序
```

##  设置 index

```
df.set_index('defect')
```

##  重命名列名

```
df2 = df.rename(columns={'level_0':'date'}) 
```
```
cls_df = cls_df.rename(columns = lambda c:"cls" + str(c))
```

##  读取 CSV 文件时设置 `columns`

```
df = pd.read_csv(csv_path, header=None, names=['xxx','xxx'])
```


