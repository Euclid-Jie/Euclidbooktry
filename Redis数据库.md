相关链接：

- [Python使用Redis (biancheng.net)](http://c.biancheng.net/redis/python.html)
- [Python redis 使用介绍 | 菜鸟教程 (runoob.com)](https://www.runoob.com/w3cnote/python-redis-intro.html)

- [Python中使用Redis详解 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/51608696)

## 链接Redis

### 开启Redis服务

安装Redis后，执行exe程序即可开启端口

```shell
cd D:\Program Files\Redis
redis-server.exe
```

### 关闭Redis服务

```shell
redis-server --service-stop
```

### 使用Python链接

- 密码：password
- 数据库编号（0-15）：db

```python
import redis
pool = redis.ConnectionPool(host='localhost', port=6379, db=1, password=None, decode_responses=True)
r = redis.Redis(connection_pool=pool)
```

## Hash命令

此系列命令用于处理Hash表，详情可参照[Python操作redis系列以 哈希(Hash)命令详解（四）](https://www.cnblogs.com/xuchunlin/p/7064860.html)

>  哈希表的组织形式为name -> {key1:value1, key2:value1...}，如下图所示，
>
> 若value为dict，则实现了DataFrame形式的存储
>
> 其中name对应为整个DataFrame，key对应为每行数据的主键，value对应以dict格式存储的单行数据

![image-20230601161542508](https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202306011615602.png)

### Hset

哈希表中的字段赋值

> 如果name不存在，将自动生成哈希表
>
> 如果key已存在，则进行写入，并返回
>
> 如果key已存在，则进行更新，并返回0

```python
r.hset(name="name",key="key1",value="value")
```

### Hdel

删除哈希表中的字段

> 成功删除则返回1
>
> 若key不存在则删除失败，返回0
>
> 删除所有的键后，name对应的数据将消失

```python
r.hdel(name="name",key="key1")
r.hdel(name='name',key=*['key1','key2'])  # 删除多个
```

### Hexists 

查看哈希表的指定字段是否存在

> 如果存在返回True，否则返回False
>
> 如果name不存在，也会返回False，故需要使用exists检测name是否存在

```python
r.hexists('name1','key2')
r.exists('name1')  # 如存在返回1, 否则返回0
```

### Hget

返回哈希表中指定字段的值

> 如果给定的字段或 key 不存在时，返回 None
>
> 如果name不存在，也会返回None

```python
r.hget('name3','key2')
```

### Hgetall

返回哈希表中，所有的字段和值

>如果name不存在，则返回{}，其type为dict

```python
r.hgetall('name')
```



## 写入数据

### 写入单个键值对

```python
r.set('webname','www.biancheng.net')
```

### 写入多个键值对

```python
r.mset({'username':'jacak','password':'123'})
```

## 删除

### 删除带指定字符的key及value

```python
# 删除带特殊符号的标题
for i in pd.DataFrame(data={'data':r.keys('*')})[pd.DataFrame(data={'data':r.keys('*')}).data.str.contains(':')].data.to_list():
    r.delete(i)
```

## 修改Key

```python
r.rename('name_2', 'name_100')
```

## 在服务器部署Redis

需要注意的是，需要在ESC安全组中开启Redis服务的端口6379

- [(89条消息) 阿里云ECS之搭建Redis环境(八)_zheng_zq666的博客-CSDN博客](https://blog.csdn.net/qq_42528769/article/details/105024569)
