---
Title | Programing CPP STD STL
-- | --
Created @ | `2021-07-27T02:50:05Z`
Updated @| `2023-06-04T04:53:33Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/83)

---
# 标准模板库
- STL -  `Standard Template Library`
- 最初由惠普实验室开发，于 1998 年被定为国际标准，成为 C++ 标准库的重要组成部分
- **内置**到 `C++ Compiler` 中(头文件方式提供)
- 包含一些容器/算法/...


## 组成

1. 容器（Containers）：提供了一些基本的数据结构，如vector、list、deque、queue、stack、set和map等，在容器上进行插入、删除、查找、排序等操作。
2. 迭代器（Iterators）：允许用户遍历容器中的元素，是一个类似于指针的对象，C++中的内置指针也是一种迭代器。
3. 函数对象（Function objects）：类似于函数指针，但它是一种类对象，可以代表函数、函数指针和函数指针所指向的函数体。
4. 算法（Algorithms）：STL提供了很多通用的算法，如排序、查找、合并、去重、计数、生成等。
5. 迭代器适配器（Iterator Adapters）：提供了对迭代器的适配和转换，如反向迭代器、插入迭代器和流迭代器等。
6. 分配器（Allocators）：用于管理动态内存分配，提供了一些基本的分配器，如allocaor、new_allocator等。
7. 智能指针（Smart pointers）：封装了指针，并在适当的时候自动释放所指向的内存，如unique_ptr、shared_ptr和weak_ptr等。


## Reference
- [STL - Standard Template Library - wikipedia](https://en.wikipedia.org/wiki/Standard_Template_Library)
- [STL教程：C++ STL快速入门](http://c.biancheng.net/view/6557.html)
- [C++ 标准库容器](https://learn.microsoft.com/zh-cn/cpp/standard-library/stl-containers)
