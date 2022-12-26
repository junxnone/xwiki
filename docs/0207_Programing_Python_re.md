---
Title | Programing Python re
-- | --
Created @ | `2019-05-23T15:35:05Z`
Last Modify @| `2022-12-26T03:19:16Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/207)

---
# re 正则表达式模块
## Reference
- [Python3 正则表达式](https://www.runoob.com/python3/python3-reg-expressions.html) 
- [Python正则表达式指南](https://www.cnblogs.com/huxi/archive/2010/07/04/1771073.html)

## Brief

- re.match
- re.search
- re.sub
- re.compile
- re.finditer
- re.split

## Examples

- 查找字符串中的数字

```
import re
pattern = re.compile('[0-9]+')
match = pattern.findall(str)
```



