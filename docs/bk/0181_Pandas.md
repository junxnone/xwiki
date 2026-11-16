-----

| Title     | Pandas                                               |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-03-04T05:45:56Z`                               |
| Updated @ | `2026-11-16T09:34:40Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/181) |

-----

# Pandas

  - 数据分析处理工具，提供 `Series`（一维）和 `DataFrame`（二维表格）两种核心数据结构
  - 常用于数据清洗、转换、统计分析、读写 `csv`/`excel`/`json` 等文件以及简单可视化

<!-- end list -->

``` python
import pandas as pd
import numpy as np
```

## 文档索引

### 基础数据结构

  - [Series](https://github.com/junxnone/xwiki/issues/184) - 带标签的一维数组
  - [DataFrame](https://github.com/junxnone/xwiki/issues/182) -
    带行/列索引的二维表格

### UseCase（常用操作）

  - [Pandas UseCase](https://github.com/junxnone/xwiki/issues/260) -
    用例总览

| 分类           | 文档                                                                                                                                                                                                                        |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 数据读写         | [IO](https://github.com/junxnone/xwiki/issues/188) / [list 保存为 csv](https://github.com/junxnone/xwiki/issues/183)                                                                                                         |
| 行 / 列 / 索引   | [行操作](https://github.com/junxnone/xwiki/issues/199) / [列操作](https://github.com/junxnone/xwiki/issues/198) / [Index](https://github.com/junxnone/xwiki/issues/202) / [xy 取值](https://github.com/junxnone/xwiki/issues/200) |
| 筛选 / 排序 / 采样 | [条件筛选](https://github.com/junxnone/xwiki/issues/201) / [排序](https://github.com/junxnone/xwiki/issues/186) / [采样](https://github.com/junxnone/xwiki/issues/203)                                                            |
| 清洗 / 合并      | [特殊值处理](https://github.com/junxnone/xwiki/issues/187) / [字符串处理](https://github.com/junxnone/xwiki/issues/204) / [Merge](https://github.com/junxnone/xwiki/issues/205)                                                     |
| 查看信息         | [Summary Info](https://github.com/junxnone/xwiki/issues/197)                                                                                                                                                              |

### 可视化

  - [可视化](https://github.com/junxnone/xwiki/issues/189)

### Issues（踩坑记录）

  - [Pandas Issues](https://github.com/junxnone/xwiki/issues/262) - 总览
  - [SettingWithCopyWarning](https://github.com/junxnone/xwiki/issues/185)
  - [csv 中 list 变成 str](https://github.com/junxnone/xwiki/issues/213)

## Reference

  - [官网](https://pandas.pydata.org/)
  - [User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
  - [cn - teadocs](https://www.pypandas.cn/)
  - [cn - apachencn](http://pandas.apachecn.org/)
