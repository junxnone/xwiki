---
Title | Programing CPP lambda
-- | --
Created @ | `2023-03-01T07:58:20Z`
Updated @| `2023-03-01T07:58:20Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/214)

---


## Reference

- [Lambda expressions](https://en.cppreference.com/w/cpp/language/lambda)

## Brief

- `[ captures ] ( params ) specs requires ﻿(optional) { body }`

## captures
- 定义外部作用域变量访问的方式
- `[]` 无变量访问
- `[&]` 引用访问
- `[=]` copy 访问
- `[x, &y]` x 按值传递, y 引用传递
- ...

