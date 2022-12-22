---
Title | X BLAS
-- | --
Created @ | `2021-08-03T02:53:39Z`
Last Modify @| `2022-12-22T08:11:06Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/179)

---
## Reference
- [BLAS reference dos](http://www.netlib.org/blas/)
- [BLAS 命名规则 - MKL](https://software.intel.com/content/www/us/en/develop/documentation/onemkl-developer-reference-c/top/blas-and-sparse-blas-routines/blas-routines/naming-conventions-for-blas-routines.html)   <sup>[中译](https://zhuanlan.zhihu.com/p/378623025)</sup>

## Brief
- BLAS - `Basic Linear Algebra Subprograms`
- 一系列基本线性代数运算函数接口
- 最早使用 Fortran 编写
- 包含内容
  - Level 1 向量与向量
  - Level 2 向量与矩阵
  - Level 3 矩阵与矩阵

## 其他版本 BLAS

Name | Vendor | 应用
-- | -- | --
[Intel MKl](https://software.intel.com/content/www/us/en/develop/documentation/onemkl-developer-reference-c/top/blas-and-sparse-blas-routines.html)  | Intel | Matlab
[OpenBLAS](https://www.openblas.net/) | **OpenSource** | Octave
[ATLAS2](https://sourceforge.net/projects/math-atlas/) | **OpenSource**
[AMD-ACML] | AMD
[cuBLAS] | NVIDIA
[Accelerate] | Apple
[Arm Performance Libraries] | Arm


## Function
```
<character><name><mod>()
```
> example.
>  - ddot - double 类型向量点乘
>  - cdotc - 复数共轭向量点乘
>  - dgemm - double  矩阵相乘

character | Description
-- | --
**s** | float 实数
**d** | double 实数
**c**  | float 复数
**z** | double 复数


name | Level |Description
-- | -- | -- 
**rot** | L1 | rotation
**swap**  | L1 | 
**scal**  | L1 | 
**copy**  | L1 | 
**axpy**  | L1 | 
**dot**  | L1 | 
**dsdot**  | L1 | 
**nrm2**  | L1 | 
**cnrm2**  | L1 | 
**asum**  | L1 | 
**amax**  | L1 | 
**ge**  | L2 & L3 | 
**gb**  | L2 & L3 | 
**sy**  | L2 & L3 | 
**sp**  | L2 & L3 | 
**sb**  | L2 & L3 | 
**he**  | L2 & L3 | 
**hb**  | L2 & L3 | 
**tr**  | L2 & L3 | 三角矩阵
**tp**  | L2 & L3 |  压缩三角矩阵
**tb**  | L2 & L3 | 

> In BLAS level 1, <name> indicates the operation type
> In BLAS level 2 and 3, <name> reflects the matrix argument type


mod | Level | Description
-- | -- | --
**c** | L1 | 
**u** | L1 |
**g** | L1 |
**m** | L1 |
**mg** | L1 |
**mv** | L2 |
**sv** | L2 |
**r** | L2 |
**r2** | L2 |
**mm** | L3 |
**sm** | L3 |
**rk** | L3 |
**r2k** | L3 |

## UseCase

