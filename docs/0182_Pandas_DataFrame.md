---
Title | Pandas DataFrame
-- | --
Created @ | `2019-03-04T05:50:26Z`
Updated @| `2023-07-06T15:10:48Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/182)

---
# DataFrame

DataFrame是Pandas中的一个表格型的数据结构，包含有一组有序的列，每列可以是不同的值类型(数值、字符串、布尔型等)，DataFrame即有行索引也有列索引，可以被看做是由Series组成的字典。

## 创建 DataFrame

### 使用字典创建

- 如果index没有传递，这些列将是字典的键的有序列表

```
d = {'one' : pd.Series([1., 2., 3.], index=['a', 'b', 'c']),
       'two' : pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
df = pd.DataFrame(d)

   one  two
a  1.0  1.0
b  2.0  2.0
c  3.0  3.0
d  NaN  4.0
```

- 包含 `scalar value` 的字典

```
df = pd.DataFrame({"A":1,"B":2,"C":3}, index=[0])
```

 A | B | C
-- | -- | -- 
1 | 2 | 3


> 结果的index是各种系列索引的并集


- 如果传递了 index，则会用于生成索引或列。并且会丢弃所有不匹配传入索引的数据。

```
pd.DataFrame(d, index=['d', 'b', 'a'])

   one  two
d  NaN  4.0
b  2.0  2.0
a  1.0  1.0

pd.DataFrame(d, index=['d', 'b', 'a'], columns=['two', 'three'])

   two three
d  4.0   NaN
b  2.0   NaN
a  1.0   NaN
```

- ndarrays 的字典

```
d = {'one' : [1., 2., 3., 4.],
       'two' : [4., 3., 2., 1.]}
pd.DataFrame(d)

   one  two
0  1.0  4.0
1  2.0  3.0
2  3.0  2.0
3  4.0  1.0

pd.DataFrame(d, index=['a', 'b', 'c', 'd'])

   one  two
a  1.0  4.0
b  2.0  3.0
c  3.0  2.0
d  4.0  1.0
```

- 来自字典的数组

```
data2 = [{'a': 1, 'b': 2}, {'a': 5, 'b': 10, 'c': 20}]
pd.DataFrame(data2)

   a   b     c
0  1   2   NaN
1  5  10  20.0

pd.DataFrame(data2, index=['first', 'second'])

        a   b     c
first   1   2   NaN
second  5  10  20.0

pd.DataFrame(data2, columns=['a', 'b'])

   a   b
0  1   2
1  5  10
```

### 使用 numpy array 创建

```
data = np.zeros((2,), dtype=[('A', 'i4'),('B', 'f4'),('C', 'a10')])
data[:] = [(1,2.,'Hello'), (2,3.,"World")]
pd.DataFrame(data)

   A    B      C
0  1  2.0  Hello
1  2  3.0  World

pd.DataFrame(data, index=['first', 'second'])

        A    B      C
first   1  2.0  Hello
second  2  3.0  World

pd.DataFrame(data, columns=['C', 'A', 'B'])

       C  A    B
0  Hello  1  2.0
1  World  2  3.0
```

### 使用 Serie 创建

- 索引与输入的 Series 相同，并且单个列的名称是 Series 的原始名称（仅当没有提供其他列名时）


### 从文件创建

#### csv

```
pd.read_csv('foo.csv')
```

#### h5

```
pd.read_hdf('foo.h5', 'df')
```

#### xlsx

```
pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
```

## Reference
- [API](http://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)
- [Pandas库之DataFrame](https://www.cnblogs.com/IvyWong/p/9203981.html)
- [reset_index](http://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.reset_index.html)
