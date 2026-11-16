-----

| Title     | Pandas UseCase ShowSummaryInfo                       |
| --------- | ---------------------------------------------------- |
| Created @ | `2022-12-22T09:23:55Z`                               |
| Updated @ | `2026-11-16T09:40:03Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/197) |

-----

# 简单查看数据

## 查看顶部和尾部的数据

    df.head()
    df.head(10)
    df.tail(3)

## 查看基本信息

    df.shape  -> (行数, 列数)
    df.info() -> 各列类型、非空数量、内存占用
    df.index  -> 显示索引
    df.columns  -> 获取列名
    df.dtypes  -> 列具有不同的数据类型

## 查看统计信息

    df.describe() -> 显示数据的快速统计摘要
    df.describe(include='all') -> 同时统计非数值列
    df.coef.value_counts() -> 查看 ’coef' 列的直方图化数
    df.coef.value_counts(1) -> 查看 ’coef' 列的直方图化数，归一化为1，即比例
    df.coef.nunique() -> 'coef' 列不同取值个数
    df.mean()  -> 进行描述性统计
    df.mean(1) -> 在axis 1 上进行描述性统计
    df.isna().sum() -> 每列缺失值个数

> 输入 `df.` + <kbd>TAB</kbd> 可以自动补全所有的列名以及公共属性。

## 显示设置

    pd.set_option('display.max_rows', 100)
    pd.set_option('display.max_columns', None)
    pd.set_option('display.width', 200)
