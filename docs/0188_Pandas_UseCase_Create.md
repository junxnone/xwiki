---
Title | Pandas UseCase Create
-- | --
Created @ | `2019-08-15T11:23:03Z`
Last Modify @| `2022-12-28T04:59:46Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/188)

---
# 读写/Format 转换

- CSV
- H5
- xlsx
- Numpy
- Markdown

## 读写文件

### csv

```
pd.read_csv('foo.csv')
df.to_csv('foo.csv')
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


## 格式转换

### 转 numpy

```
df.to_numpy()
```

### 转 Markdown

```
df.to_markdown()
```



