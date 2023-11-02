---
Title | Programing Python datetime
-- | --
Created @ | `2019-11-02T09:33:27Z`
Updated @| `2023-11-02T06:35:14Z`
Labels | ``
Edit @| [here](https://github.com/junxnone/xwiki/issues/212)

---
# datetime


## 获取时间

```
import datetime
print(datetime.datetime.now())
```
```
2022-12-28 13:17:17.400825
```

### 格式化输出

```
date_time = datetime.datetime.now.strftime("%m/%d/%Y, %H:%M:%S")
```


## 获取不同时区的时间

### 通过 `pytz` 设置时区

```
import pytz
import datetime
tz = pytz.timezone('Asia/Shanghai')

datetime.datetime.now(tz).strftime("%Y-%m-%d %H:%M:%S")
```


### 通过加减时间计算

```
tz_utc_8 = datetime.timezone(datetime.timedelta(hours=8))
datetime.datetime.now(tz_utc_8)
```

```
datetime.datetime.now(tz_utc_8).isoformat(' ')
```

```
'2020-03-12 13:53:24.699528+08:00'
```

## Reference
- [API](https://docs.python.org/3/library/datetime.html#module-datetime)
- [datetime处理日期和时间](https://www.cnblogs.com/qisq/p/7614398.html)
- [jupyter notebook](https://github.com/junxnone/examples/blob/master/python/python_datetime.ipynb)

