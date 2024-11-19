-----

| Title     | Programing Python Tools PySnooper                    |
| --------- | ---------------------------------------------------- |
| Created @ | `2024-05-14T06:43:45Z`                               |
| Updated @ | `2024-11-19T06:23:01Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/304) |

-----

# PySnooper

  - Debug Python Code: 使用 `装饰器` 实现的调试器，可以打印出每行执行的结果,

<!-- end list -->

    pip install pysnooper

    import pysnooper
    @pysnooper.snoop('debug_xxx.log', color=False)

    Source path:... /path/to/your/scripts/tap.py
    Starting var:.. gt_sp = [0, 0, 0, 0, 1, 1, 1, 1, 1, 1]
    Starting var:.. pr_sp = [0.9919, 0.9923, 0.9942, 0.992, 0.9916, 0.9913, 0.9926, 0.9951, 0.9894, 0.9905]
    14:52:56.296655 call        14 def test(gt_sp, pr_sp):
    14:52:56.296869 line        15     thres = 0.9979
    New var:....... thres = 0.9979
    14:52:56.296932 line        17     pr_l = [ 1 if num > thres else 0 for num in pr_sp]
    New var:....... pr_l = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    14:52:56.297000 line        18     print(pr_l)
    [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
    14:52:56.297071 line        20     aas = accuracy_score(gt_sp, pr_l)
    New var:....... aas = 0.4
    14:52:56.298280 line        22     print(f'accuracy_score：{aas}')
    accuracy_score：0.4
    14:52:56.298393 line        25     ap = average_precision_score(gt_sp, pr_sp)
    New var:....... ap = 0.6251322751322752
    14:52:56.299719 line        26     print(f'ap: {ap}')
    ap: 0.6251322751322752
    14:52:56.299832 line        28     precision, recall, thresholds = precision_recall_curve(gt_sp, pr_sp)
    New var:....... precision = array([0.6       , 0.55555556, 0.5       , 0.428...66667, 0.5       , 1.        ,       1.        ])
    New var:....... recall = array([1.        , 0.83333333, 0.66666667, 0.5  ...33333, 0.16666667, 0.16666667,       0.        ])
    New var:....... thresholds = array([0.9894, 0.9905, 0.9913, 0.9916, 0.9919, 0.992 , 0.9923, 0.9926,       0.9942, 0.9951])
    14:52:56.300593 return      28     precision, recall, thresholds = precision_recall_curve(gt_sp, pr_sp)
    Return value:.. None
    Elapsed time: 00:00:00.004629

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

```

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

    @pysnooper.snoop('/my/log/file.log')

> 默认是终端带颜色的字体，在编辑器中会有乱码，可以使用 `color=False` 禁止带颜色

### 展开列表/词典

    @pysnooper.snoop(watch_explode=('foo', 'self'))

### 使用环境变量 Disable PySnooper

> 是不是可以用来打印 卷积网络图？？

    export PYSNOOPER_DISABLED=1

### 自定义输出方式

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

### 默认打印长度

  - 默认打印长度为 100，变量超过此值被省略

<!-- end list -->

``` 
    @pysnooper.snoop(max_variable_length=200)
```

> `max_variable_length=None` 不限制输出

## Reference

  - [PySnooper](https://github.com/cool-RR/PySnooper)
  - [Advanced
    Usage](https://github.com/cool-RR/PySnooper/blob/master/ADVANCED_USAGE.md)
