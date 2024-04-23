-----

| Title     | Programing Python Tools bandit                      |
| --------- | --------------------------------------------------- |
| Created @ | `2019-11-13T08:10:36Z`                              |
| Updated @ | `2024-04-23T02:13:44Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/91) |

-----

# bandit 代码安全分析

  - **python 代码安全分析工具**
  - Bandit使用标准库中的ast模块，将Python源码解析成Python语法节点构成的树。
  - Bandit允许用户编写自定义的测试。
  - 测试完成后，Bandit会生成针对源码的安全报告。

## Install

    pip3 install bandit

## Scan

    bandit -r /path/to/your/code

> `-lll` 只显示高危问题

## 使用配置文件

    bandit -c config -r /path/to/your/code

> bandit-config-generator 可用于产生配置文件 config file in YAML format

## 指定 baseline 文件

  - **生成为baseline 文件**

<!-- end list -->

    bandit -r /path/to/your/code -f json -o baseline.json

  - **使用baseline文件**

<!-- end list -->

    bandit -r /path/to/your/code -b baseline.json

## Reference

  - [Github - PyCQA](https://github.com/PyCQA/bandit)
  - [Docs](https://bandit.readthedocs.io/en/latest/)
