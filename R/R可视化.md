记录R语言可视化相关的内容

## 散点图

- `plot`散点图，直接使用`plot`

  ```R
  plot(data$x, data$y, xlab="x", ylab="y", pch=16)   # 参数pch设置点的类型
  ```

  ![简单散点图](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124102949628.png)

- 限制y范围

  ```R
  plot(ylim=c(0,2),hii_order,xlab="",ylab="",pch=16)
  ```

- 散点图矩阵

  ```R
  pairs(data, main="Basic Scatter Plot Matrix")     # 基础的散点图矩阵
  library(car)
  scatterplotMatrix(data, spread=F, smoother.args=list(lty=2),regLine=T,smooth = F,main="Scatter Plot Matrix via car Pakage")   # 带有分布图的散点图矩阵
  library(GGally)
  ggpairs(data = data)  # 美观的变量矩阵
  ```

  ![散点图矩阵](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124102919102.png)

  ![带有分布图的散点图矩阵](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124123140827.png)

  ![使用ggpairs绘制的散点图矩阵](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124123306464.png)



## 线图

- 添加回归直线

  ```R
  mo <- lm(y~x,data)                                  # 最小二乘回归
  summary(mo)                                         # 打印结果
  abline(mo, col="red", lwd=2)                        # 添加经验回归直线
  ```

  ![添加经验回归拟合直线的散点图](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124103117934.png)

## 坐标轴

- 带坐标轴的回归结果添加

  ```R
  x1 <- rnorm(50,4,2)
  e <- rnorm(50,0,0.1)
  y <- -2 + x1 + e
  plot(x1, y, xlab="x", ylab="y", ylim=c(-8,8), xlim=c(-8,8), pch=15)    # 绘制散点图
  abline(h=0, v=0, lty=2)
  abline(reg=m1, col="black", lwd=2) 
  ```

![带坐标轴的回归直线](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124145543270.png)