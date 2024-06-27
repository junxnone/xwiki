---
Title | Tools Jupyter
-- | --
Created @ | `2018-09-25T07:48:41Z`
Updated @| `2024-06-27T00:55:35Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/163)

---
# Jupyter

- jupyter - web 端 开发工具
- 支持语言
  - python
  - C++ - jupyter_cpp
- [Jupyrwe Kernels](https://github.com/jupyter/jupyter/wiki/Jupyter-kernels)
- [Jupyter Magic Commands]

## Install with pip

- Host / Virtualenv

```
pip3 install jupyter
```

## UseCase

UseCase | Command
-- | --
本机使用 | `jupyter notebook`
本机打开文件 | `jupyter notebook notebook.ipynb`
在其他主机访问 | `jupyter notebook --ip=xxx.xxx.xx.xx(local IP)`
后台运行 | `nohup jupyter notebook --ip=xxx.xxx.xx.xx &`
Work with virtualenv | `workon yourvirtualenv`<br>`pip install ipykernel`<br>`ipython kernel install --user --name=yourvirtualenv`<br>`jupyter notebook`
works with conda | `conda install nb_conda_kernels`
remove from ipykernel | `jupyter kernelspec remove your_kernel_name`


## Jupyter notebook extensions
```
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
```

常用扩展 | 描述
-- | --
Collapsible headings | 折叠标题
Notify | 通知机制，跑一些耗时较久的任务，完成后通知
Codefolding | 折叠代码
Zen mode | 隐藏活动状态栏，方便注意代码
Execute Time | 显示运行的时间
jupytext | 同步保存 py 文件


## Tips
### 查看方法帮助
1 方法后面添加 `?` <br> `cv2.resize?` | ![image](https://user-images.githubusercontent.com/2216970/70609679-2a828100-1c3d-11ea-8d1a-ebb16f050037.png)
-- | --
2 <kbd>Shift</kbd> + <kbd>Tab</kbd> | ![image](https://user-images.githubusercontent.com/2216970/70609869-84834680-1c3d-11ea-9673-b634a7cb9caf.png)


### Magic Command

cmd | Description
-- | --
%time | 当前**行**的代码运行一次所花费的时间
%%time | 当前**cell**的代码运行一次所花费的时间
%timeit | 执行一个语句100，000次(默认情况下)，然后给出运行最快3次的平均值<br> -n N 指定执行次数
`%%writefile test.txt` | 将当前单元格内容写到文件


## Reference 

- [jupyter](https://jupyter.org/) 
- [Jupyter 同时支持python2, python3](https://www.cnblogs.com/mashuai-191/p/9045736.html)
- [Jupyter Notebook 的快捷键](https://www.cnblogs.com/zhizhan/p/5660031.html)
- [Jupyter Magic - Timing(%%time %time %timeit)](https://blog.csdn.net/shuibuzhaodeshiren/article/details/86650688)
- [awesome-jupyter - tools, packages](https://github.com/markusschanta/awesome-jupyter)
- [Jupyter notebook extensions](https://github.com/ipython-contrib/jupyter_contrib_nbextensions/blob/master/README.md) 
- [My notebook example on Github](https://github.com/junxnone/jupyter_notebook.git)


