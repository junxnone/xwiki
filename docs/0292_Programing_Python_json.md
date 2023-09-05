---
Title | Programing Python json
-- | --
Created @ | `2018-09-11T16:30:45Z`
Updated @| `2023-09-05T14:29:28Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/292)

---

# json

```
import json 
```

## 读入 json
- 将 `str` 类型的数据(File Content)转成 `dict`

```
dict_var = json.loads(file_content)
```

- 用于从 `json` 文件中读取数据

```
dict_var = json.load( open(json_file_name) )
```

## 写 json
- 将 `dict` 类型的数据转成 `str`

```
str_content = json.dumps(dict_var)
```

- 将dict类型的数据转成str, 并写入 `json` 文件

```
json.dump(dict_var, open(json_file_name, 'w') )
```

用于将dict类型的数据转成str，并写入到json文件中




## Usecase

```
def github_issue_json2md(json_path):
    with open(json_path, 'r') as jf:
        content_dict = json.loads(jf.read())
        a_body = content_dict['body']
        a_title = content_dict['title']

        with open(a_title.replace(' ', '_') + '.md', 'w') as af:
            af.write(a_body)
```

## Issues
## json.loads utf-8 codec can't decode byte 0xba
- 解决方法
```
import codecs
with codecs.open(labl_json, 'r', encoding=u'utf-8',errors='ignore') as jf:
```


## Reference

- [Python】Json模块dumps、loads、dump、load函数介绍](https://blog.csdn.net/mr_evanchen/article/details/77879967)
- [Python JSON 编码和解码 JSON 对象](http://www.runoob.com/python/python-json.html)
