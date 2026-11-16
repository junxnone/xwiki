-----

| Title     | Pandas                                               |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-03-04T05:45:56Z`                               |
| Updated @ | `2026-11-16T09:39:46Z`                               |
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

  - [Series](/0184_Pandas_Series) - 带标签的一维数组
  - [DataFrame](/0182_Pandas_DataFrame) - 带行/列索引的二维表格

### UseCase（常用操作）

  - [Pandas UseCase](/0260_Pandas_UseCase) - 用例总览

| 分类           | 文档                                                                                                                                             |
| ------------ | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| 数据读写         | [IO](/0188_Pandas_UseCase_IO) / [list 保存为 csv](/0183_Pandas_UseCase_list2csv)                                                                  |
| 行 / 列 / 索引   | [行操作](/0199_Pandas_UseCase_row) / [列操作](/0198_Pandas_UseCase_columns) / [Index](/0202_Pandas_UseCase_Index) / [xy 取值](/0200_Pandas_UseCase_xy) |
| 筛选 / 排序 / 采样 | [条件筛选](/0201_Pandas_UseCase_condition) / [排序](/0186_Pandas_UseCase_sort) / [采样](/0203_Pandas_UseCase_sampling)                                 |
| 清洗 / 合并      | [特殊值处理](/0187_Pandas_UseCase_SpecialValue) / [字符串处理](/0204_Pandas_UseCase_string) / [Merge](/0205_Pandas_UseCase_Merge)                        |
| 查看信息         | [Summary Info](/0197_Pandas_UseCase_ShowSummaryInfo)                                                                                           |

### 可视化

  - [可视化](/0189_Pandas_Visualization)

### Issues（踩坑记录）

  - [Pandas Issues](/0262_Pandas_Issues) - 总览
  - [SettingWithCopyWarning](/0185_Pandas_Issues_SettingWithCopyWarning)
  - [csv 中 list 变成 str](/0213_Pandas_Issues_csvliststr)

## Reference

  - [官网](https://pandas.pydata.org/)
  - [User Guide](https://pandas.pydata.org/docs/user_guide/index.html)
  - [cn - teadocs](https://www.pypandas.cn/)
  - [cn - apachencn](http://pandas.apachecn.org/)
