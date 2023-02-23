本节会记录部分处理`pd.DadaFrame`、`pd.Series`数据时使用到的方法

# pd.DadaFrame函数

## 判断是否为df

```python
if isinstance(data, pd.DataFrame):
```

## 创建DataFrame

```python
Pandas.DataFrame(data,index,columns)
```

用于构建`DataFrame`对象

- `data`可以为`list`，也可以为`pd.series`。需要注意的是，如果数据是单个数，需要使用中括号括起来，否则会报`Index`有关错误

  ```python
  data = {"col1":[number1],"col2":[number2]}
  ```

- `index`可以为别的`df`的索引，也可以写一个list作为索引

- `columns`为列表，用于标记列的名称

## 使用apply进行行或列遍历

```python
Pandas.DataFrame.apply(func,axis)
```

用于对df进行遍历操作，类似于`MATLAB`中对列进行操作实际上是对列中的每个元素进行操作

- `func`，我会写成`lambda x: f(x)`的形式，官方中说，可以调用一个`def(x)`，或者是直接使用`np.sum()`之类的

- `axis=1`就是对列中的每一个进行操作，一般就是这样

```Python
demo_df['updateTime'] = demo_df['updateTime'].apply(lambda x:x.split(' ')[0])
```

## 使用groupby进行分组操作

```python
Pandas.DataFrame.groupby(by,axis)
```

用于对df进行先分组、后操作，值得注意的是，类似Matlab中，分组和操作是分开的，groupby之后只是创建了一个group对象，具体的操作还要再写

- by可以是个str就是某一列的列名，或者是list，因为可以进行多级别的分组

- axis就是行操作还是列操作

- 其他还有很参数，目前没用到，举个列子吧，说一下分组以后怎么进一步操作

```Python
demo_df.groupby(['secID','endDate','publishDate','updateTime','getDate','cat1'])['holdPct'].sum().sort_index()
```

## 输出为csv文件

```python
Pandas.DataFrame.to_csv(filename,mode,encoding,header,index)
```

这个方法是把内存中的df对象保存到本地

- `filename`是保存文件的名称，其实也可以加上路径，就比如`'\导出数据\cross\Shcategory.csv'`，但必须保证文件夹存在，否则会报错。建议在代码中加入路径不存在则使用`os`创建的逻辑

- `mode`是写入的类型，和`python`写入一样的，我不太熟悉，只用到w是创建并写入，`a`是追加写入

- `encoding`是写入文件的编码格式，如果想要用`Excel`打开就是`gbk`，如果用编辑器查看就是`utf-8`，不过`pycharm`可以提醒你用gbk重新打开，不过目前来看最万能的格式是`utf_8_sig`，两边打开都不会乱码

- `header`表示是否写入表头，追加时不要表头，新写时需要写入表头

- `index`表示是否需要写入索引，一般是不需要的，所以index=FALSE就成，仅当index含有除了序号以外的其他信息的时候，才需要写入

## 使用merge拼接数据

```python
Pandas.DataFrame.merge(right,how,on,axis)
```

这个方法类似于`Excel`中的`Vlookup`了，根据关键词将两个df匹配拼接起来

- `right`表示需要拼接的`df`，其实写成`pd.merge(left_df,right_df)`亲测也可以
- `how`表示拼接方法，可选`‘left’, ‘right’, ‘outer’, ‘inner’, ‘cross’`, 默认 `inner`，表示仅保留两个`df`共有的部分，`left`表示仅保留左边`left`的部分
- `on`表示关键词列，如果左右名称不一样，可以分别使用`left_on`，`right_on`
- `axis`一般就是`1`了

特别的，使用merge按照Index拼接

```python
data_df.merge(REVS5,left_index=True,right_index=True)
```



## 使用concat拼接数据

```python
Pandas.DataFrame.concat([df1,df2],axis)
```

这个方法是把两个df直接拼接到一起，或许多个df也可以，没有匹配的功能，就是简单拼接

- `axis = {0:’index’,1:’columns’}, default 0`，意思就是说，默认为0表示根据Index进行拼接

- 还有一些参数，排序之类的就不详细写了，注意的是**两个df一定要写在中括号里面**

## 使用replace替换数据中的元素

```python
Pandas.Series.replace()
```

对Series对象中的符合规定的元素进行替换，可以用正则表达式，很不错

```Python
SecData_df['vwap'].replace(0, np.nan, inplace=True)
```

## 使用GroupBy.rank进行排序

```python
Pandas.DataFrame.groupby().rank()
```

这个操作是对某列的数据进行聚类然后对其它列的属于同类数据进行数值大小排序

- `method`的意思是遇到相同的数值怎么算排名，如果选`‘average’`，那么就会取两个`rank`的平均数，导致的结果就是`rank`中会出现小数，如果选`‘min'`那就是都取最小的排名，如果是‘first’那就是将考前的数值设置为更小的排名

- `ascending`标记排序顺序是从大到小还是从小到大，TRUE表示从小到大

- `na_option`表示了对缺失值NaN怎么处理，`{‘keep’,‘top’,‘bottom’}`，选为`top`则是移到顶部

```python
df.groupby(['gender'])['age'].rank()
```

## 使用roling实现滚动窗口

