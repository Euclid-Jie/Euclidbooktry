- 切换工作路径

```stata
cd C:\Users\欧玮杰\Desktop\商务统计上机作业
```

- 查看工作路径下所有文件

```stata
ls
```

- 导入数据，直接使用`stata`指定文件格式

```stata
use "C:\Users\欧玮杰\Desktop\商务统计上机作业\mus08psidextract.dta"
```

- 输出为`word`

```stata
asdoc reg Y Z
```

## 面板数据回归

- 设置观测个体和时序变量

```stata
 xtset id t
```

- 混合回归

```stata
reg Y X
```

- 随机效应

```stata
xtreg Y X ,re r theta
```

- LM检验

```stata
xtreg Y X,re r theta
estimates store RE
xttest0
```

- 固定效应模型

```stata
xtreg lwage exp exp2 wks ed ,fe
xtreg lwage exp exp2 wks ed ,fe r # 聚类稳健
```

- 带时间效应的固定效应模型

```stata
xtreg lwage exp exp2 wks ed i.t, fe r
```

- 豪斯曼检验

```stata
xtreg lwage exp exp2 wks ed,fe
estimates store FE
xtreg lwage exp exp2 wks ed
re theta、estimates store RE
hausman FE RE, constant sigmamore
```

