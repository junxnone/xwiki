---
Title | Programing Python Tools pdb
-- | --
Created @ | `2024-04-23T02:03:59Z`
Updated @| `2024-06-19T06:28:20Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/303)

---
# pdb
- 插入断点以便逐步调试


```
import pdb; 

your_code
...
pdb.set_trace()
....


```

## 调试方法

```
h (help) : 帮助
n（next）：执行下一行代码。
c（continue）：继续执行直到下一个断点。
s（step）：逐行执行代码，如果遇到函数则进入函数内部。
q（quit）：退出调试模式。
w (where) : 打印 stack trace
r (return) : 继续执行到当前函数的返回处
l (list): 列出当前执行的行附近的行(默认 11行，可以加参数)
ll (longlist): 列出整个function 或 frame

```


## Reference
- [doc](https://docs.python.org/3/library/pdb.html)
