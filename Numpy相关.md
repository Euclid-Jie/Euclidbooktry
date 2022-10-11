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