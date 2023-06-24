---
Title | Doc Tools pandoc
-- | --
Created @ | `2023-06-24T04:50:42Z`
Updated @| `2023-06-24T05:18:13Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/268)

---
# Pandoc
- 转换 markdown -> pdf
- 提取媒体文件



## 提取媒体文件

- `input.md` --> `output.md`  
- `images` -> `media/`
```
pandoc --wrap=preserve -f markdown input.md --extract-media=media -t markdown -o output.md
```


## Reference
- [[官网](https://pandoc.org/)]  [[Getting started](https://pandoc.org/getting-started.html)] [[User’s Guide](https://pandoc.org/MANUAL.html)]
- [github pandoc action](https://github.com/pandoc/pandoc-action-example)
- [Pandoc 从入门到精通 - 提取媒体文件](https://sspai.com/post/77206)
