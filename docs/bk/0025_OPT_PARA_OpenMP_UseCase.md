-----

| Title         | OPT PARA OpenMP UseCase                             |
| ------------- | --------------------------------------------------- |
| Created @     | `2021-11-05T09:31:24Z`                              |
| Last Modify @ | `2022-12-22T03:49:11Z`                              |
| Labels        | \`\`                                                |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/25) |

-----

## Reference

## Brief

  - 头文件 `include <omp.h>`
  - 格式 `#pragma omp <编译关键字> [ 子句[ [,] 子句]…… ]`

## 设定线程数量

  - 设置环境变量 `OMP_NUM_THREADS=N ./your/program`
  - 编译指令中设定 \`\#pragma omp parallel num\_threads(N)

## parallel

  - 每个 thread 都执行 并行区域 code

## for

  - 分发 loop iteration 到所有 thread

<!-- end list -->

    #pragma omp parallel
    #pragma omp for

    #pragma omp parallel for

## sections

    #pragma omp parallel sections

  - single
  - task
