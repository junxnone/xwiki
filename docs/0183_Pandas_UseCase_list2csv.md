---
Title | Pandas UseCase list2csv
-- | --
Created @ | `2019-08-12T07:24:10Z`
Updated @| `2026-11-16T09:39:50Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/183)

---
# list 保存为 csv

- 将多个等长 `list` 用 `zip` 合并后构造 `DataFrame`，再保存为 `csv`

## Code

```
import pandas as pd
list_a = ["a", "b", "c", "d", "e", "f"]
list_b = [1,2,3,4,5,6]
list_c = ["z", "y", "x", "w", "v", "u"]

pdata = list(zip(list_a, list_b, list_c))
df = pd.DataFrame(data=pdata, columns=['name', 'value', 'new_name'])
df.to_csv('./map_table.csv',index=True,header=True)
```

**df**

name | value | new_name
-- | -- | --
a | 1 | z
b | 2 | y
c | 3 | x
d | 4 | w
e | 5 | v
f | 6 | u

**map_table.csv**
```
,name,value,new_name
0,a,1,z
1,b,2,y
2,c,3,x
3,d,4,w
4,e,5,v
5,f,6,u
```

## 不保存 index

```
df.to_csv('./map_table.csv', index=False)
```
```
name,value,new_name
a,1,z
b,2,y
...
```

## 等价写法：用字典构造

```
df = pd.DataFrame({'name': list_a, 'value': list_b, 'new_name': list_c})
```

