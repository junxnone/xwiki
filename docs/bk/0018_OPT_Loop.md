-----

| Title         | OPT Loop                                            |
| ------------- | --------------------------------------------------- |
| Created @     | `2021-12-14T07:42:33Z`                              |
| Last Modify @ | `2022-12-22T03:42:35Z`                              |
| Labels        | \`\`                                                |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/18) |

-----

# Loop

## Reference

  - [HLS Loop
    Optimizations](https://learning.intel.com/developer/learn/course/external/view/elearning/242/hls-loop-optimizations-part-3-of-7)

## Brief

  - Loop Pipelining
  - Loop Unrolling

## Loop Pipelining

| No Loop![image](media/dfecad3465f2365e02375c942c3c7f6a3a77a447.png) | ![image](media/50e605b1c8725f275b4501ce54313eb111877393.png) |
| ------------------------------------------------------------------- | ------------------------------------------------------------ |

## Loop Unrolling

    accum = 0;
    #pragma unroll N
    for (size_t i=0; i<4; i++) {
      accum += data[i];
    }
    sum_out = accum;

| unroll/nounroll | Execution                                                    |
| --------------- | ------------------------------------------------------------ |
| nounroll        | ![image](media/d33c5e28b2faf365849f00bc3ef338c611e73257.png) |
| Unroll 2        | ![image](media/1130b47a4c3fa7beb320ce1c8e08e99076a76586.png) |
| Fully Unroll    | ![image](media/6798e907b5b5d17b173235ee435c409cc1074387.png) |

| Basic Loop                                                   | Unrolled Loop                                                | Pipelined Loop                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![image](media/7693eb40490469501a9324ca6585c01d2f94ede6.png) | ![image](media/3e3748cecb650978d5f0525adf40d9049c27b74b.png) | ![image](media/a243279ed12372f5cf9183ed43b9e9535c69e628.png) |
