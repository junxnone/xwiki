-----

| Title     | Doc YAML                                             |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-08-07T02:06:17Z`                               |
| Updated @ | `2024-10-23T09:02:38Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/140) |

-----

# YAML

  - YAML - `Yet Another Markup Language` - 类似 `xml/json`
  - **用途**: yaml 作为配置文件 （kubernetes/docker/...)
  - **python 常用工具** pyyaml/ruamel/yaml/yacs/hydra

## YAML 语言规则

  - 大小写敏感
  - `key: value` - `:` 后面加空格

### 层级关系

  - 使用空格缩进，相同层级对齐即可

### 数据类型

#### 字典

#### 数组

  - 以 `-` 开头的行表示构成一个数组
  - 多维数组表示 - `key: [value1, value2, ...]`

#### 纯量

  - `int/float/string/boolen/...`

### 注释

  - 注释标识为 `#`

### `yaml.load` vs `yaml.safe_load`

    Warning: It is not safe to call yaml.load with any data received from an untrusted source!
    yaml.load is as powerful as pickle.load and so may call any Python function. 
    Check the yaml.safe_load function though.

## Tools

  - [pyYAML](https://github.com/yaml/pyyaml)
  - [yacs](https://github.com/rbgirshick/yacs/tree/master)
  - [hydra](https://github.com/facebookresearch/hydra)

## History

  - 2004.01.29 `spec 1.0`
  - 2004.12.30 `spec 1.1`
  - 2010.20.01 `spec 1.2`

## Reference

  - [YAML Spec](https://yaml.org/spec/)
  - **pyyaml** \[[code](https://github.com/yaml/pyyaml)\]
    \[[docs](https://pyyaml.org/wiki/PyYAMLDocumentation)\]
      - [python：yaml模块](https://www.jianshu.com/p/eaa1bf01b3a6)
  - **ruamel.yaml**
    \[[code](https://sourceforge.net/p/ruamel-yaml/code/ci/default/tree/)\]
    \[[docs](https://yaml.readthedocs.io/en/latest/)\]
      - [ruamel.yaml - Differences with
        PyYAML](https://yaml.readthedocs.io/en/latest/pyyaml.html)
  - [material and tools](https://yaml.org/)
