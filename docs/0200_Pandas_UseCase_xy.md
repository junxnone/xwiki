---
Title | Pandas UseCase xy
-- | --
Created @ | `2022-12-22T09:29:52Z`
Last Modify @| `2022-12-22T09:29:52Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/200)

---

# 单元格操作

## 位置 + columns

```
df.loc[10,'coef']  -> 10行 ’coef‘ 列
```

##  按位置选择

```
df.iloc[2,1] -> 按位置选择
df.iloc[2] -> 按位置选择
```

##  写指定位置

```
df.at[id[0], 'coef'] = 0  -> 通过标签赋值
df.iat[0, 1] = 0 ->通过位置赋值
df.id[df.name == 'xxx'] = '123'
```
