记录`MonGoDB`数据库的使用，主要使用`Python`语言。

## MongoDB安装及配置

参照[最详细的Windows平台安装MongoDB教程 - TM0831 - 博客园 (cnblogs.com)](https://www.cnblogs.com/TM0831/p/10606624.html)

## 数据库启动服务

- 启动数据库服务

切换到`mogod`路径，运行`mogod`，并指定参数

```shell
mongod --dbpath D:\Euclid_Jie\DBdata
```

查看端口http://127.0.0.1:27017/，若显示如下内容，说明服务已经启动

```
It looks like you are trying to access MongoDB over HTTP on the native driver port.
```

- 关闭数据库服务

  于服务窗口按下ctrl+C结束服务

- 使用数据库命令关闭（适用于数据库存储位置错误启动）

  ```shell
  use admin
  db.shutdownServer()
  ```

## 数据库创建及写入

使用`pymongo`库完成对`Mongo`的操作

- 连接数据库，其中`DBName`为数据库的名字，`collectionName`类似于表名

  ```python
  import pymongo
  def MongoClient(DBName, collectionName):
      # 连接数据库
      myclient = pymongo.MongoClient("mongodb://localhost:27017/")
      mydb = myclient[DBName]  # 数据库名称
      mycol = mydb[collectionName]  # 集合（表）
      return mycol
  # 返回一个数据表
  mycol = MongoClient("ZhiHu", '11月知乎舆情')
  ```

- 创建数据库、表

  直接连接指定的库和表，如果存在则连接，如果不存在将创建，但是需要注意的是，只有当正式往表中写入数据后，表才被正式创建

- 写入数据

  ```python
  mycol.insert_one(document)  # 其中document为json格式的数据
  mycol.insert_many(document)  # 写入多条
  ```

- 读取数据

  Mongo数据库的数据由唯一的键`_id`进行索引，如果没有写入指定的`_id`，将自动创建索引。

  ```python
  mycol.distinct("_id")  # 获取数据表的所有id，返回格式为list
  mycol.find_one({'_id': id})  # 根据指定条件查询，返回数据表的其中一条数据，格式为json
  ```

- 修改数据（增加列）

  对原始的数据进行修改或，增加列内容，逻辑为确定哪一行，然后进行何种修改

  ```python
  mycol.update_one({'_id': id}, {"$set": {'comment': comment}})  # $set为一种更新方法
  ```


- 筛选子集

  使用distinct设置筛选条件，获取符合条件的字段

  ```python
  idList = mycol.distinct("_id", {'天眼查Num': "天眼查无法查询", 'Url': {'$exists': False}})
  ```
  
  ## 数据查询
  
  ### 查询字段非空
  
  ```shell
  db.cols.find({"name":{"$ne":null}})
  ```
  
  ### 查询字段包含数字
  
  ```shell
  db.cols.find({"name":{$regex:"\d"}})
  db.cols..find({"name":{$regex:"[0-9]"}})
  ```
  
  未完待续，详见[官方文档](https://www.mongodb.com/docs/manual/tutorial/)
