-----

| Title         | Pandas UseCase condition                             |
| ------------- | ---------------------------------------------------- |
| Created @     | `2022-12-22T09:31:37Z`                               |
| Last Modify @ | `2022-12-22T09:31:37Z`                               |
| Labels        | \`\`                                                 |
| Edit @        | [here](https://github.com/junxnone/xwiki/issues/201) |

-----

# 条件操作

## 按条件选择

    df[df.coef> 1]  -> 'coef' 值大于1 的行
    df[df.coef.isin([2])] 'coef 是 2的行
    df[df.coef.isin([1, 2, 3])] 'coef 是 1, 2, 3的行

## 包含字符串的值

    df.name.str.contains('abc')
    df.name.str.contains('abc|abd')

## 某个取值范围 (min, max)

    df[(df.area > min) & (df.area < max)]

## 多重条件选择

  - | for or
  - & for and
  - \~ for not

<!-- end list -->

    df[(df.coef> 1) & (df.coef<3)]  -> 'coef' 值大于1 小于3 的行
