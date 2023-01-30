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
