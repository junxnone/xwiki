---
Title | OPT LIB OneAPI
-- | --
Created @ | `2021-06-23T06:24:28Z`
Updated @| `2023-02-24T03:23:28Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/76)

---
## OneAPI

- **SYCL** : 主要的编程语言，用于加速器和多处理器编程，可以跨硬件(CPU/GPU/FPGA)编程
- **oneDPL** : `oneAPI DPC++ Library` 实现了一些基本功能函数
  - **Parallel API**: 并行算法实现
  - **SYCL Kernels API**: 
- **oneDNN** : `Deep Neural Network` 高性能实现的深度学习框架
- **oneCCL** : `Collective Communications Library` 服务于深度学习框架的跨硬件通信库
- **Level Zero**: 系统硬件接口
- **oneDAL**: `Data Analytics Library` 数据科学加速算法
- **oneTBB**: `Threading Building Blocks` 基于线程的并行编程库
- **oneVPL**: `Video Processing Library` 视频处理加速库
- **oneMKL**: `Math Kernel Library` 高性能数学库实现
- **Ray Tracing**: 光线追踪库


## Reference

- [OneAPI](https://www.intel.com/content/www/us/en/developer/tools/oneapi/overview.html)
- [OneAPI Specification](https://spec.oneapi.io/versions/1.2-rev-1/) [[repo](https://github.com/oneapi-src/oneAPI-spec)]
- [oneAPI-samples](https://github.com/oneapi-src/oneAPI-samples)




## Install  with Linux

```
wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB
sudo apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB
echo "deb https://apt.repos.intel.com/oneapi all main" | sudo tee /etc/apt/sources.list.d/oneAPI.list
sudo add-apt-repository "deb https://apt.repos.intel.com/oneapi all main"
sudo -E apt install intel-basekit
```


