---
Title | Pandas UseCase SpecialValue
-- | --
Created @ | `2019-08-15T11:05:16Z`
Updated @| `2026-11-16T09:39:57Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/187)

---
# 特殊值

## 重复值

```
df.duplicated()  -> 查看重复的
df[df['id'].duplicated()]  ->查看 'id' 重复的 keep = False, 'first','last'
df.drop_duplicates(keep='last') -> 删除重复，只留最后一个值
df.drop_duplicates(subset=['id']) -> 仅根据 'id' 列判断重复
```
> `keep` 取值：`'first'`（默认，保留第一个）、`'last'`（保留最后一个）、`False`（全部标记/删除）

## na/NA

```
np.nan -> nan 缺失值
df.dropna(how='any') -> 删除任何带有缺失值的行
df.dropna(how='all') -> 删除全为缺失值的行
df.dropna(subset=['id']) -> 仅看 'id' 列
df.fillna(value=5) ->填充缺失值
df.fillna(df.mean(numeric_only=True)) -> 用各列均值填充
df.ffill() / df.bfill() -> 前向 / 后向填充
pd.isna(df1) -> 获取值为nan的掩码
df.isna().sum() -> 每列缺失值个数
```

## 无穷值

```
df.replace([np.inf, -np.inf], np.nan)
```

## Reference
- [Working with missing data](https://pandas.pydata.org/docs/user_guide/missing_data.html)
- [duplicated](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.duplicated.html)

