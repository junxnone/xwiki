---
Title | OPT PARA DPCPP Arch
-- | --
Created @ | `2023-03-07T03:55:03Z`
Updated @| `2023-03-07T03:55:03Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/216)

---
# 架构及相关概念

## 架构


## 相关概念

### Device
- CPU/GPU/FPGA/Accelerator
- kernel 运行的设备
- 可以通过相关 APIs 获取 Name/Vendor/Version/...
- **Device Selector** 用于选取 kernel 运行的设备

### Queue
- 用于异构执行任务的机制
- 每个 queue 映射到一个 Device
- 多个 queue 可以映射到同一个 Device

### Kernel
- 用于执行的数据并行代码
- 在 kernel 被调度时构建
- Kernel 中 使用 C++  有限制
- `range` 用来描述迭代空间
- `id` 用来索引执行实例
- `item` 可以获取 id & range
- 并行 Kernel
  - for-loop 基本并行 Kernel
  - ND-Range


### USM Unified Shared Memory
- 需要硬件支持 `统一虚拟地址空间`
- 三种分配方式
  - Host - Host 分配, Host & Device 都可以访问
  - Device - Device 分配，只能 Device  访问
  - Shared - 编译器管理

