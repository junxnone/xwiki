---
Title | Pandas UseCase ShowSummaryInfo
-- | --
Created @ | `2022-12-22T09:23:55Z`
Last Modify @| `2022-12-22T09:23:55Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/197)

---
# 简单查看数据

## 查看顶部和尾部的数据

```
df.head()
df.head(10)
df.tail(3)
```

## 查看统计信息

```
df.index  -> 显示索引
df.columns  -> 获取列名
df.dtypes  -> 列具有不同的数据类型
df.describe() -> 显示数据的快速统计摘要
df.coef.value_counts() -> 查看 ’coef' 列的直方图化数
df.coef.value_counts(1) -> 查看 ’coef' 列的直方图化数，归一化为1，即比例
df.mean()  -> 进行描述性统计
df.mean(1) -> 在axis 1 上进行描述性统计
```
> 输入 `df.` + <kbd>TAB</kbd> 可以自动补全所有的列名以及公共属性。


