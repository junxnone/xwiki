-----

| Title     | Hardware SIMD 原理                                   |
| --------- | -------------------------------------------------- |
| Created @ | `2021-08-02T02:42:03Z`                             |
| Updated @ | `2023-10-08T02:04:01Z`                             |
| Labels    | \`\`                                               |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/8) |

-----

# SIMD 原理

  - SIMD - `Single Instruction Multiple Data` - 单**指令流**多**数据流**
  - ALU - `arithmetic and logic unit` - 算术逻辑单元

<img width=800 src="https://user-images.githubusercontent.com/2216970/162369549-ca1fb468-98b8-449b-91f8-66afd8cc66f0.png">

## Scalar & SIMD Mode

![image](media/d8005bb1493d64ef46582879906e987e6625c659.png)

## SIMD Arch

<img width=300 src="https://user-images.githubusercontent.com/2216970/127798065-e41ca06b-46db-4833-ba38-a2f7723ed21a.png">

## Pipeline

![128](media/d5824668ebec4f8f3d5fbbe35ba4ddcf4d2a8feb.gif)

![avx2](media/4d488109117cbff4f1c9546ef288db79ad6ce28c.gif)

![avx512](media/9dad4613bfb0412ca947629ce6dc9e49898b4d47.gif)

## Reference

  - [SIMD简介](https://zhuanlan.zhihu.com/p/55327037)
  - [Basics of SIMD
    Programming](http://ftp.cvut.cz/kernel/people/geoff/cell/ps3-linux-docs/CellProgrammingTutorial/BasicsOfSIMDProgramming.html)
