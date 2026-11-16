---
Title | Pandas UseCase row
-- | --
Created @ | `2022-12-22T09:28:35Z`
Updated @| `2026-11-16T09:40:07Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/199)

---
# 行操作


## 选择行

```
df[0:3]  -> 切片
df.loc[0:10,['id', 'coef']] -> 选择两列的切片
```

操作 | 语法 | 结果
-- | -- | --
按标签选择行 | df.loc[label] | Series
按整数位置选择行 | df.iloc[loc] | Series
对行切片 | df[5:10] | DataFrame
通过布尔向量选择行 | df[bool_vec] | DataFrame

> `loc` 的切片包含两端，`iloc` 和 `df[a:b]` 的切片不包含右端点

## 添加新行

```
df.loc[len(df)] = [ 'xxx', 'yyy', 'xxz']
df.loc[len(df), 'name'] = 'xxx'
```

- 用 `concat` 追加多行（`DataFrame.append` 在 pandas 2.0 已移除）

```
df = pd.concat([df, pd.DataFrame([{'name': 'xxx'}])], ignore_index=True)
```

## 删除行

```
df.drop([0,1],inplace=True) 删除 行
df = df[df.coef > 1]  -> 保留满足条件的行（等价于删除不满足的）
```

## 遍历行

```
for index, row in df.iterrows():
  print(row)
```

- `itertuples` 比 `iterrows` 更快，返回 namedtuple

```
for row in df.itertuples():
  print(row.Index, row.id)
```
> 能向量化的操作尽量不要遍历行

## Reference
- [Indexing and selecting data](https://pandas.pydata.org/docs/user_guide/indexing.html)

