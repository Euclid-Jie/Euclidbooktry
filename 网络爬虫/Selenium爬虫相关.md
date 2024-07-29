为了`Selenium`方法的成功使用，必须保证`ChromeDriver`安装版本与`Chrome`版本匹配。当然你也可以使用其它浏览器，个人选择。

这是`ChromeDriver`的镜像下载[地址](https://registry.npmmirror.com/binary.html?path=chromedriver/)，更新浏览器后记得更新`ChromeDriver`，顺便我个人记录一下，我的`ChromeDriver`装在`C:\Program Files (x86)\Google\Chrome\Application`

> 注意：
>
> 1、上文中的镜像已停止更新，现在只能从`ChromeDriver`官方[站点](https://googlechromelabs.github.io/chrome-for-testing/)进行下载
>
> 2、此外`ChromeDriver`不仅要放到`\Chrome\Application`下，还有可能需要放到python路径下：`D:\Program Files\Anaconda3`

# 主要流程讲解

## 1、控制开启浏览器

```python
from selenium.webdriver import Chrome, ChromeOptions # 导入类库
option = ChromeOptions() # 初始化类
option.add_experimental_option("excludeSwitches", ['enable-automation', 'enable-logging']) # 添加参数
driver = Chrome(options=option)  # 模拟开浏览器
driver.get('https://m.xiaozhu.com/#') # 跳转网址
myDriver.maximize_window()  # 最大化窗口
driver.title  # 如果成功打印title则说明接管成功
```

## 2、获取对应元素

```python
driver.find_elements_by_class_name('list_con') # 通过class的方式获取，也可以使用其他方式
find_elements(By.XPATH,"//*[contains(@href, 'pdf')]").get_attribute('href')
```

`selenium`更新后，之前的获取元素的方式发生了改变，主要差异为引入了`By`,其他的参数直接点开`By`查看即可

```python
from selenium.webdriver.common.by import By
driver.find_elements(By.CLASS_NAME, 'list_con')
```

同样可以使用`Xpath`获取元素，语法为`//节点名[starts-with(@元素名, "相同部分")]`

```python
//div[starts-with(@id,'ma')]  # 选取id值以ma开头的div节点
//div[contains(@id,'ma')]  # 选取id值含有ma的div节点
//div[contains(@id,'ma') and contains(@id,'in')]  # 选取id值包含ma和in的div
//div[contians(text(),'ma')]  # 选取节点文本包含ma的div节点
```



## 3、处理元素数据

我习惯于使用`BeatifulSoup`处理，当然也可以使用`selenium`套件处理，等有空我再学习一下补上

```python
idList = driver.find_elements_by_class_name('list_con')
soup = BeautifulSoup(idList[0].get_attribute('outerHTML')) # 转换为soup对象
divs = soup.find_all('div', "list clearfix carnival_item") # 找到对象中数据列表
element.click() # 点击元素
```

## 4、设置等待
```python
from selenium.webdriver.support.wait import WebDriverWait
WebDriverWait(myDriver, 10).until(lambda driver: driver.find_element(By.CLASS_NAME, 'bicon.bar-icon-fp'))
```

## 5、托管指定端口的浏览器

对于知乎这种网站，使用selenium控制开启一个浏览器往往会被识别，所以需要我们配置一个浏览器（进行登录等常规操作）后，再使用代码直接托管，具体流程如下：

- 将Chrome发送到桌面快捷方式，并设置其端口和缓存文件路径

  <img src="https://euclid-picgo.oss-cn-shenzhen.aliyuncs.com/image/202211291930932.png" alt="image-20221129193010882"  />

  目标处填入“程序路径 端口设置 文件路径”，具体如下

    ```
    "C:\Program Files\Google\Chrome\Application\chrome.exe" --remote-debugging-port=9222 --user-data-dir="D:\Euclid_Jie"
    ```

- 使用Python接管浏览器

  ```python
  from selenium import webdriver
  options = webdriver.ChromeOptions()
  options.add_experimental_option("debuggerAddress", "127.0.0.1:9222")  # 接管
  driver = webdriver.Chrome(options=options)  # 设置参数
  driver.get(Url)  # 跳转网页
  ```
  
  
