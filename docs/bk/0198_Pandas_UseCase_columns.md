-----

| Title         | Pandas UseCase columns                               |
| ------------- | ---------------------------------------------------- |
| Created @     | `2022-12-22T09:27:16Z`                               |
| Last Modify @ | `2022-12-22T09:27:16Z`                               |
| Labels        | \`\`                                                 |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/198) |

-----

# 列操作

## 选择列

### 通过 label 选择单列

    df['id']  ->选择列 'id'
    df.id  -> 同上

### 通过 `loc` 选择多列

    df.loc[:,'id']  -> 同上
    df.loc[:,['id', 'coef']]  -> 选择两列

| 操作      | 语法                                | 结果        |
| ------- | --------------------------------- | --------- |
| 选择列     | df\[col\]                         | Series    |
| 按标签选择多列 | df\[\['name', 'label', 'year'\]\] | DataFrame |

## 添加新列

### 根据其他列创建新列

    df['three'] = df['one'] * df['two']
    df['flag'] = df['one'] > 2
    df['foo'] = 'bar' # 自动扩充添加列
    df['one_trunc'] = df['one'][:2]

### 使用字典添加新列

    df = df.append(dict_a, ignore_index=True)

### 通过 `numpy array` 赋值

    df.loc[:, 'coef'] = np.array([5] * len(df))

### 插入某列

    df.insert(1, 'bar', df['one'])

``` 
   one   flag  foo  one_trunc
a  1.0  False  bar        1.0
b  2.0  False  bar        2.0
c  3.0   True  bar        NaN
d  NaN  False  bar        NaN

----after insert----

   one  bar   flag  foo  one_trunc
a  1.0  1.0  False  bar        1.0
b  2.0  2.0  False  bar        2.0
c  3.0  3.0   True  bar        NaN
d  NaN  NaN  False  bar        NaN
```

### assign 添加新列

``` 
(iris.assign(sepal_ratio = iris['SepalWidth'] / iris['SepalLength'])

   SepalLength  SepalWidth  PetalLength  PetalWidth         Name  sepal_ratio
0          5.1         3.5          1.4         0.2  Iris-setosa       0.6863
1          4.9         3.0          1.4         0.2  Iris-setosa       0.6122
2          4.7         3.2          1.3         0.2  Iris-setosa       0.6809
3          4.6         3.1          1.5         0.2  Iris-setosa       0.6739
4          5.0         3.6          1.4         0.2  Iris-setosa       0.7200


## 传递函数，效果同上
iris.assign(sepal_ratio = lambda x: (x['SepalWidth'] / x['SepalLength'])).head() 

```

### 从一列的字符串中分离出部分字符成为新的一列

    df['category'] = df['name'].str.split('_',1).str[0]

> 假设 df\['name'\] 为类似字符 `Class1_0000xxx.png`

## 删除列

### drop 删除列

    df.drop(df.columns[0],axis=1,inplace=True) ->删除第一列
    df.drop(df.columns[[0,1]],axis=1,inplace=True) ->删除第 0,1 列
    df.drop(['id','coef'],axis=1,inplace=True)  删除 'id' 'coef‘ 列

### del 删除列

    del df['two']

### pop 删除列

    three = df.pop('three')
