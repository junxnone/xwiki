-----

| Title         | Programing Python Slice                             |
| ------------- | --------------------------------------------------- |
| Created @     | `2019-05-14T14:34:29Z`                              |
| Last Modify @ | `2022-12-22T06:31:15Z`                              |
| Labels        | \`\`                                                |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/86) |

-----

## Reference

  - [python切片操作](https://www.cnblogs.com/mzct123/p/6031092.html)
  - [Understanding slice
    notation](https://stackoverflow.com/questions/509211/understanding-slice-notation)

## Brief

  - slice 切片

| Pattern                               | Description                                    | UseCase       |
| ------------------------------------- | ---------------------------------------------- | ------------- |
| **seq**\[`s_index`:`e_index`\]        | 从 `s_index` 到 `e_index -1` 的切片                 | `s  == s[:]`  |
| **seq**\[`s_index`:`e_index`:`step`\] | 从 `s_index` 到 `e_index -1` 的切片, 每隔 `step` 取一次值 | `s[-2:-6:-1]` |

## UseCase

| UseCase         | Example                                                                                             | Description                         |
| --------------- | --------------------------------------------------------------------------------------------------- | ----------------------------------- |
| 多维(矩阵)          | `a[1:2, 2:3]`                                                                                       | 取第一维的`[2-3)`和第二维的`[3-5)`            |
| 翻转字符串 `::`      | `a[::-1]` == `a[-1:-len(a)-1:-1]`                                                                   | `s_index` & `e_index` 不指定 `step=-1` |
| 省略号 `…`         | `a[:, :, None]` == `a[…, None]`                                                                     | 省略其他维度                              |
| Image BGR-\>RGB | channels first `img = img[::-1, ...]` <br>channles last `img = img[..., ::-1]` == `img[:, :, ::-1]` |                                     |

    s[-2:-6:-1]

![image](media/93ec83103e44db9d28792583ce0714060b6057d2.png)
![image](media/879104e4c1d0db055e07ab3d7dbdd39df8900f7b.png)

> 不包括ending\_index
