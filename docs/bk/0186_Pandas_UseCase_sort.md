-----

| Title     | Pandas UseCase sort                                  |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-08-15T01:58:49Z`                               |
| Updated @ | `2026-11-16T09:39:55Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/186) |

-----

# 排序

  - `sort_values` - 按值排序
  - `sort_index` - 按索引（行/列标签）排序

## 参数

    axis：0按照行名排序；1按照列名排序
    ascending：默认True升序排列；False降序排列
    inplace：默认False，否则排序之后的数据直接替换原来的数据框
    kind：排序方法，{‘quicksort’, ‘mergesort’, ‘heapsort’}, default ‘quicksort’
    na_position：缺失值默认排在最后{"first","last"}
    by：按照某一列(行)或几列(行)数据进行排序（仅 sort_values）

> 指定多列（多行）排序时，先按排在前面的列（行）排序，如果内部有相同数据，再对相同数据内部用下一个列（行）排序

## 示例数据

``` python
df = pd.DataFrame({'a': [2, 1, 2, 3], 'b': [4, 3, 1, 2]}, index=[3, 1, 0, 2])
```

## sort\_index

  - 按“行标签”升序排列

<!-- end list -->

``` python
df.sort_index()
```

  - 按“列标签”升序排列

<!-- end list -->

``` python
df.sort_index(axis=1)
```

  - 指定“多列”排序

<!-- end list -->

``` python
df.sort_values(by=['a', 'b'])
```

## sort\_values

  - 按b列升序排序

<!-- end list -->

``` python
df.sort_values(by='b')
```

  - 先按b列降序，再按a列升序排序

<!-- end list -->

``` python
df.sort_values(by=['b', 'a'], ascending=[False, True])
```

  - 按行3升序排列

<!-- end list -->

``` python
df.sort_values(by=3, axis=1)
```

  - 按行3升序，行0降排列

<!-- end list -->

``` python
df.sort_values(by=[3, 0], axis=1, ascending=[True, False])
```

## 其他

  - 排序后重置索引：`df.sort_values('b').reset_index(drop=True)`
  - 取最大/最小的 n 行：`df.nlargest(3, 'b')` / `df.nsmallest(3, 'b')`
  - 自定义排序函数：`df.sort_values('name', key=lambda s: s.str.lower())`（pandas
    \>= 1.1）

## Reference

  - [sort\_values](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_values.html)
  - [sort\_index](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.sort_index.html)
