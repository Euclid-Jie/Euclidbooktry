用于记录`R`语言的一些语法操作，主要为研究生期间的课程所学

# 数据读写

- 读取`csv`文件

  ```R
  data <- read.csv("fileName.csv")  
  ```

- 读取`txt`数据

  ```
  data <- read.table("energy.txt",header = TRUE,sep = '\t')            # 读取数据
  ```


# 随机数

- 设置随机种子

  ```R
  set.seed(1234)
  ```

- 随机生产序列

  ```R
  x1 <- rnorm(50,4,2)
  e <- rnorm(50,0,0.1)
  y <- -2 + x1 + e
  ```

  ![随机生产的序列](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/image-20221124145033909.png)