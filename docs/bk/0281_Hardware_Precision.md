-----

| Title     | Hardware Precision                                   |
| --------- | ---------------------------------------------------- |
| Created @ | `2023-07-14T08:35:15Z`                               |
| Updated @ | `2023-07-14T08:45:17Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/281) |

-----

# Precision

  - FP32
  - FP16
  - BF16
  - FP64
  - FP80
  - TF32

## FP32

  - `float`
  - `tf.float32`
  - `torch.float32`/`torch.float`

![image](media/50d3a5266328a6bacb9691715a944b587dbffc3c.png)

## TF32

  - `tensor float 32`
  - CUDA 用于提升 FLOPS

![image](media/a784a6848a38ce61170564dbf8cc4103278e0d87.png)

![image](media/d4805c6ed12b2ac9cc9ab8c13640b30e9c40b521.png)

## FP16

  - `short float`
  - `tf.float16`
  - `torch.float16` / `torch.half`

![image](media/9bf3c2a00df34044e84bf1c681d7a5d4dc5b8951.png)

## BF16

  - `tf.bfloat16`
  - `torch.bfloat16`

![image](media/4d514691647a34ca0d3793a683fd68399ef1bc0f.png)

### bf16 vs fp16 vs fp32

![image](media/6d79e5249c65cb3d603636805d4a11369555b6bb.png)

## FP64

  - `double`
  - `tf.float64`
  - `torch.float64` / `torch.double`

![image](media/9eccae3d742ddd41ad79cc342544ccab88b79749.png)

## FP80

  - `long double`

![image](media/3588c626cf8c8ffc25ad47ea30f05df35f070242.png)
