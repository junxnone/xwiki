---
Title | OPT Tools Vtune
-- | --
Created @ | `2018-09-28T05:35:41Z`
Updated @| `2023-05-25T12:49:35Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/19)

---
# Intel Vtune
VTune可视化性能分析器（Intel VTune Performance Analyzer）是一个用于分析和优化程序性能的工具，作为Intel为开发者提供的专门针对寻找软硬件性能瓶颈的一款分析工具，它能确定程序的热点（hotspot），找到导致性能不理想的原因，从而让开发者据此对程序进行优化。

- 分析算法选项
- 发现串行或并行代码的瓶颈
- 了解应用如何被硬件资源影响
- 
- VTune性能分析器能通过以下的手段发现和定位程序中的性能问题：
  - 从当前系统中收集性能数据；
  - 从系统到源代码不同的层次上，以不同的互动形式来组织和展示数据；
  - 发现潜在的性能问题，并提出改进措施。
- [Vtune Command Line](/0020_OPT_Tools_Vtune_CommandLine)


## Overview

- **Support Devices** - CPU/GPU/FPGA
- **Where**
  -  Local Host
  - Remote Linux(SSH)
  - Android Device(ADB)
  - Communication Agent(TCP/IP) : 分析实时系统
  - Arbitrary Host (not connected)
- **What**
  - Launch Application : App & Script
  - Attach to Process
  - Profile System : 监控整个系统
  - Launch Android Package
- **How**  
  - Performance Snapshot : 查看 App 的综合情况
  - Algorithm
    - Hotspots
    - Anomaly Detection
    - Memory Consumtion
  - Microarchitecture
    - Microarchitecture Exploration
    - Memory Access
  - Paralleslism
    - Threading
    - HPC Chaeacterization
  - I/O
    - Input and Output
  - Accelerators
    - GPU Offload
    - GPU Compute/Media Hotspots
    - GPU/FPGA Interaction
  - Platform
    - System Overview
    - Platform Profiler


## 注意事项
- 应用编译需要添加 `symbol information @Release mode` 
- 






## Reference
- [VTune](https://software.intel.com/en-us/vtune)
- [Get Started with Intel® VTune™ Profiler](https://www.intel.com/content/www/us/en/docs/vtune-profiler/get-started-guide)
- [User Guide](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2023-1/overview.html)
- [Intel VTune Profiler Performance Analysis Cookbook](https://www.intel.com/content/www/us/en/docs/vtune-profiler/cookbook)
- [CPU Metrics Reference](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2023-0/cpu-metrics-reference.html)
- [Parallel Matrix Multiplication - Code Samples of Intel(R) VTune(TM) Profiler](https://github.com/oneapi-src/oneAPI-samples/tree/master/Tools/VTuneProfiler)
- [性能测试工具VTune的功能和用法介绍](https://blog.csdn.net/WY_stutdy/article/details/79106501)
- [VTune工具的安装与基本使用](https://zzqcn.github.io/perf/intel_vtune/intro.html)
- [Cache line 问题](https://zzqcn.github.io/perf/cpu_cache.html)
- [onapi devcloud 06_Intel_VTune_Profiler](https://jupyter.oneapi.devcloud.intel.com/oneAPI_Essentials/06_Intel_VTune_Profiler)

