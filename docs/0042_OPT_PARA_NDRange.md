---
Title | OPT PARA NDRange
-- | --
Created @ | `2021-11-19T01:12:36Z`
Updated @| `2023-03-07T08:34:13Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/42)

---
## Reference
- [One-Dimensional NDRange](https://www.xilinx.com/html_docs/xilinx2017_4/sdaccel_doc/ece1504034297316.html)
- [DPC++ Thread Hierarchy and Mapping](https://www.intel.com/content/www/us/en/develop/documentation/oneapi-gpu-optimization-guide/top/thread-mapping.html)
- [Mapping of oneAPI and DPC++ to CPUs, GPUs, and FPGAs](https://www.intel.com/content/www/us/en/developer/articles/technical/comparing-cpus-gpus-and-fpgas-for-oneapi.html?wapkw=NDRANGE#gs.ivap1r)
- [ND-range data-parallel kernels](https://enccs.github.io/sycl-workshop/expressing-parallelism-nd-range/)

## Brief
- work-group memory - work-items 可以访问同 group 的 memory，不必重新载入
- work-group barriers/fences 同步 work-items
- work-group collectives 通信
- wrok-group 中的 work-items 同时调度进同一个处理单元

![image](https://user-images.githubusercontent.com/2216970/141645331-c69a9cdb-ae77-40c5-83c4-182faaf7c234.png)


Dims | Figure
-- | --
One Dim | ![image](https://user-images.githubusercontent.com/2216970/142524016-84a667ec-7c37-4881-b3c4-c612bd77f963.png)
Two Dim | ![image](https://user-images.githubusercontent.com/2216970/142524708-5f69b20d-2683-4189-b03e-148e054eb95f.png)
Three Dim | ![image](https://user-images.githubusercontent.com/2216970/142524937-881aa871-d0f3-4c53-abd8-7ea59b4b3b49.png)


## NDRange Mapping to Hardware

Devices | Mapping
-- | --
CPU | ![image](https://user-images.githubusercontent.com/2216970/221084720-632452b3-2aff-4441-8f63-25b616a7a7b0.png)
iGPU | ![image](https://user-images.githubusercontent.com/2216970/142132985-86a8e414-1596-4378-9069-d8609d0f329f.png)
FPGA | ![image](https://user-images.githubusercontent.com/2216970/146120629-aef3232d-7d90-4930-96b5-0917e11d195a.png)

