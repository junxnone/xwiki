---
Title | Pandas UseCase xy
-- | --
Created @ | `2022-12-22T09:29:52Z`
Updated @| `2026-11-16T09:40:09Z`
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
df.loc[df.name == 'xxx', 'id'] = '123'  -> 按条件赋值（推荐）
```
> 不推荐链式赋值 `df.id[df.name == 'xxx'] = '123'`，会触发 [SettingWithCopyWarning](/0185_Pandas_Issues_SettingWithCopyWarning)

## 方法对比

方法 | 索引方式 | 说明
-- | -- | --
loc | 标签 | 切片包含两端
iloc | 整数位置 | 切片不含右端
at | 标签 | 仅单个值，更快
iat | 整数位置 | 仅单个值，更快

