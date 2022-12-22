---
Title | Pandas UseCase sampling
-- | --
Created @ | `2022-12-22T09:33:43Z`
Last Modify @| `2022-12-22T09:33:43Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/203)

---

# 抽样

## 打乱样本

```
df.sample(n=None, frac=None, replace=False, weights=None, random_state=None, axis=None)
```
> Returns a random sample of items from an axis of object.
frac 为选取的比例 0 ~ 1

```
df = df.sample(frac = 1) 
```

## 按概率抽样

```
s = pd.Series([0,1,2,3,4,5])
example_weights = [0, 0, 0.2, 0.2, 0.2, 0.4]
s.sample(n=3, weights=example_weights)

5    5
4    4
3    3
```
