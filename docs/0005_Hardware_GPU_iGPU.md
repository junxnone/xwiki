---
Title | Hardware GPU iGPU
-- | --
Created @ | `2021-11-10T17:21:22Z`
Updated @| `2023-03-14T07:23:20Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/5)

---
## Reference
- [Intel® Processors with Integrated Graphics](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/gen-arch.html)
- [Intel® graphics processor table](https://dgpu-docs.intel.com/devices/hardware-table.html)
- [Install Ubuntu intel-graphics Drivers](https://dgpu-docs.intel.com/index.html)
- [Shared Local Memory](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/kernels/slm.html)
- [DPC++ Thread Hierarchy and Mapping](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/thread-mapping.html)
- [INTEL® GPU Occupancy Calculator](https://oneapi-src.github.io/oneAPI-samples/Tools/GPU-Occupancy-Calculator/index.html)
- [Intel Processor Graphics - Architecture & Programming](https://www.intel.com/content/dam/develop/external/us/en/documents/intel-graphics-architecture-isa-and-microarchitecture-698638.pdf)


## Brief
- Slice/SubSlice/EU/ALU
- GRF - `general-purpose registers`
- [iGPU Tools](/iGPU_Tools)
- [iGPU Issues](/iGPU_Issues)


## Arch

iGPU |  ![image](https://user-images.githubusercontent.com/2216970/141686187-0d20ab0b-2e9b-46c7-87c3-fe7094aa2b41.png)
-- | --

Slice | SubSlice | EU
:--: | :--: | :--:
![image](https://user-images.githubusercontent.com/2216970/141405977-200c4977-23ce-4ebe-8198-f1a81b245054.png) | ![image](https://user-images.githubusercontent.com/2216970/141405952-23e3a489-4f2a-4165-b533-43c6bb7cce87.png) |  ![image](https://user-images.githubusercontent.com/2216970/141405945-dbf2689a-b650-4df2-b808-989fce52a9e1.png)

Generations | Threads per EU | EUs per SubSlice | SubSlices | Total Threads | Total Operations
-- | -- | -- | -- | -- | --
Gen9 (BDW) | 7 | 8 | 3 | 168 | 1344
Intel Iris Xe (Gen11) | 7 | 8 | 8 | 448 | 3584
Intel Iris Xe (Gen12) | 7 | 16 | 6 | 672 | 5376

- 每个 EU 包含两个 ALU
- 每个 ALU 可以执行 4xFP32/8xFP16
- 每个 EU 可以执行 8xFP32
- `Total Threads = SubSlices x EUs x Threads`
- `Total Operations = Total Threads x SIMD Width`

### Subslice & SLM 
- `Instruction Cache`
- `Local Thread Dispatcher`
- `Read-Only Texture/Image Sampler` - 64B/Cycle
- `Dataport` - 64B/Cycle
- SLM  - `Shared Local Memory` - 64KB/Subslice
- 每个 Subslice 执行的 `work-items` = `Eus x Threads x SIMD Width`
- SLM: 是在 Subslice 所有 `work-items` 内共享 `atomic data`
  - 如果 work-group 内包含同步操作, 需要分配在同一个 Subslice
- `work-groups` < 16


### Memory
- CPU & GPU 共享物理内存(zero-copy)
- L1 & L2 Sampler caches
- L3 Cache(64Byte/Cycle)


![image](https://user-images.githubusercontent.com/2216970/142150859-40a9a152-c17f-4e0c-b9ff-0fcb2548dc08.png)

#### Shared Local Memory
- 通过 Global Memory 共享数据和通信效率较低，所以 SLM 出现了
- SLM 的设计目的: 高带宽/低延迟 work-items 之间共享数据
- Read & Write /Cycle = 64 Byte = 16 x 4 Byte
- DPCPP 获取 SLM Info - `q.get_device().get_info<sycl::info::device::local_mem_size>()`
- **Bank Conflicts** [[CUDA SHARED MEMORY - Bank Conflict](https://www.cnblogs.com/1024incn/p/4605502.html)]
  - 依赖于 Device
  - **Bank(Cache line)** - 64 Byte = 16 Bank x 4 Byte(32-bit)
  - 同时访问一个 Bank 的不同地址会引起 `Bank conflicts`, 硬件限制会导致串行访问




### [[NDRange]] Mapping to iGPU
- `work-items` 分配到 operations
- `sub-group` 分配到 threads
- `work-group` 受 hardware 限制 (Iris Xe 每个 subslice 最多 16个，最多 512 个  `work-items`)


![image](https://user-images.githubusercontent.com/2216970/142132985-86a8e414-1596-4378-9069-d8609d0f329f.png) | ![image](https://user-images.githubusercontent.com/2216970/146315451-1dc8b933-7007-4974-8610-868134394e4d.png)
-- | --

Summary | EUs | Threads | Operations | Maximum Work Group Size | Maximum Work Groups
-- | -- | -- | -- | -- | --
Each SubSlice | 16 |  7x16=112 | 112x8=896   | 512 | 16
Total | 16x6=96  |  112x6=672 | 896x6=5376  | 512 |  16x6=96

> Intel® Iris® Xe Graphics (TGL) GPU

> `There are 16 barrier registers per sub-slice, so no more than 16 work-groups can be executed simultaneously.`
> `The amount of shared local memory available per sub-slice (64KB). If for example a work-group requires 32KB of shared local memory, only 2 of those work-groups can run concurrently, regardless of work-group size.`


###  GPU 利用率 (Utilization) 和占用率 (Occupancy)

- Utilization : 时间维度上的统计计算资源
- Occupancy: 空间维度上统计计算资源占用情况


Work-items | Group Size | Threads | SubSlice Utilization | SubSlice Occupancy
-- | -- | -- | -- | --
64x64x128 = 524288    | (R=1) 128 | 16 | 16/112 = 14% | 128 x 7 / 112 x 8 = 100% with 7 work-groups
64x64x128 = 524288    | (R=2) 128 x 2| 2 x 16 | 32/112 = 28.6% | 128 x 2 x 3 / 112 x 8 = 86% with 3 work-groups
64x64x128 = 524288    | (R=3) 128 x 3| 3 x 16 | 48/112 = 42.9% | 128 x 3 x 2 / 112 x  8 = 86% with 2 work-groups
64x64x128 = 524288    | (R=4) 128 x 4| 4 x 16 | 64/112 = 57%  | 128 x4 / 112 x8 = 57% maximum
64x64x128 = 524288    | (R>4) 640+ |   |   | Fail to launch


