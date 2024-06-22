---
Title | X JITvsAOT
-- | --
Created @ | `2024-06-22T09:46:07Z`
Updated @| `2024-06-22T09:46:07Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/308)

---
# JIT vs AOT
- JIT - `Just-in-Time` - 即时编译(动态编译) - 在程序执行期间对计算机代码进行编译
  - JIT编译是静态编译和解释的结合，结合了两者的优点和缺点。
  - 使用 JIT 的语言有 Java/C#/Python/Lua/Julia/PHP8.0, SYCL 中支持多种硬件的方式也使用 JIT
- AOT - `Ahead of time` - 提前编译(提前编译) 
  - AOT 则包含 C/C++/Java, 可以 减少运行时开销，提高性能
