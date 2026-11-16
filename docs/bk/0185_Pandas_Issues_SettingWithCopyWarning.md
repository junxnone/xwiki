-----

| Title     | Pandas Issues SettingWithCopyWarning                 |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-08-14T10:33:31Z`                               |
| Updated @ | `2026-11-16T09:39:54Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/185) |

-----

# SettingWithCopyWarning

## Error Log

    SettingWithCopyWarning: A value is trying to be set on a copy of a slice from a DataFrame

  - 操作可能没有按预期运行，需要检查结果以确保没有出错。

## Reproduce

``` python
df = pd.DataFrame({'a': [1, 2, 3], 'b': [4, 5, 6]})
sub = df[df.a > 1]      # 可能是副本，也可能是视图
sub['b'] = 0            # 触发 SettingWithCopyWarning，df 不会被修改
```

  - 链式赋值 `df[df.a > 1]['b'] = 0` 同样会触发，且**不会**修改 `df`

## Solution

  - 如果要更改原始数据，使用单一赋值操作（loc）

<!-- end list -->

``` python
df.loc[df.a > 1, 'b'] = 0
```

  - 如果想要一个副本，确保强制让 Pandas 创建副本 `.copy()`

<!-- end list -->

``` python
sub = df[df.a > 1].copy()
sub['b'] = 0
```

  - 关闭警告的设置方法（不推荐，只是隐藏问题）: `pd.set_option('mode.chained_assignment',
    None)`

## Details

Pandas 中的某些操作会返回数据的视图（View），某些操作会返回数据的副本（Copy），且返回哪种取决于底层内存布局，难以预测。因此
Pandas 无法确定链式赋值是否作用于原数据，只能给出警告。

> Pandas 3.0 起默认启用 Copy-on-Write，链式赋值永远不会修改原对象，该警告将被移除。

## Reference

  - [Pandas 中 SettingwithCopyWarning
    的原理和解决方案](https://www.jianshu.com/p/72274ccb647a)
  - [Returning a view versus a
    copy](https://pandas.pydata.org/docs/user_guide/indexing.html#returning-a-view-versus-a-copy)
  - [Copy-on-Write](https://pandas.pydata.org/docs/user_guide/copy_on_write.html)
