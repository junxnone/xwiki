---
Title | Doc Tools pandoc mdtoc
-- | --
Created @ | `2023-06-24T10:37:34Z`
Updated @| `2023-06-24T10:37:34Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/273)

---
# Pandoc: 生成目录TOC

```
pandoc --wrap=preserve -f gfm --toc -s input.md  -o output.md -w gfm
```
