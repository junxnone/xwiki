---
Title | Programing Python Argparse
-- | --
Created @ | `2018-09-02T14:46:47Z`
Updated @| `2023-06-17T06:51:01Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/258)

---
# Argparse

- Parser for command-line options, arguments and sub-commands
- python 脚本参数解析

```
import argparse
parser = argparse.ArgumentParser()
parser.add_argument("echo")
args = parser.parse_args()
print(args.echo)
```

## `add_argument()` parameters

### type

```
parser.add_argument('count', type=int)
```

- float
- int
- str
- function 


#### function 
- type-checking and type conversions

```
>>> def perfect_square(string):
...     value = int(string)
...     sqrt = math.sqrt(value)
...     if sqrt != int(sqrt):
...         msg = "%r is not a perfect square" % string
...         raise argparse.ArgumentTypeError(msg)
...     return value
...
>>> parser = argparse.ArgumentParser(prog='PROG')
>>> parser.add_argument('foo', type=perfect_square)
>>> parser.parse_args(['9'])

### choices

```
parser.add_argument('move', choices=['rock', 'paper', 'scissors'])
```

### required
- True/False

```
parser.add_argument('--foo', required=True)
```

### help

```
parser.add_argument('--foo', action='store_true',
                    help='foo the bars before frobbling')
```

### action
- store(default) - 仅存储参数
- store_const - 指定默认值 `const=xx`
- store_true - 指定默认值 True
- store_false - 指定默认值 False
- append - 指定多值，append 到 list
- append_const
- count
- help
- version
- extend




## UseCase

### 参数多值传入

- 一次传入多个文件为 `list`

```
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('--kgf', type=str, nargs='+', default='none', help='python merge_kg.py kg1.json kg2.json kg3.json')
args = parser.parse_args()
print(args.kgf)
```

```
$ python3 merge_kg.py --kgf linux_kg.json wiki_kg.json xwiki_kg.json aiwiki_kg.json 

['linux_kg.json', 'wiki_kg.json', 'xwiki_kg.json', 'aiwiki_kg.json']
```



```

## Reference

- [argparse ——  The Python Standard Library](https://docs.python.org/3/library/argparse.html)
- [args type](https://docs.python.org/3/library/argparse.html#type)
- [jupyter notebook](https://nbviewer.jupyter.org/github/junxnone/examples/blob/master/python/argparse.ipynb)

