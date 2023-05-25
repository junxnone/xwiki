---
Title | OPT Tools Vtune iGPU
-- | --
Created @ | `2023-05-25T13:19:54Z`
Updated @| `2023-05-25T13:32:24Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/245)

---
# Intel Vtune iGPU Analysis

## Setup
- Intel Metric Discovery API Library
  - Windows 集成在 Drivers 里面
  - [Linux Install](https://github.com/intel/metrics-discovery)
- Enable Permissions
- Enable GPU utilization events (i915 ftrace events)


## Reference
- [Set Up System for GPU Analysis](https://www.intel.com/content/www/us/en/docs/vtune-profiler/user-guide/2023-0/set-up-system-for-gpu-analysis.html)
- [oneAPI GPU Optimization Guide](https://www.intel.com/content/www/us/en/docs/oneapi/optimization-guide-gpu/2023-0/overview.html)
- [Using the Command-Line Interface to Analyze the Performance of a SYCL* Application running on a GPU](https://www.intel.com/content/www/us/en/docs/vtune-profiler/cookbook/2023-1/profiling-gpu-from-cli.html)
