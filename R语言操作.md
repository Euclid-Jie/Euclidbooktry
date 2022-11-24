用于记录`R`语言的一些语法操作，主要为研究生期间的课程所学

# 数据读写

- 读取csv文件

  ```R
  data <- read.csv("fileName.csv")  
  ```

# 绘图

## 散点图

- `plot`散点图，直接使用`plot`

  ```R
  plot(data$x, data$y, xlab="x", ylab="y", pch=16)   # 参数pch设置点的类型
  ```

  ![image-20221124102949628](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124102949628.png)

- 限制y范围

  ```R
  plot(ylim=c(0,2),hii_order,xlab="",ylab="",pch=16)
  ```

- 散点图矩阵

  ```R
  pairs(data, main="Basic Scatter Plot Matrix")     # 基础的散点图矩阵
  ```

  ![image-20221124102919102](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124102919102.png)

## 线图

- 添加回归直线

  ```R
  mo <- lm(y~x,data)                                  # 最小二乘回归
  summary(mo)                                         # 打印结果
  abline(mo, col="red", lwd=2)                        # 添加经验回归直线
  ```
  
  ![image-20221124103117934](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124103117934.png)

# 回归分析

## 数据预处理

- 中心化标准化

  ```R
  data <- as.data.frame(scale(data, center = T, scale = T))    # 标准化
  data <- as.data.frame(scale(data, center = T, scale = F))    # 中心化
  ```

## 建立模型

- 最小二乘回归

  ```R
  mo <- lm(y~x,data)                                  # 最小二乘回归
  summary(mo)                                         # 打印结果
  ```

- 计算杠杆值

  ```R
  hii <- hatvalues(mo)                                # 杠杆值
  ```

  ![image-20221124103158877](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124103158877.png)

- 计算模型残差

  ```R
  SSE <- sum(mo$residuals^2)                          # 残差平方和
  sqrt(SSE/(length(data$x)-2))
  ```


## 模型分析

- 点预测

  ```R
  mo <- lm(y~x,data)                                                  # 最小二乘回归
  none_interval <- predict.lm(mo, data, interval="none")              # 计算点预测值
  ```

- 区间预测

  ```R
  confidence_interval <- predict.lm(mo, data, interval="confidence")  # 计算置信区间预测值
  prediction_interval <- predict.lm(mo, data, interval="prediction")  # 计算预测区间预测值
  ```

- 绘制区间图

  ```R
  # 对齐数据顺序
  data_order <- data[order(data$x),]
  confidence_interval_order <- confidence_interval[order(data$x),]
  prediction_interval_order <- prediction_interval[order(data$x),]
  ```

  开始绘图

  ```R
  plot(data$x, data$y, xlab="x", ylab="y", pch = 16)  # 绘制轮廓
  polygon(c(data_order$x,rev(data_order$x)),c(prediction_interval_order[,2],rev(prediction_interval_order[,3])),col = rgb(221,234,243,max = 255),border = NA)
  polygon(c(data_order$x,rev(data_order$x)),c(confidence_interval_order[,2],rev(confidence_interval_order[,3])),col = "gray",border = NA)  # 其中polygon为绘制多边形的函数，rev为排序函数
  abline(mo, col="red", lwd=2)  
  points(data$x, data$y, pch = 16) 
  ```
  
  ![image-20221124103249152](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124103249152.png)

## 预测相关

- 新值预测

  ```R
  new <- data.frame(x = 3.5)  # 生成新的数据
  predict.lm(mo, new, interval="prediction")  # 点预测+预测上下界
  predict.lm(mo, new, interval="confidence")  # 点预测+置信上下界
  ```

## 随机数

- 设置随机种子

  ```R
  set.seed(1234)
  ```

  