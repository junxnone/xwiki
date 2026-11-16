-----

| Title     | Pandas UseCase IO                                    |
| --------- | ---------------------------------------------------- |
| Created @ | `2019-08-15T11:23:03Z`                               |
| Updated @ | `2026-11-16T09:39:59Z`                               |
| Labels    | \`\`                                                 |
| Edit @    | [here](https://github.com/junxnone/xwiki/issues/188) |

-----

# Format Output 读写文件

  - Numpy
  - Markdown
  - CSV
  - H5
  - xlsx
  - json / pickle

## 格式转换

### 转 numpy

    df.to_numpy()

### 转 Markdown

    df.to_markdown()

> 依赖 `tabulate`：`pip install tabulate`

### 转 dict / list

    df.to_dict()                  # {列: {index: 值}}
    df.to_dict(orient='records')  # [{列: 值}, ...]
    df.values.tolist()            # [[...], [...]]

## 读写文件

### csv

    pd.read_csv('foo.csv')
    df.to_csv('foo.csv')

  - 保存为无 `index` 的 `csv`

<!-- end list -->

    df.to_csv('csv_name.csv', index=False)

  - 常用读取参数

<!-- end list -->

    pd.read_csv('foo.csv', sep=',', header=None, names=['a','b'], usecols=['a'], nrows=100, encoding='utf-8')

### h5

    pd.read_hdf('foo.h5', 'df')
    df.to_hdf('foo.h5', key='df')

> 依赖 `tables`：`pip install tables`

### xlsx

    pd.read_excel('foo.xlsx', 'Sheet1', index_col=None, na_values=['NA'])
    df.to_excel('foo.xlsx', sheet_name='Sheet1')

> 依赖 `openpyxl`：`pip install openpyxl`

  - 写入多个 sheet

<!-- end list -->

    with pd.ExcelWriter('foo.xlsx') as writer:
        df1.to_excel(writer, sheet_name='Sheet1')
        df2.to_excel(writer, sheet_name='Sheet2')

### json / pickle

    df.to_json('foo.json'); pd.read_json('foo.json')
    df.to_pickle('foo.pkl'); pd.read_pickle('foo.pkl')

> `list` 等 Python 对象存 csv 会变字符串，见 [csv list 变
> str](/0213_Pandas_Issues_csvliststr)

## Reference

  - [IO tools](https://pandas.pydata.org/docs/user_guide/io.html)
