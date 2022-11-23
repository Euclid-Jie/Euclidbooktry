作为Requests和Selenium的补充，简单记录其用法

## Urllib3的请求方法

- Get请求

    ```python
    import urllib3
    http = urllib3.PoolManager()  # 创建PoolManager对象生成请求
    response = http.request('GET', 'http://www.baidu.com') # get方式请求
    print(response.status,response.data.decode('utf-8'))  # 获得状态码, html源码(utf-8解码)
    ```

- Post请求

    ```
    import urllib3
    import json
    http = urllib3.PoolManager()
    headers = {
        'User-Agent':'Mozilla/5.0 (Windows NT 10.0; WOW64)',
        'Host':'httpbin.org'}
    data = {'word':'hello'}
    data = json.dumps(data).encode()  # json.dumps方法可以将python对象转换为json对象
    response = http.request('POST','http://httpbin.org/post',body=data, headers=header)
    print(response.status,response.data.decode('utf-8')) 
    ```

