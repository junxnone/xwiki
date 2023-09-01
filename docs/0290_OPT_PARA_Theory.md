---
Title | OPT PARA Theory
-- | --
Created @ | `2023-09-01T10:25:40Z`
Updated @| `2023-09-01T10:25:40Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/290)

---
# 并行计算理论

## Amdahl
- $S=1/((1-a) + a/n)$
  - `a` 为程序中并行计算的比例
  - `n` 为并行计算获得的加速比

## Gustafson
- 扩展加速比模型 - `@1988`
- $S = n+ (1-n) * f = f - n(f-1)$ 
  - `n` 为 程序中串行部分的比例
  - `f` 为 处理器核的数量
  - `S` 为扩展加速比


