-----

| Title     | Programing Python Tools cProfile                     |
| --------- | ---------------------------------------------------- |
| Created @ | `2026-02-28T01:17:40Z`                               |
| Updated @ | `2026-02-28T01:17:40Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/318) |

-----

# cProfile

  - Python 标准库自带的确定性性能分析器，实用的性能分析工具
  - 跟踪程序中每一个函数的调用次数、每次调用的耗时、函数执行的总时间等详细信息
  - 不会显著增加程序的运行开销
  - 记录每个函数的调用次数（ncalls）、累计耗时（tottime）、函数自身耗时（percall）、总耗时（cumtime）等核心指标。

| 指标                        | 含义                                           |
| ------------------------- | -------------------------------------------- |
| ncalls                    | 函数被调用的次数。如果是 n/m 格式，n 是总调用次数，m 是原生调用次数（排除递归） |
| tottime                   | 函数自身执行的总时间（不包含调用其他函数的耗时），单位：秒                |
| percall                   | tottime /ncalls，即每次调用函数自身的平均耗时               |
| cumtime                   | 函数累计执行的总时间（包含调用其他函数的耗时），单位：秒                 |
| percall                   | cumtime /ncalls，即每次调用的累计平均耗时                 |
| filename:lineno(function) | 函数所在的文件、行号和函数名                               |

## UseCase

### 命令行直接运行（最简单） 分析整个脚本

    python -m cProfile -s cumulative test.py

>   - \-s cumulative：按 cumtime（累计耗时）排序，优先显示最耗时的函数（最常用）；
>   - \-o result.prof：将分析结果保存到 result.prof 文件，后续可读取分析；
>   - \-l：显示函数的行号信息。

### 代码内嵌入调用（灵活）

    import cProfile
    import pstats  # 用于解析和美化分析结果
    
    # 定义需要分析的函数
    def slow_function():
        total = 0
        for i in range(1000000):
            total += i
        return total
    
    def main():
        # 1. 开始分析
        profiler = cProfile.Profile()
        profiler.enable()  # 启用分析
    
        # 执行需要分析的代码
        slow_function()
    
        # 2. 停止分析
        profiler.disable()  # 禁用分析
    
        # 3. 解析并打印结果（按累计耗时排序）
        stats = pstats.Stats(profiler)
        stats.sort_stats(pstats.SortKey.CUMULATIVE)  # 排序方式：累计耗时
        stats.print_stats(10)  # 只打印前10条结果
    
    if __name__ == "__main__":
        main()

### `.prof` 结果文件分析

    import pstats
    
    # 读取分析文件
    stats = pstats.Stats("result.prof")
    # 按累计耗时排序，打印前20条
    stats.sort_stats("cumulative").print_stats(20)
    # 还可以过滤结果，比如只显示包含 "slow" 的函数
    stats.print_stats("slow")
