-----

| Title         | Hardware SIMD AVX                                  |
| ------------- | -------------------------------------------------- |
| Created @     | `2021-08-02T02:31:09Z`                             |
| Last Modify @ | `2022-12-22T03:23:22Z`                             |
| Labels        | \`\`                                               |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/9) |

-----

## Reference

  - [AVX512 Intrinsic
    instructions](https://software.intel.com/sites/landingpage/IntrinsicsGuide/#techs=AVX_512)
  - [Intel
    AVX-512简介](https://github.com/zenny-chen/Intel-AVX512-Brief-Introduction)
  - [Ref docs
    Compilers](https://software.intel.com/content/www/us/en/develop/documentation/cpp-compiler-developer-guide-and-reference/top/compiler-reference/intrinsics/details-about-intrinsics.html)
  - [使用 AVX 系列指令集进行向量化](https://enigmahuang.me/2017/09/29/AVX-SIMD/)
  - [AVX / AVX2 Intrinsics Example
    Code](https://github.com/chen0031/AVX-AVX2-Example-Code)
  - [Intel
    内部指令---AVX编程基础](https://blog.csdn.net/chen134225/article/details/105935153)

## Brief

  - AVX512 - `Advanced Vector Extensions` - 512Bit SIMD - `AVX/AVX2` 的扩展
  - 加速批量数据运算
  - 32个SIMD寄存器(128/256/512Bit)
  - [AVX Code Compile](/AVX_Code_Compile)

## 内建函数

### 函数命名解析

    _mm<bit_width>_<func_name>_<data_type>

  - **bit\_width** - 128/256/512 `空为128`
  - **func\_name** - 实现内容
  - **data\_type** 向量类型
      - **ps** - float
      - **pd** - double
      - **epi8/epi16/epi32/epi64** - 有符号整数
      - **epu8/epu16/epu32/epu64** - 无符号整数
      - **si128/si256/si512** 未指定类型
  - **I/O Data Type**
      - **\_\_m64** `4x16bit/2x32bit/1x64bit`
      - **\_\_m128/\_\_m256/\_\_m512** - `4/8/16 个 32bit float`
      - **\_\_m128d/\_\_m256d/\_\_m512d** - `2/4/8 个 32bit double`
      - **\_\_m128i/\_\_m256i/\_\_m512i** - `Nx char/short/int/long`
      - **\_\_m128h/\_\_m256h/\_m512h** ???

### 函数类型

#### 初始化类

| Name   | Sub             | Description                                       |
| ------ | --------------- | ------------------------------------------------- |
| set    | `_setzero_`     | 创建 /s/d/sixxx 类型的 vector                          |
| \--    | `_set1_xx(k)`   | 创建 xxx 类型的 vector 并全部设置为值 k                       |
| \--    | `_set_xx(K[])`  | 创建 xxx 类型的 vector 并依次设置为值 `K[ xn, xn-1, ..., x1]` |
| \--    | `_setr_xx(K[])` | 创建 xxx 类型的 vector 并依次设置为值 `K[ x1, x2, ..., xn]`   |
| load   | `_load_`        | 从内存加载变量(需对齐)                                      |
| \--    | `_loadu_`       | 从内存加载变量(不需对齐)                                     |
| \--    | `_maskload_`    | 根据掩码加载部分变量 `mask 最高Bit 为 1 时加载`                   |
| store  | `_store_`       | 存储变量到内存                                           |
| \--    | `_storeu_`      |                                                   |
| \--    | `_mask_storeu_` |                                                   |
| stream | `_stream_`      |                                                   |
| \--    | `_stream_load_` |                                                   |

#### 算术/Arithmetic

| Name   | Sub                 | Description                                                                                                                                         |
| ------ | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| add    | `_add_`             | 相加                                                                                                                                                  |
| \--    | `_adds_`            | 饱和相加 如果超过最大值，则等于最大值                                                                                                                                 |
| \--    | `_hadd_`            | 水平相加<br> ` 256double:  ` <br>$c\_0=a\_0+a\_1$ <br>$c\_1 = b\_0 + b\_1$ <br>$c\_2 = a\_2 + a\_3$ <br>$c\_3 = b\_2 + b\_3$                            |
| \--    | `_hadds_`           | 同 `_hadd_` - 但是饱和相加                                                                                                                                 |
| sub    | `_sub_`             | 相减                                                                                                                                                  |
| \--    | `_subs_`            | 饱和相减 如果小于最小值, 则等于最小值                                                                                                                                |
| \--    | `_hsub_`            | 水平相减<br> ` 256double:  ` <br>$c\_0=a\_0 - a\_1$ <br>$c\_1 = b\_0 - b\_1$ <br>$c\_2 = a\_2 - a\_3$ <br>$c\_3 = b\_2 - b\_3$                          |
| \--    | `_hsubs_`           | 同 `_hsub_` 但是饱和相减                                                                                                                                   |
| \--    | `_mask_subs_`       |                                                                                                                                                     |
| \--    | `_maskz_subs_`      |                                                                                                                                                     |
| \--    | `_sub_round_`       |                                                                                                                                                     |
| \--    | `_mask_sub_round_`  |                                                                                                                                                     |
| \--    | `_maskz_sub_round_` |                                                                                                                                                     |
| addsub | `_addsub_`          | 间或加减 ` 256double:  ` <br>$c\_0=a\_0 - b\_0$ <br>$c\_1 = a\_1 + b\_1$ <br>$c\_2 = a\_2 - b\_2$ <br>$c\_3 = a\_3 + b\_3$                              |
| mul    | `_mul_`             | 相乘                                                                                                                                                  |
| \--    | `_mullo_`           | 相乘 `32Bit x 32Bit = 64 Bit` , 取\[0:31\]                                                                                                             |
| \--    | `_mulhi_`           | 相乘 `16Bit x 16Bit = 32 Bit` , 取\[16:31\]                                                                                                            |
| \--    | `_mulhrs_`          | 相乘 `16Bit x 16Bit --> 右移 14位 --> + 1` 取 \[1:16\]                                                                                                    |
| div    | `_div_`             | 相除                                                                                                                                                  |
| fm     | `_fmadd_`           | `axb+c`                                                                                                                                             |
| \--    | `_fmsub_`           | `axb-c`                                                                                                                                             |
| \--    | `_fnmadd_`          | `-(axb)-c`                                                                                                                                          |
| \--    | `_fnmsub_`          | `-(axb)-c`                                                                                                                                          |
| \--    | `_fmaddsub_`        | 间或乘加减 ` 256double:  ` <br>$r\_0=a\_0 x b\_0 - c\_0$ <br>$r\_1 = a\_1 x b\_1 + c\_1$ <br>$r\_2 = a\_2 x b\_2 - c\_2$ <br>$r\_3 = a\_3 x b\_3 + c\_3$ |
| \--    | `_fmsubadd_`        | 间或乘加减 ` 256double:  ` <br>$r\_0=a\_0 x b\_0 + c\_0$ <br>$r\_1 = a\_1 x b\_1 - c\_1$ <br>$r\_2 = a\_2 x b\_2 + c\_2$ <br>$r\_3 = a\_3 x b\_3 - c\_3$ |

#### Permuting and Shuffling

| Name    | Sub                | Description                                                                                                                                                               |
| ------- | ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| permute | `_permute_`        | $r\_0=m\_0? a\_1:a\_0 $ $r\_1 = m\_1? a\_1:a\_0$                                                                                                                          |
| \--     | `_permute4x64_`    | $r\_t = \\begin{cases} a\_0 & \\text{ if } m\_t= b'00 \\ a\_1 & \\text{ if } m\_t= b'01 \\ a\_2 & \\text{ if } m\_t= b'10\\ a\_3 & \\text{ if } m\_t= b'11 \\end{cases} $ |
| \--     | `_permute2f128_`   |                                                                                                                                                                           |
| \--     | `_permutevar_`     |                                                                                                                                                                           |
| \--     | `_permutevar8x32_` |                                                                                                                                                                           |
| shuffle | `_shuffle_`        | $r\_0 = m\_0,?, a\_0:a\_1$<br>$r\_1 = m\_1,?,b\_0:b\_1$ <br>$r\_2 = m\_2,?,a\_2:a\_3$<br> $r\_3 = m\_3,?,b\_2:b\_3$                                                       |
| \--     | `_shufflehi_`      |                                                                                                                                                                           |
| \--     | `_shufflelo_`      |                                                                                                                                                                           |

#### Others

| Name         | sub                    | Description                                                                                       |
| ------------ | ---------------------- | ------------------------------------------------------------------------------------------------- |
| zext         | `_zextxx_xx`           | 转换 type (\_\_m256 到 \_\_m512)                                                                     |
| xor          | `_xor_xx`              | Bitwise XOR                                                                                       |
| \--          | `_mask_xor_xx`         | mask 为 0 的部分 使用 src 相应值                                                                           |
| \--          | `_maskz_xor_xx`        | mask 为 0 的部分 设为 0                                                                                 |
| unpacklo     | `_unpacklo_`           | a\[512\] b\[512\] --\> \[a\[31:0\],b\[31:0\],a\[63:32\],b\[63:32\],a\[159:128\],b\[159:128\]...\] |
| \--          | `_mask_unpacklo_`      |                                                                                                   |
| \--          | `_maskz_unpacklo_`     |                                                                                                   |
| unpackhi     | `_unpackhi_`           |                                                                                                   |
| \--          | `_mask_unpackhi_`      |                                                                                                   |
| \--          | `_maskz_unpackhi_`     |                                                                                                   |
| undefinec    | `_undefined_`          | 返回未定义的元素                                                                                          |
| test         | `_test_`               |                                                                                                   |
| \--          | `_mask_test_`          |                                                                                                   |
| \--          | `_testn_`              |                                                                                                   |
| \--          | `mask_testn_`          |                                                                                                   |
| ternarylogic | `_ternarylogic_`       |                                                                                                   |
| \--          | `_mask_ternarylogic_`  |                                                                                                   |
| \--          | `_maskz_ternarylogic_` |                                                                                                   |
| srl          | `_srl_`                |                                                                                                   |
| \--          | `_mask_srl_`           |                                                                                                   |
| \--          | `_maskz_srl_`          |                                                                                                   |
| srli         | `_srli_`               |                                                                                                   |
| \--          | `_mask_srli_`          |                                                                                                   |
| \--          | `_maskz_srli_`         |                                                                                                   |
| srlv         | `_srlv_`               |                                                                                                   |
| \--          | `mask_srlv_`           |                                                                                                   |
| \--          | `maskz_srlv_`          |                                                                                                   |
| sra          | `_sra_`                |                                                                                                   |
| \--          | `_mask_sra_`           |                                                                                                   |
| \--          | `_maskz_sra_`          |                                                                                                   |
| srai         | `_srai_`               |                                                                                                   |
| \--          | `_mask_srai_`          |                                                                                                   |
| \--          | `_maskz_srai_`         |                                                                                                   |
| srav         | `_srav_`               |                                                                                                   |
| \--          | `_mask_srav_`          |                                                                                                   |
| \--          | `_maskz_srav_`         |                                                                                                   |
| sqrt         |                        |                                                                                                   |
| sll          |                        |                                                                                                   |
| shldi        |                        |                                                                                                   |
| shldv        |                        |                                                                                                   |
| shrdi        |                        |                                                                                                   |
| shrdv        |                        |                                                                                                   |

### 寄存器

  - SSE 128Bit `XMM0-XMM31`
  - AVX 256Bit `YMM0-YMM31`
  - AVX-512 512Bit`ZMM0-ZMM31`

<img height=500 src="https://user-images.githubusercontent.com/2216970/162350293-92addcc3-496f-4cd1-b35c-69df4469084a.png">

## UseCase
