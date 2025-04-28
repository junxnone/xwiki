---
Title | Programing Python pip
-- | --
Created @ | `2018-11-25T09:47:54Z`
Updated @| `2025-04-28T07:12:26Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/95)

---
# pip
- Python Package 管理工具


## UseCase

UseCase | Comandline
-- | --
Install | `sudo apt install python3-pip`<br>`sudo apt install python-pip`
Install with non-root user | `wget https://bootstrap.pypa.io/get-pip.py`<br>`python get-pip.py --user`<br>`export PATH=~/.local/bin:$PATH`
**Install Package** |
Install your package | `pip3 install your_package`
Install from requirement.txt | `pip3 install -r requirements.txt`
Install with mirror | `pip3 install your_package -i https://pypi.tuna.tsinghua.edu.cn/simple`
Export requirements.txt | `pip freeze > requirements.txt`
查看 package 信息 | `pip show -f package_name`



## Config
### Setup default Mirrors


```
vi ~/.config/pip/pip.conf
```
or
```
vi ~/.pip/pip.conf
```
```
[global]  
timeout = 6000
index-url = https://pypi.douban.com/simple/

[install]
use-mirrors = true
mirrors = https://pypi.douban.com/simple/
trusted-host = pypi.douban.com
```
```
unset all_proxy && unset ALL_PROXY && unset http_proxy && unset https_proxy
```

#### 常用 mirrors
- 清华 https://pypi.tuna.tsinghua.edu.cn/simple
- 豆瓣 http://pypi.doubanio.com/simple
- 阿里 https://mirrors.aliyun.com/pypi/simple
- 华为 https://repo.huaweicloud.com/repository/pypi/simple
- 网易 http://mirrors.163.com/pypi/simple/
- 默认 https://pypi.org/simple/

## Tips

### Editable project location

- 通过 `pip install -e .` 安装的项目是以可编辑模式安装的，源代码编辑后将直接反映在环境中
- 通过 `pip show -f package_name` 查看源码位置

```
Location: xxx/miniforge3/envs/anomalib/lib/python3.11/site-packages
Editable project location: xxx/anomalib
Requires: docstring-parser, jsonargparse, omegaconf, rich, rich-argparse
Required-by:
Files:
  ../../../bin/anomalib
  ...

```



## Issues

### No module named _internal
```
Traceback (most recent call last):   
File "/usr/bin/pip", line 9, in <module>     
from pip._internal import main 
ImportError: No module named _internal
```

- **Solution**

```
sudo apt install python-pip --reinstall
```
or

```
python -m pip install --upgrade pip
```

### Pip install package on Limited Resource Device

- Device - RAM/Disk 比较小的系统上会出现此类问题

#### Memory 不足, kswapd 进程 卡住
- 当 memory不足时，会导致`pip install` 卡住 ，`kswapd` 进程卡在最前面
- 如果 没有 swap, [增加 swap](/Increase_Swap) 
 
#### `/tmp`  No space left on device
- tmp 分区比较小，编译时空间不足
  - `export TMPDIR` 指定 tmp 目录
  - `-b` 指定 build 目录
```
export TMPDIR=your_tmp_dir
```
> `your_tmp_dir` 最好使用绝对路径, `matplotlib` 使用相对路径时出错

### SSL 问题
- 系统时间是否不准确？
- Workaround: 直接信任某些网站

```
pip install --trusted-host pypi.org --trusted-host files.pythonhosted.org <package_name>
```
- 设置为全局信任

```
#pip.ini
[global]
trusted-host = pypi.org files.pythonhosted.org download.pytorch.org
```



## Reference
- [pip configuration](https://pip.pypa.io/en/latest/user_guide/#configuration )
- [Python 生成requirement 使用requirements.txt](https://blog.51cto.com/meyangyang/2094937)


