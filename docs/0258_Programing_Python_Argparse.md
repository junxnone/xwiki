---
Title | Programing Python Argparse
-- | --
Created @ | `2018-09-02T14:46:47Z`
Updated @| `2023-06-17T06:31:52Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/258)

---
# Argparse

- Parser for command-line options, arguments and sub-commands
- python 脚本参数解析

## [type](https://docs.python.org/3/library/argparse.html#type)
**type-checking and type conversions**

- float
- int
- function 

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
```

## 参数多值传入

- 一次传入多个文件为 `list`

```
import argparse

ap = argparse.ArgumentParser()
ap.add_argument('--kgf', type=str, nargs='+', default='none', help='python merge_kg.py kg1.json kg2.json kg3.json')
args = ap.parse_args()
print(args.kgf)
```

```
$ python3 merge_kg.py --kgf linux_kg.json wiki_kg.json xwiki_kg.json aiwiki_kg.json 

['linux_kg.json', 'wiki_kg.json', 'xwiki_kg.json', 'aiwiki_kg.json']
```


## Reference

- [argparse ——  The Python Standard Library](https://docs.python.org/3/library/argparse.html)
- [jupyter notebook](https://nbviewer.jupyter.org/github/junxnone/examples/blob/master/python/argparse.ipynb)

