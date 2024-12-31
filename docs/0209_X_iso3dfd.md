---
Title | X iso3dfd
-- | --
Created @ | `2021-11-08T08:44:04Z`
Updated @| `2024-12-31T01:51:57Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/209)

---
# iso3dfd
- 偏微分方程(Partial Differential Equation - PDE) 问题: 声波在 `各向同性介质` 中的传播
- OpenMP 优化
- 有限差分(Finite-difference) 用于近似 偏微分方程
- [SYCL Code 分析](https://github.com/junxnone/oneAPI-samples/issues/1)

###  问题描述
- **p**: 压力/压强/应力 `@t`
- **v**: 速度 `@t`
- **t**: 时间

2D 波动方程 | 3D 波动方程
--  | --
![image](https://user-images.githubusercontent.com/2216970/140710523-15f2cc22-8dfe-4d44-94c4-0331f23c0831.png) | ![image](https://user-images.githubusercontent.com/2216970/140710530-3f6d0907-3b04-418f-b285-04399edb13bc.png)


## iso2dfd
- 使用有限差分 2 阶模板
- 2D 方程 离散化 -->


---

![image](https://user-images.githubusercontent.com/2216970/140723634-fc7aba3b-0a62-44f9-ba80-90a8a0329542.png)
-- | 
![image](https://user-images.githubusercontent.com/2216970/140723652-48e87e0d-5030-4b28-be5d-d7d61b66c1d9.png)

> p<sub>i, j</sub><sup>n+1</sup> ： 在时间 `n+1` 时 位置 `i, j` 处的压力波场值



![image](https://user-images.githubusercontent.com/2216970/140723893-65216db5-018a-4d04-977c-9482b4e787e6.png)


## iso3dfd

- 使用有限差分 16 阶模板
- 3D 方程 离散化
- Shared Local Memory Optimization for iGPU

计算公式
:--: |
![image](https://user-images.githubusercontent.com/2216970/140724354-f275ed0b-05d6-4a04-abe1-5f32d1ca278b.png)


![image](https://user-images.githubusercontent.com/2216970/145940342-d4d395f6-c002-4d24-a4aa-4cefe790693d.png) | ![oInlZwTSIM](https://user-images.githubusercontent.com/2216970/141894886-901adfd1-dda4-4998-9c2f-525b11c83523.gif)
-- | --
为了计算边缘点，每个维度需要向外扩展 2 x 8(kHalfLength) | 每个维度正负方向 `+8`<br> 计算右上角的点需要 48 (8 x 3 x 2) 个点(紫色部分点)

![image](https://user-images.githubusercontent.com/2216970/141893331-39db815d-61fa-4ad7-bf72-87f6ffbefd7a.png)
-- |


## Optimization


### SIMD Vectorization
- 使用 OpenMP SIMD 指令 使 处理时 使用 SIMD 并行化

![image](https://user-images.githubusercontent.com/2216970/141059698-55584797-ef18-4452-bd17-d5d373cb5969.png)


### Improve Memory Access
- simd 访问连续内存
- **Intel Advisor**
  - **Uniform stride**: 理想情况，一直访问同一个地址
  - **Unit stride**: 访问连续的地址, 可以提升 `cache reusage`,
  - **Constant stride**: 访问结构化数据，应该避免，并提升到 `Unit stride`, 一般是 `wrong iteration order· 造成
  - **Random access**: 最坏情况,很难避免，间接寻址是主要原因
- 更改 x 轴作为最内层循环，从 `Constant stride` 到 `Unit stride`

![image](https://user-images.githubusercontent.com/2216970/141060078-b40abbea-9434-4e08-b3d7-9ed49cdb0cc7.png)


### Threading Parallelism
- 使用 OpenMP 多线程

![image](https://user-images.githubusercontent.com/2216970/141060410-7194a867-a2f4-47d4-bad1-57bc9012dd01.png)


### Cache Reuse
- 添加 `Cache blocking` 提升 Cache 利用率(减少 DRAM 交互)

![image](https://user-images.githubusercontent.com/2216970/141060752-4a421708-3468-4857-b4eb-29d47b32b20c.png)


### [openmp implementation](https://github.com/oneapi-src/oneAPI-samples/tree/master/DirectProgramming/C%2B%2B/StructuredGrids/iso3dfd_omp_offload)

- **Baseline**: `OpenMP` + `SIMD` + `Cache Reuse` + `Improve Memory Access` + `Default Distribution`
- **Opt1**: `Baseline` + `Tiling Approach distribution`(OpenMP teams)
- **Opt2**: `Baselin` +  `Tiling Approach distribution`(OpenMP teams) + `Registers front/back`
- **Opt3**: `Baselin` +  `Tiling Approach distribution`(OpenMP teams) + `Registers front/back` + `CPU Threads`

## Tips

- windows 编译使用 SLM: 添加 `-DUSE_SHARED` 到 `项目属性->DPC++->Command Line->其他选项`

![image](https://user-images.githubusercontent.com/2216970/147624212-e4b20ea0-ccbc-429d-afaa-03eab75878f3.png)


## Reference
- [ISO3DFD Code Walkthrough](https://www.intel.com/content/www/us/en/developer/articles/technical/iso3dfd-code-walkthrough.html)
- [[OpenMP Code](https://github.com/oneapi-src/oneAPI-samples/tree/master/DirectProgramming/C%2B%2B/StructuredGrids/iso3dfd_omp_offload)] [[DPCPP Code](https://github.com/oneapi-src/oneAPI-samples/tree/master/DirectProgramming/DPC%2B%2B/StructuredGrids/iso3dfd_dpcpp)]
- [波动方程](https://baike.baidu.com/item/%E6%B3%A2%E5%8A%A8%E6%96%B9%E7%A8%8B/1613956)
-  1996 [Distributed three-dimensional finite-difference modeling of wave propagation in acoustic media](https://aip.scitation.org/doi/pdf/10.1063/1.168610)
- [Yet Another Stencil Kernel: A framework for hpc stencil code-generation and tuning.pdf](https://github.com/junxnone/tech-io/files/7509445/yask.pdf)
- [YASK-tutorial.pdf](https://github.com/junxnone/tech-io/files/7509475/YASK-tutorial.pdf)
- [Memory-Level Roofline Analysis in Intel® Advisor](https://www.intel.com/content/www/us/en/developer/articles/technical/memory-level-roofline-model-with-advisor.html)
- [Cache Blocking Techniques](https://www.intel.com/content/www/us/en/developer/articles/technical/cache-blocking-techniques.html)
- [Optimize Memory Access Patterns using Loop Interchange and Cache Blocking Techniques](https://www.intel.com/content/www/us/en/develop/documentation/advisor-cookbook/top/optimize-memory-access-patterns.html)


