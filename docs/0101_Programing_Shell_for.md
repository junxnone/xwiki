---
Title | Programing Shell for
-- | --
Created @ | `2022-06-16T02:45:07Z`
Updated @| `2024-05-30T02:20:17Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/101)

---
# Shell for

- **用途**
  - 数字遍历
  - 词组/字符串遍历
  - 路径/文件遍历

## 数字循环

### i++

```
for((i=1;i<=10;i++));
do 
    echo $(expr $i \* 3 + 1);
done
```

### `..` 生成遍历区间值

```
for i in {1..10}
do
    echo $(expr $i \* 3 + 1);
done
```

### seq 生成遍历区间值

```
for i in $(seq 1 10)
do 
    echo $(expr $i \* 3 + 1);
done
```

## 变量循环


### 输入参数遍历

```
for i in $* ;
do
    echo $i is input chart\! ;
done
```

### 遍历多个变量

```
for i in f1 f2 f3 ;
do
    echo $i is appoint ;
done
```

### 遍历变量中的字符串

```
list="rootfs usr data data2"
for i in $list;
do
    echo $i is appoint ;
done
```

### 遍历数组

```
# 定义一个数组变量
fruits=("Apple" "Banana" "Orange" "Grapes")

# 使用for循环遍历数组元素
for fruit in "${fruits[@]}"; 
do
    echo "Fruit: $fruit"
done
```


## 遍历路径匹配

```
for file in /proc/*;
do
    echo $file is file path \! ;
done
```

## 遍历命令执行结果

```
for file in $(ls *.sh)
do
    echo $file is file path \! ;
done
```

```
for i in `ls`;
do 
    echo $i is file name\! ;
done
```


## Reference
- [Shell中for循环的几个常用写法](https://blog.csdn.net/babyfish13/article/details/52981110)


