-----

| Title     | OPT PARA                                            |
| --------- | --------------------------------------------------- |
| Created @ | `2021-11-05T09:03:54Z`                              |
| Updated @ | `2023-09-01T10:20:07Z`                              |
| Labels    | \`\`                                                |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/22) |

-----

# 并行计算

## 任务并行 & 数据并行

  - 数据并行 - `Data Parallelism` - 数据可以分发到不同的计算单元，进行并行处理
  - 任务并行 - `Task Parallelism` - 不同的任务处理不同的数据并行进行

![image](media/59bbd92c9fbeab14dc382e7ae1c0913eedaada7a.png)

## Parallel Programming Models

  - Shared Memory (without threads)
  - Threads
  - Distributed Memory / Message Passing
  - Data Parallel
  - Hybrid
  - SPMD - `Single Program Multiple Data`
  - MPMD - `Multiple Program Multiple Data`

### SPMD

  - vs SIMD
      - SIMD: 处理器体系结构，指令级，执行相同的指令集
      - SPMD: 编程模型，程序级，可以包含不同的指令集/执行路径(分支)

## Optimization

  - 线程并行
      - \[\[OpenMP\]\]
      - \[\[SYCL\]\]
      - \[\[DPCPP\]\]
      - \[\[OpenCL\]\]
  - 向量化 - \[\[SIMD\]\]
  - High-Level Optimization
      - 增加并行 - 保证 Hardware 高利用率
      - 最小化 Kernel - 保持 Kernel 保存在 Instruction Cache
      - Kernel Balance - 避免 长时间执行的 Kernel 成为瓶颈
      - 避免执行时间长的函数
  - [Memory-related Optimizations](/Memory_Optimizations)
  - [Loop - related Optimizations](/Loop_Optimizations)

## Tools

  - \[\[Vtune\]\]
  - [pmu tools](https://github.com/andikleen/pmu-tools)

## Tips

  - [Program Bind Socket Core](/Program_Bind_Socket_Core)

## Reference

  - [Introduction to Parallel Computing
    Tutorial](https://hpc.llnl.gov/training/tutorials/introduction-parallel-computing-tutorial)
  - [并行计算blogs](http://parallel.zhangjikai.com/)
  - [Optimize - Intel® oneAPI Programming
    Guide](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-programming-guide/top/software-development-process/performance-tuning-cycle/optimize.html)
  - [Software optimization resources](https://www.agner.org/optimize/)
