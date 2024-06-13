---
Title | Programing Python Decorator property
-- | --
Created @ | `2024-06-13T09:09:44Z`
Updated @| `2024-06-13T09:09:44Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/306)

---
# `@property` decorator
- 只能修饰不带参数的方法
- 用于隐藏变量，变量只读，控制属性访问权限
- 使类中的方法，可以像类中属性一样的方式被调用

```
class ds(object):
  @property
  def temp(self):
    return 11
  def temp_wo_p(self):
    return 12

d1 = ds()
print(d1.temp)
print(d1.temp_wo_p())
print(d1.temp_wo_p)

```

- **Output**

```
11
12
<bound method ds.tw of <__main__.ds object at 0x7fd3d03c8550>>
```




