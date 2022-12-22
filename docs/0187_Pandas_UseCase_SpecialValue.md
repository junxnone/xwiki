---
Title | Pandas UseCase SpecialValue
-- | --
Created @ | `2019-08-15T11:05:16Z`
Last Modify @| `2022-12-22T09:36:40Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/187)

---
# 特殊值

## 重复值

```
df.duplicated()  -> 查看重复的
df[df['id'].duplicated()  ->查看 'id' 重复的 keep = False, 'first‘,’last’
df.drop_duplicates(keep='last') -> 删除重复，只留最后一个值
```

## na/NA


```
np.nan -> nan 缺失值
df.dropna(how='any') -> 删除任何带有缺失值的行
df.fillna(value=5) ->填充缺失值
pd.isna(df1) -> 获取值为nan的掩码
```

