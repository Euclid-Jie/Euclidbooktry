记录Python包安装的注意事项

## 安装问题

- 指定源，处理超时问题

  ```shell
  pip install redis -i http://pypi.douban.com/simple --trusted-host pypi.douban.com
  ```

- 注意安装Python的环境，不要装到别的环境中，可修改`pycharm`中的终端为`cmd`，可使得每次使用当前环境执行命令

## 安装whl

直接使用pip安装对应下载的whl文件即可，注意whl文件的路径，或者将whl移入到Anaconda\Lib\site-packages下

```python
pip install Path\pakageName.whl
```



## 判断下载win32还是amd64的whl文件

如果返回32bit，则下载win32，一般都是64位，所以下载amd64.whl

```python
import platform
platform.architecture()
```



# 值得记一下的库

## tqdm

用于构建循环进度条

```python
from tqdm import tqdm
with tqdm(range(begin, end)) as Range:
    for i in Range:
        Range.set_postfix({"_id": TaxNum})  # 进度条右边显示信息
```

## retry

修饰器，执行函数重试

```python
from retrying import retry
@retry(stop_max_attempt_number=10)  # 最多尝试10次
def MainGet(myHeaders, begin, end):
	pass
```



