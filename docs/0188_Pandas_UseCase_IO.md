---
Title | Pandas UseCase IO
-- | --
Created @ | `2019-08-15T11:23:03Z`
Updated @| `2023-06-13T02:20:05Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/188)

---
# Format Output/读写文件


- Numpy
- Markdown
- CSV
- H5
- xlsx


## 格式转换

### 转 numpy

```
df.to_numpy()
```

### 转 Markdown

```
df.to_markdown()
```


## 读写文件

### csv

```
pd.read_csv('foo.csv')
df.to_csv('foo.csv')
```

- 保存为无 `index` 的 `csv`

```
df.to_csv('csv_name.csv', index=None)
```

### h5

```
pd.read_hdf('foo.h5', 'df')
df.to_hdf('foo.h5', 'df')
```

### xlsx

```
pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
df.to_excel('foo.xlsx', sheet_name='Sheet1')
```


