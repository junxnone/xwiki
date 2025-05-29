---
Title | Hardware GPU iGPU
-- | --
Created @ | `2021-11-10T17:21:22Z`
Updated @| `2025-05-29T02:30:42Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/5)

---
# Intel GPUs - iGPU/dGPU

- Intel 显卡早期以集成显卡为主
- 独立显卡
- 服务器显卡(用于计算)


##  GPU 利用率 (Utilization) 和占用率 (Occupancy)

- Utilization : 时间维度上的统计计算资源
  - 按时间分片，当前 100 片时间内，如果 GPU 有 50 片在执行任务，则称当前 GPU 利用率 `50%` 
- Occupancy: 空间维度上统计计算资源占用情况


Work-items | Group Size | Threads | SubSlice Utilization | SubSlice Occupancy
-- | -- | -- | -- | --
64x64x128 = 524288    | (R=1) 128 | 16 | 16/112 = 14% | 128 x 7 / 112 x 8 = 100% with 7 work-groups
64x64x128 = 524288    | (R=2) 128 x 2| 2 x 16 | 32/112 = 28.6% | 128 x 2 x 3 / 112 x 8 = 86% with 3 work-groups
64x64x128 = 524288    | (R=3) 128 x 3| 3 x 16 | 48/112 = 42.9% | 128 x 3 x 2 / 112 x  8 = 86% with 2 work-groups
64x64x128 = 524288    | (R=4) 128 x 4| 4 x 16 | 64/112 = 57%  | 128 x4 / 112 x8 = 57% maximum
64x64x128 = 524288    | (R>4) 640+ |   |   | Fail to launch


EUs | Max Threads | Max Operations
-- | -- | --
16 | 7 x16 = 112 | 112 x8 = 896

> 7 : Threads/EU  
> 8 : 8-wide Single Instruction Multiple Data (SIMD) Arithmetic Logic Units (ALU) 


## Reference
- [Intel® Processors with Integrated Graphics](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/gen-arch.html)
- [Intel® graphics processor table](https://dgpu-docs.intel.com/devices/hardware-table.html)
- [Install Ubuntu intel-graphics Drivers](https://dgpu-docs.intel.com/index.html)
- [Shared Local Memory](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/kernels/slm.html)
- [DPC++ Thread Hierarchy and Mapping](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/thread-mapping.html)
- [INTEL® GPU Occupancy Calculator](https://oneapi-src.github.io/oneAPI-samples/Tools/GPU-Occupancy-Calculator/index.html)
- [Intel Processor Graphics - Architecture & Programming](https://www.intel.com/content/dam/develop/external/us/en/documents/intel-graphics-architecture-isa-and-microarchitecture-698638.pdf)
- [GPU Architecture Terminology for Intel® Xe Graphics](https://www.intel.com/content/www/us/en/developer/articles/technical/gpu-terminology-for-intel-xe.html)
- [Thread Mapping and GPU Occupancy](https://www.intel.com/content/www/us/en/docs/oneapi/optimization-guide-gpu/2023-1/thread-mapping-and-gpu-occupancy.html)

