`IP`代理作为反反爬的一个有效途径，面对一些基础的反爬网站，学会使用`IP`代理非常有必要

目前我使用来着`GitHub`上一个[开源项目](https://github.com/jhao104/proxy_pool)抓取公开`IP`的项目构建`IP`池子，再次感谢开源博主，下面进行介绍

## `Clone`项目

```shell
git clone git@github.com:jhao104/proxy_pool.git
```

## 确认安装`Redis`并开启服务

`Redis`是一个用于存储键值对的简单数据库，可以从GitHub[下载](https://github.com/tporadowski/redis/releases)，也可以上[官网](https://redis.io/)，安装完成后，运行`redis-cli.exe`，如显示`127.0.0.1:6379>`，说明安装成功，并在指定端口开启服务，进一步可以配置密码，[具体教程](https://www.redis.net.cn/tutorial/3503.html)

```shell
config set requirepass 123456  # 设置密码为123456
```

## 进行项目配置

- 配置`redis`数据库密码

  ```python
  DB_CONN = 'redis://:pwd@127.0.0.1:8888/0'  # pwd改为自己的密码123456
  ```

## 启动IP抓取

```shell
python proxyPool.py schedule  # 运行后开始抓取IP并存入数据库
```

## 调用IP池

```shell
python proxyPool.py server  # 启动API服务接口,端口为http://127.0.0.1:5010
```

具体调用规则包括

| api | method | Description | params|
| ----| ---- | ---- | ----|
| / | GET | api介绍 | None |
| /get | GET | 随机获取一个代理| 可选参数: `?type=https` 过滤支持https的代理|
| /pop | GET | 获取并删除一个代理| 可选参数: `?type=https` 过滤支持https的代理|
| /all | GET | 获取所有代理 |可选参数: `?type=https` 过滤支持https的代理|
| /count | GET | 查看代理数量 |None|
| /delete | GET | 删除代理  |`?proxy=host:ip`|

## 调用实例（记得先开启API服务）


```python
import requests

# 从数据库调用IP
def get_proxy():
    return requests.get("http://127.0.0.1:5010/get/").json()
# 删除数据库中IP
def delete_proxy(proxy):
    requests.get("http://127.0.0.1:5010/delete/?proxy={}".format(proxy))

# 使用代理IP发起请求
def getHtml():
        retry_count = 5
        proxy = get_proxy().get("proxy")
        while retry_count > 0:
            try:
                html = requests.get(URL, proxies={"http": "http://{}".format(proxy)})
                # 使用代理访问
                return html
            except Exception:
                retry_count -= 1
                # 删除代理池中代理
                delete_proxy(proxy)
                return None
```

