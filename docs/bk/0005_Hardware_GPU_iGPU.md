-----

| Title     | Hardware GPU iGPU                                  |
| --------- | -------------------------------------------------- |
| Created @ | `2021-11-10T17:21:22Z`                             |
| Updated @ | `2025-05-29T02:35:59Z`                             |
| Labels    | \`\`                                               |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/5) |

-----

# Intel GPUs - iGPU/dGPU

  - Intel 显卡早期以集成显卡为主
  - 独立显卡
  - 服务器显卡(用于计算)

## 历史

Intel GPU的发展历程丰富，从早期为单板计算机提供显示功能，到如今在集成显卡和独立显卡领域均有布局：

1.  **萌芽探索期（1977 - 1988年）**：1977年，Intel推出首款显示相关芯片C8275
    CRT控制器，用于Intel单板计算机的视频/图形模块，后续还推出其升级版本8276芯片。1982年，授权NEC
    μpd
    7220生产82720芯片，应用于多种设备；同年推出的82730芯片是文本协处理器。1984年的82716芯片是视频存储和显示设备
    。1986年，Intel推出首款离散图形协处理器82786，集成多个功能单元，支持多种功能。
2.  **技术积累期（1989 -
    1999年）**：1989年，Intel推出i860显示控制芯片，为MMX指令打下基础。1998年，Intel与Real3D和Chips
    and
    Technologies公司联合开发i740显卡，虽商业上失败，但为后续集显技术发展积累了经验。1999年，Intel推出i810芯片组，内置i752图形核心，开启集成显卡的发展征程。
3.  **集成显卡发展期（2000 - 2010年）**：2002年，集成“Extreme
    Graphics”的i845G/E芯片组推出，集成显卡性能大幅提升。2004年，随着915GM芯片组到来，Graphics
    Media Accelerator（GMA）系列图形芯片诞生，如GMA 900。2006年，G965芯片组带来GMA
    X3000图形芯片，完整支持DirectX 9.0c。2007年，G35芯片组的GMA
    X3500图形核心增加对DX10的支持。2010年，Clarkdale处理器将HD
    Graphics图形核心与CPU集成在一块芯片上，标志着核心显卡诞生。
4.  **核心显卡拓展期（2011 - 2020年）**：2011年，Sandy Bridge架构处理器集成Intel HD Graphics
    2000/3000，首次支持DirectX 10.1和OpenGL 3.1。2012年，Ivy Bridge架构集成Intel HD
    Graphics 2500/4000 。2013年，Haswell架构集成Intel HD Graphics
    4400/4600等，还推出高端核显Iris Graphics系列。2015年，Broadwell架构集成Intel
    HD Graphics 5500/6000 。2016 - 2019年，Skylake、Kaby Lake、Coffee
    Lake、Comet Lake等架构不断推出新的集成显卡型号，性能和功能持续改进。2020年，Comet Lake
    Refresh架构集成Intel UHD Graphics 730 。
5.  **独立显卡突破期（2021年 - 至今）**：2021年，Intel推出Xe架构，其中Xe -
    LP用于入门独显和核心显卡，并宣布全新高性能显卡品牌“Arc”（锐炫），采用Xe
    - HPG架构。Arc系列独立显卡支持DirectX 12 Ultimate和Vulkan
    1.2等，为用户提供了更多选择，在游戏、创作等领域展现出一定竞争力。此后Intel持续优化和升级Xe架构，推出更多Arc独显和核显产品
    。

## GPU 利用率 (Utilization) 和占用率 (Occupancy)

  - Utilization : 时间维度上的统计计算资源
      - 按时间分片，当前 100 片时间内，如果 GPU 有 50 片在执行任务，则称当前 GPU 利用率 `50%`
  - Occupancy: 空间维度上统计计算资源占用情况

| Work-items         | Group Size    | Threads | SubSlice Utilization | SubSlice Occupancy                             |
| ------------------ | ------------- | ------- | -------------------- | ---------------------------------------------- |
| 64x64x128 = 524288 | (R=1) 128     | 16      | 16/112 = 14%         | 128 x 7 / 112 x 8 = 100% with 7 work-groups    |
| 64x64x128 = 524288 | (R=2) 128 x 2 | 2 x 16  | 32/112 = 28.6%       | 128 x 2 x 3 / 112 x 8 = 86% with 3 work-groups |
| 64x64x128 = 524288 | (R=3) 128 x 3 | 3 x 16  | 48/112 = 42.9%       | 128 x 3 x 2 / 112 x 8 = 86% with 2 work-groups |
| 64x64x128 = 524288 | (R=4) 128 x 4 | 4 x 16  | 64/112 = 57%         | 128 x4 / 112 x8 = 57% maximum                  |
| 64x64x128 = 524288 | (R\>4) 640+   |         |                      | Fail to launch                                 |

| EUs | Max Threads | Max Operations |
| --- | ----------- | -------------- |
| 16  | 7 x16 = 112 | 112 x8 = 896   |

> 7 : Threads/EU  
> 8 : 8-wide Single Instruction Multiple Data (SIMD) Arithmetic Logic
> Units (ALU)

## Reference

  - [Intel® Processors with Integrated
    Graphics](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/gen-arch.html)
  - [Intel® graphics processor
    table](https://dgpu-docs.intel.com/devices/hardware-table.html)
  - [Install Ubuntu intel-graphics
    Drivers](https://dgpu-docs.intel.com/index.html)
  - [Shared Local
    Memory](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/kernels/slm.html)
  - [DPC++ Thread Hierarchy and
    Mapping](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/thread-mapping.html)
  - [INTEL® GPU Occupancy
    Calculator](https://oneapi-src.github.io/oneAPI-samples/Tools/GPU-Occupancy-Calculator/index.html)
  - [Intel Processor Graphics - Architecture &
    Programming](https://www.intel.com/content/dam/develop/external/us/en/documents/intel-graphics-architecture-isa-and-microarchitecture-698638.pdf)
  - [GPU Architecture Terminology for Intel® Xe
    Graphics](https://www.intel.com/content/www/us/en/developer/articles/technical/gpu-terminology-for-intel-xe.html)
  - [Thread Mapping and GPU
    Occupancy](https://www.intel.com/content/www/us/en/docs/oneapi/optimization-guide-gpu/2023-1/thread-mapping-and-gpu-occupancy.html)
