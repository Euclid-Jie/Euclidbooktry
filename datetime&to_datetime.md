# datetime

```
import datetime  # 导入库
datetime.datetime.today() 
```

## 获取当前时间

```python
datetime.datetime.today() 
# Out[19]: datetime.datetime(2023, 4, 3, 23, 15, 38, 611194) # type为datetime.datetime
```

## 处理为日期数据

```python
datetime.datetime.today().date()
# Out[23]: datetime.date(2023, 4, 3)  # type为datetime.date
```

## str转datetime.datetime

```python
day1 = datetime.datetime.today().date()
day1.strftime("%Y%m%d")
# Out[30]: '20230403'  # type为str
```

## datetime.datetime转str

```python
datetime.datetime.strptime('20200101','%Y%m%d')
# Out[34]: datetime.datetime(2020, 1, 1, 0, 0) # type为datetime.datetime
```

# pandas.to_datetime

## str转timestamps.Timestamp

```python
pd.to_datetime("20200101")
# Out[37]: Timestamp('2020-01-01 00:00:00')  # type为pandas._libs.tslibs.timestamps.Timestamp
```

## timestamps.Timestamp转str

```python
day2 = pd.to_datetime("20200101")
day2.strftime('%Y%m%d')
# Out[40]: '20200101'  # type为str
```

### timestamps.Timestamp转datetime.date

```python
day2.date()
# Out[41]: datetime.date(2020, 1, 1)  # type为datetime.date
```

### timestamps.Timestamp查看周几

```python
day2.day_name()
Out[44]: 'Wednesday'
```

