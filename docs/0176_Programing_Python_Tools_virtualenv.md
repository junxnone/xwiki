---
Title | Programing Python Tools virtualenv
-- | --
Created @ | `2018-11-25T09:53:47Z`
Updated @| `2024-06-26T06:05:27Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/176)

---
# virtualenv

- 用于创建独立的 python 虚拟环境, 隔离 host python 环境
- 一般使用 [[virtualenvwrapper]] 管理虚拟环境

## Install

### pip

```
pip3 install virtualenv
```

### apt

```
sudo apt install -y virtualenv
```

> Raspberry pi 3B 

## UseCase

### 创建虚拟环境

`virtualenv yourenv` 

#### 创建特定python 版本的虚拟环境

```
virtualenv -p python3 env
```

### 使用虚拟环境

```
source yourenv/bin/activate
```

### 退出虚拟环境

```
deactivate
```

