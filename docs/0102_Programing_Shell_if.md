---
Title | Programing Shell if
-- | --
Created @ | `2019-07-25T08:00:08Z`
Last Modify @| `2022-12-22T06:42:19Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/102)

---
# if  判断

## Brief

- 判断变量是否相等
- 判断是否是数字 `N`
- 判断是否是字符串 `xxx`


```
i=1
if [ $i -lt 10 ]
then
    echo "xxx"
else
    echo "xxx"
fi
```
> 注意 $i 和 10 前后都有空格  

## UseCase

### 判断变量是否是 `0`

```
if [ $var -eq 0 ];then
    echo "$var is 0"
else
    echo "$var is not 0"
fi
```
```
if [ $var == 0 ]
then
    echo "$var is 0"
else
    echo "$var is not 0"
fi
```

### 判断变量是否为字符串`xxx`

```
if [ $var == 'abc' ]
then
    echo "$var is abc"
else
    echo "$var is not abc"
fi
```

### 判断变量是否相等

```
if [ $var == $var2 ]
then
    echo "$var = $var2"
else
    echo "$var != $var2"
fi
```
