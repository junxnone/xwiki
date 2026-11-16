---
Title | Pandas UseCase condition
-- | --
Created @ | `2022-12-22T09:31:37Z`
Updated @| `2026-11-16T09:40:11Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/201)

---

# 条件操作


## 按条件选择

```
df[df.coef> 1]  -> 'coef' 值大于1 的行
df[df.coef.isin([2])] 'coef 是 2的行
df[df.coef.isin([1, 2, 3])] 'coef 是 1, 2, 3的行
df[~df.coef.isin([1, 2, 3])] 'coef 不是 1, 2, 3的行
df.query('coef > 1 and id == "a"')  -> 用表达式筛选
```

##  包含字符串的值

```
df.name.str.contains('abc')
df.name.str.contains('abc|abd')
df[df.name.str.contains('abc', na=False)]  -> 忽略 NaN
```

##  某个取值范围 (min, max)

```
df[(df.area > min) & (df.area < max)]
df[df.area.between(min, max)]  -> 默认包含两端
```

##  多重条件选择

- | for or
- & for and
- ~ for not

```
df[(df.coef> 1) & (df.coef<3)]  -> 'coef' 值大于1 小于3 的行
```
> 每个条件必须加括号，因为 `&` `|` 优先级高于比较运算符

## 条件赋值

```
df.loc[df.coef > 1, 'flag'] = True
df['level'] = np.where(df.coef > 1, 'high', 'low')
```

