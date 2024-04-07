`Numpy`和`Pandas`同等地位的存在，但是我实际用到的不多

### np.cunsum()

累加

```python
self.wheredf['cumsum'] = np.cumsum(self.SecDatadf.TradVolume)
```

### np.max(df)

可以直接取得df中的最大值，还挺不错，min也是一样

```Python
mymax = np.max(df)
```

### np.issubdtype

`np.issubdtype`函数可以检查一个数据类型是否为另一个数据类型的子类型。可以将其与`np.float`传递给`dtype`属性进行比较，如下所示：

```python
import numpy as np
a = np.array([1, 2, 3, 4, 5], dtype=np.float32)
assert np.issubdtype(a.dtype, np.float)
```

这样就可以确保`a.dtype`是`float32`或`float64`，并且断言将不会引发错误。