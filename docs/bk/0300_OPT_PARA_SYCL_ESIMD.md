-----

| Title     | OPT PARA SYCL ESIMD                                  |
| --------- | ---------------------------------------------------- |
| Created @ | `2024-01-15T14:47:08Z`                               |
| Updated @ | `2024-01-15T14:47:08Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/300) |

-----

# ESIMD

  - ESIMD - `Explicit SIMD` SYCL extension
  - 用于 Intel GPUs 的高效底层编程扩展，用于编写显示向量化代码
  - APIs - `loads/stores/gathres/scatters/ explicit cache hints/ gpu
    inline assembly`
  - `相当于 SYCL subgroup size=1`

## API

  - SIMD Vector
  - simd\_view
  - Reduction func
  - Memory Access
      - SLM
      - Atomics
  - Math
  - Dot Product Accumulate Systolic - DPAS

-----

  - 哪些可以直接 `Run on Host Device` ?

## Reference

  - [Explicit SIMD Programming Extension for
    DPC++](https://github.com/intel/llvm/blob/sycl/sycl/doc/extensions/supported/sycl_ext_intel_esimd/sycl_ext_intel_esimd.md)
  - [ESIMD
    API](https://intel.github.io/llvm-docs/doxygen/group__sycl__esimd.html)
  - [examples](https://github.com/intel/llvm/blob/sycl/sycl/doc/extensions/supported/sycl_ext_intel_esimd/examples/README.md)
  -