```python
Pandas.DataFrame.rolling()
```

计算滚动窗口的均值，`EMA`的主要实现方式

## 使用pivot数据重构

```python
Pandas.DataFrame.pivot()
```

数据重构的主要实现方式，通过指定`index`，`columns`，`values`实现对原始`DataFrame`的数据重构

## 使用re对数据中的str数据处理

```
Pandas.Series.str.**
```

这一块就是pandas和re的结合了，但每个方法都很简单，就挨个说一下

- `pandas.Series.str.contains(pat)`，包含`pat`返回`TRUE`，`pat`可以写成正则表达式，可以用|拼接多个

- `pandas.Series.str.endswith(pat)`，以`pat`结尾返回`TRUE`，`pat`可以写成正则表达式，但是不能拼接多个

- `pandas.Series.str.extract(pat)`，使用`pat`拆分，返回多列，然后使用`apply`提取内容

- `pandas.Series.str.len()`，返回元素长度

## 查询元素是否在一个list里出现

```
Pandas.Series.isin(values)
```

这个方法，总体上还是类似`MatLab`，就是对一列里面的每一个元素都操作

- `values`为`list`或者是`str`

- 如果元素在`values`这个`list`中，或者就等于这个`str`（不过这个有点鸡肋，干嘛不直接用==)就在对于的地方返回`True`，整体上来看，也是属于筛选的某些行的操作范畴

## 使用drop删除指定部分

```
Pandas.DataFrame.drop()
```

这个方法就是删除指定的行了，一般第一个参数是以`index`为基础的索引，实操中我一般会先做一个`tag`，然后使用`tag == TRUE`的`index`，作为`drop`的`index`

```python
tag_a = self.CAdf['TradTime'].str.contains('14:5[789]:[0-9]{2}.[0-9]{3}|15:00:[0-9]{2}.[0-9]{3}')
self.SecDatadf.drop(tag_a.index[tag_a], inplace=True)  # 删除提取出的数据
```

删除特定列

```python
data_df.drop(columns=['aiq_date','closePrice','turnoverVol'])
```

## 序列差分

```python
Pandas.DataFrame.diff(axis=1,periods=1)
```

做差分，第一个会变成`NaN`

- 参数`axis`表示对几列进行差分
- 参数`periods`表示差分跨度，默认为`1`

```python
self.wheredf['diff'] = self.wheredf[['Vgroup']].diff()
```

## 使用iterrows生成迭代器

```python
for index, row in data.iterrows():
    # 针对每行数据计算变动
    row_dict = {}
    row_dict['index'] = index
    row_dict['updateTime'] = row['updateTime']
    if index > 0:
        for col in cols:
            if data.iloc[index - 1][col] == np.NaN or data.iloc[index][col] == np.NaN:
                row_dict[col + '_rate'] = np.NaN
            d1 = float(data.iloc[index - 1][col])
            d2 = float(data.iloc[index][col])
            rate = (d2 - d1) / d1
            row_dict[col + '_rate'] = rate
        rate_df = rate_df.append(row_dict, ignore_index=True)
return rate_df
```

## 使用GroupBy生产遍历序列

```
for author_group, group_df in self.mergedata.groupby(['author', 'secCode']):
    # 按照每年分组查询
    for year, year_df in group_df.groupby('foreYear'):
        year_df = year_df.sort_values(by='writeDate')  # 对研报预测时间进行排序
        year_df[field + '_forecast_change'] = year_df.groupby('author')[field].apply(lambda x: (x - x.shift(1)) / x.shift(1))  # 根据要求公式得到想预测字段的变动并储存
        year_df = year_df[['author', 'secName', 'foreYear', field + '_forecast_change', 'writeDate', 'publishDate']]
        self.result = pd.concat([self.result, year_df])
```

# DataFrame切片

## loc

loc对应的是index，loc中可以直接写对Series对象的逻辑判断

```python
subset.loc[subset['upLimitDay'] == 0]
```

## iloc

iloc与loc的区别是，loc以index为基准，iloc则是忽略index直接以行数取出。

当然，iloc也可以取多行，例如：

```python
df2 = self.wheredf.iloc[where:, :]
```

## 直接切

使用尾追一个列表，表示取多少到多少位

```Python
target_position[0:10]
```

## 切出一个元素

想要提取一个元素（数值或str），目前的方法就是先取为list再取其第一个元素

```Python
price = list(temp_df[name])[0]
```

这两种方法也可以

```python
self.SecID = self.SecDatadf['SecurityID'][0] 
```

```python
self.wheredf.loc[indexi]['Vgroup']
```


## pandas分箱

主要步骤是设置箱子bins，注意bins的每个相邻元素之间组成的区间为箱子区间，所以bins元素个数要比箱子个数多一个；然后就是使用Pd.cut进行分箱，几个参数labels为各个箱子的标签，retbins：获取边界值列表，include_lowest字面意思，righ：包含右边界与否

```python
bins = [i * self.targenum for i in range(0, self.cellNum + 1)]  # 设置箱子
pd.cut(np.cumsum(self.SecDatadf.TradVolume), bins, labels=range(1, self.cellNum + 1),retbins=False,include_lowest=True, right=True)
```