---
Title | Hardware CPU Cache
-- | --
Created @ | `2022-04-25T03:29:21Z`
Updated @| `2024-04-01T06:17:54Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/16)

---
# Cache Memory
- Cache - 高速缓冲存储器
  - 更快的读写数据, 可以缓冲 DRAM 读写速度较慢和 CPU 计算较快的速度差距
  - **时间局部性:** 一个数据如果当前被使用到，那么接下去一段时间它很可能被再次用到
  - **空间局部性:** 一个数据如果当前被使用到，那么接下去一段时间它周围的数据很可能也会被用到
- Data Block: 主存和Cache 会被分割成一定大小块, 相互映射读写
  - 直接映射/`Direct Mapped`
  - 组相联/`Set Associative`
  - 全相联/`Fully Associative`
- Cache Line: 主存中的 Data Block 映射到 Cache 中
- 除了 CPU 和 DRAM 之间的 Cache 外，还有其他一些 Cache[Table Lookup Buffer/Reorder Buffer/Memory Ordering Buffer]



## Cache Arch
- 多级 Cache:
  - 每个 Core 都会有自己的 `L1 Cache` & `L2 Cache`
  - 不同的 Core 共享 `L3 Cache`


![image](https://user-images.githubusercontent.com/2216970/165016896-a476cb9a-2cc7-4d4e-b1bc-289951c5e79f.png)
![image](https://user-images.githubusercontent.com/2216970/165035159-bbf5b607-aa0d-40ad-b15b-35a3c31ed91e.png)



### Intel Tiger Lake Cache
- DCU: L1 Data Cache
- IFU: L1 Instruction Cache
- MLC: L2 Mid Level Cache
- LLC: L3 Last Level Cache
- L1/L2 每个核独立, L3 多核共享

![image](https://user-images.githubusercontent.com/2216970/165446774-2a1238e2-a2b3-4611-b3f0-0773fe19a452.png)

### 映射方式
- 直接映射/`Direct Mapped`:  每个主存 Block 只能映射到特定 `Cache Line`
- 组相联/`Set Associative`: Cache 分组 主存 Block 映射到组
- 全相联/`Fully Associative` : 可以放在任何位置

<img width=500 src="https://user-images.githubusercontent.com/2216970/165017679-58109c88-1645-4171-9ca1-4e6fa9028f57.png">

映射方式 | Example | 优缺点
-- | -- | --
全相联 | `Memory Block 12` 可以映射到 `Cache Block 0~7` | 电路复制/速度慢/不存在冲突缺失/命中率高
直接映射 |  `Memory Block 12` 可以映射到 `Cache Block 4` (12 MOD 8) | 电路实现简单/命中时间短/空间利用率低/命中率低
组相联 | `Memory Block 12` 可以映射到 `Set 0` (12 MOD 4) | 电路较简单/速度较快/命中率较高

> MOD - 取余

## Cache Line
- TGL Cache Line: 64 Byte
- Cache Line 状态(MESI)
  - Modified: 只被缓存在当前 CPU, 被修改过, 写回主存后变为 `Exclusive` 状态
  - Exclusive: 只被缓存在当前 CPU, 未被修改
  - Shared: 被多个 CPU 缓存, 当一个缓存修改, 其他缓存 Invalid
  - Invalid: 无效缓存

![image](https://user-images.githubusercontent.com/2216970/165450175-d30308d8-4f13-48bb-bb68-eb3551d2182a.png)

## Cache Hit/Miss

- CPU 读写数据时，如果数据在 Cache 中 称为 `Cache Hit`, 否则称为 `Cache Miss`
- 命中率高会增加程序性能，减少 CPU 等待空闲时间，减少 DRAM 读取，降低功耗

## Reference
- [计算机体系结构(Spring 2021)](http://staff.ustc.edu.cn/~xhzhou/CA-Spring2021/CA.html)  [[chapter04-01.pdf](https://github.com/junxnone/linuxwiki/files/8551388/chapter04-01.pdf)]
- [计算机体系结构-Cache高速缓存](https://zhuanlan.zhihu.com/p/482651908)
- [Cache地址映射与计算方式](https://www.cnblogs.com/AD-milk/p/13225494.html)
- [一文搞懂cpu cache工作原理](https://zhuanlan.zhihu.com/p/593016449)

