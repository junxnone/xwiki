---
Title | Programing Python Tools PySnooper
-- | --
Created @ | `2024-05-14T06:43:45Z`
Updated @| `2024-05-14T06:43:45Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/304)

---
# PySnooper

- Debug Python Code: 使用 `装饰器` 实现的调试器，可以打印出每行执行的结果,


```
16:49:26.097070 line       109         with torch.no_grad():
16:49:26.106352 line       110             image_features, patch_features = model.encode_image(image, features_list, DPAM_layer = 20)
New var:....... image_features = tensor([[ 7.4489e-02,  9.8921e-02, -2.6420e-01, ...-01,  3.4232e-01,  1.4390e-01]], device='cuda:0')
New var:....... patch_features = [tensor([[[-0.6382, -0.5245, -0.5684,  ..., -0.3...080,  0.6653, -0.2632]]],       device='cuda:0')]
16:49:26.356453 line       111             image_features = image_features / image_features.norm(dim=-1, keepdim=True)
Modified var:.. image_features = tensor([[ 8.9026e-03,  1.1823e-02, -3.1576e-02, ...-02,  4.0912e-02,  1.7199e-02]], device='cuda:0')
16:49:26.390644 line       113             text_probs = image_features @ text_features.permute(0, 2, 1)
New var:....... text_probs = tensor([[[-0.1082,  0.2346]]], device='cuda:0')
16:49:26.423401 line       114             text_probs = (text_probs/0.07).softmax(-1)
Modified var:.. text_probs = tensor([[[0.0074, 0.9926]]], device='cuda:0')
16:49:26.456468 line       115             text_probs = text_probs[:, 0, 1]
Modified var:.. text_probs = tensor([0.9926], device='cuda:0')
```

## Use Case

### 调试函数

```
import pysnooper

@pysnooper.snoop()
def number_to_bits(number):
    if number:
        bits = []
        while number:
        ....

````

### 调试某段代码

```
import pysnooper
import random

def foo():
    lst = []
    for i in range(10):
        lst.append(random.randrange(1, 1000))

    with pysnooper.snoop():
        lower = min(lst)
        upper = max(lst)
        mid = (lower + upper) / 2
        print(lower, mid, upper)

```

### 写入 log 文件

```
@pysnooper.snoop('/my/log/file.log')
```

> 默认是终端带颜色的字体，在编辑器中会有乱码，可以使用 `color=False` 禁止带颜色


### 展开列表/词典

```
@pysnooper.snoop(watch_explode=('foo', 'self'))
```


### 使用环境变量 Disable PySnooper

> 是不是可以用来打印 卷积网络图？？


```
export PYSNOOPER_DISABLED=1
```

### 自定义输出方式

```
def large(l):
    return isinstance(l, list) and len(l) > 5

def print_list_size(l):
    return 'list(size={})'.format(len(l))

def print_ndarray(a):
    return 'ndarray(shape={}, dtype={})'.format(a.shape, a.dtype)

@pysnooper.snoop(custom_repr=((large, print_list_size), (numpy.ndarray, print_ndarray)))
def sum_to_x(x):
    l = list(range(x))
    a = numpy.zeros((10,10))
    return sum(l)

sum_to_x(10000)
```

### 默认打印长度

- 默认打印长度为 100，变量超过此值被省略

```
    @pysnooper.snoop(max_variable_length=200)
```



## Reference
- [PySnooper](https://github.com/cool-RR/PySnooper)
- [Advanced Usage](https://github.com/cool-RR/PySnooper/blob/master/ADVANCED_USAGE.md)
