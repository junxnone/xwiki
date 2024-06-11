---
Title | Programing Shell Tips
-- | --
Created @ | `2024-06-11T11:34:55Z`
Updated @| `2024-06-11T11:34:55Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/305)

---
# Shell Tips

## 回显执行过的命令

```
set -x 
```

> 脚本结束位置加 `set +x`，否则会在终端执行命令时也回显
