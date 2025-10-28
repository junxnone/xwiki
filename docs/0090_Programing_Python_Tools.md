---
Title | Programing Python Tools
-- | --
Created @ | `2020-03-16T00:12:19Z`
Updated @| `2025-10-28T07:56:45Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/90)

---
# 工具


## 代码分析工具
- bandit
- pylint
- yapf

Name | History | Type | Description
-- | -- | -- | --
pylint | 2003 - ~ | analysis | PyCQA
 `-` | 2015 | analysis | --> PyCQA
bandit | 2018 - ~  | security | OpenStack --> PyCQA
yapf |  | formatter | Google

> analysis - static code analysis

## 代码Debug 工具
- [pdb/ipdb](0303_Programing_Python_Tools_pdb)
- [PySnooper](https://github.com/cool-RR/PySnooper)  : 以装饰器的形式打印函数运行过程中运行了哪些代码行
  - 运行时变量的值及运行的时间(`时间应该不是太准确，有打印操作`)
  - 支持监控指定函数变量
  - 支持只 debug 某段 code
  - 支持输出log到文件
- [Python Tutor](https://pythontutor.com/visualize.html#mode=edit): 代码虚拟图形分析，也可以分析 Java/JS/C/C++
- [futurecoder](https://futurecoder.io/course/#ide)： 集成 `snoop`/`Python Tutor`...
- [heartrate](https://github.com/alexmojaki/heartrate) 浏览器实时显示代码的执行次数
- [birdseye](https://github.com/alexmojaki/birdseye/tree/master): 浏览器查看执行过的 code stack data

## Config Tools
- Argparse python 内置的简单的命令行输入
- hydra
- omegaconf

## Web Tools

- **Streamlit**: 基于 Python 的 Web 应用程序框架, 可以在短时间内开发机器学习 (ML) 可视化仪表板
- **Gradio**: 快速开发 Web App


## 日期时间工具

- **datetime**
- **calendar**
- **time**

## 系统信息工具

- **psutil**: 获取系统硬件信息
- **py-cpuinfo**: CPU 相关信息(类似于 `lscpu`), 获取内容为 `dict`

## 进度条工具

- **tqdm**

## 打包工具

### 打包成 whl 
- setuptools
- wheel

### 打包成可执行文件
- pyinstaller
- nuitka
