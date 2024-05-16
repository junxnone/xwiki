-----

| Title     | Programing Python Tools                             |
| --------- | --------------------------------------------------- |
| Created @ | `2020-03-16T00:12:19Z`                              |
| Updated @ | `2024-05-16T11:20:32Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/90) |

-----

# 工具

## 代码分析工具

  - bandit
  - pylint
  - yapf

| Name   | History   | Type      | Description          |
| ------ | --------- | --------- | -------------------- |
| pylint | 2003 - \~ | analysis  | PyCQA                |
| `-`    | 2015      | analysis  | \--\> PyCQA          |
| bandit | 2018 - \~ | security  | OpenStack --\> PyCQA |
| yapf   |           | formatter | Google               |

> analysis - static code analysis

## 代码Debug 工具

  - [PySnooper](https://github.com/cool-RR/PySnooper) :
    以装饰器的形式打印函数运行过程中运行了哪些代码行
      - 运行时变量的值及运行的时间(`时间应该不是太准确，有打印操作`)
      - 支持监控指定函数变量
      - 支持只 debug 某段 code
      - 支持输出log到文件
  - [Python Tutor](https://pythontutor.com/visualize.html#mode=edit):
    代码虚拟图形分析，也可以分析 Java/JS/C/C++

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

## 进度条工具

  - **tqdm**
