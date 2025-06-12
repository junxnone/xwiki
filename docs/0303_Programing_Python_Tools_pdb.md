---
Title | Programing Python Tools pdb
-- | --
Created @ | `2024-04-23T02:03:59Z`
Updated @| `2025-06-12T08:21:00Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/303)

---
# pdb/ipdb
- 插入断点以便逐步调试
- **pdb**: Python 标准库的一部分，内置调试器
- **ipdb**: 基于 pdb + IPython 的增强版
  - 支持 IPython 特性：语法高亮、自动补全（按 Tab 键）、多行输入（如直接编写循环 / 条件语句）。
  - 美化打印（pp 命令）：复杂数据结构显示更清晰，可读性更强。
  - 可使用 IPython 内置函数（如 %timeit 性能分析）


| **维度**         | **`pdb`**                              | **`ipdb`**                            |
|------------------|----------------------------------------|---------------------------------------|
| **安装**         | 无需安装（内置）                       | 需要 `pip install ipdb`               |
| **交互体验**     | 基础文本界面，无自动补全/高亮          | 支持 IPython 特性，交互更高效         |
| **适合场景**     | 简单调试、生产环境（轻量级）、纯净环境 | 开发阶段调试、复杂逻辑排查、交互式开发 |
| **学习成本**     | 较低（命令简单，但功能有限）           | 与 `pdb` 兼容，额外学习 IPython 特性   |
| **扩展性**       | 有限                                   | 可集成 IPython 插件、魔法命令等        |

## ipdb

```
pip install ipdb
```


```
import ipdb; ipdb.set_trace()  
```

| 命令         | 说明                                                                 |
|--------------|----------------------------------------------------------------------|
| `n`/`next`   | 执行下一条语句（不进入函数调用内部）                                 |
| `s`/`step`   | 单步执行，进入函数调用内部（用于追踪函数内部逻辑）                   |
| `c`/`continue` | 继续执行程序，直到遇到下一个断点或程序结束                          |
| `l`/`list`   | 显示当前代码上下文（默认显示 11 行）                                 |
| `p <expr>`   | 打印表达式的值（如 `p result`）                                      |
| `pp <expr>`  | 美化打印表达式的值（适合复杂数据结构）                               |
| `where`/`w`  | 查看当前调用栈（追踪代码执行路径）                                   |
| `exit`/`q`   | 退出调试模式                                                       |
| `help`       | 查看所有可用命令的帮助信息                                           |



## pdb

```
import pdb; 

your_code
...
pdb.set_trace()
....


```

### 调试方法

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
- [pdb doc](https://docs.python.org/3/library/pdb.html)
- [ipdb repo](https://github.com/gotcha/ipdb)
