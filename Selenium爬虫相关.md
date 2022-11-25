为了`Selenium`方法的成功使用，必须保证`ChromeDriver`安装版本与`Chrome`版本匹配。当然你也可以使用其它浏览器，个人选择。

这是`ChromeDriver`的镜像下载[地址](https://registry.npmmirror.com/binary.html?path=chromedriver/)，更新浏览器后记得更新`ChromeDriver`，顺便我个人记录一下，我的`ChromeDriver`装在`C:\Program Files (x86)\Google\Chrome\Application`

# 主要流程讲解

## 1、控制开启浏览器

```python
from selenium.webdriver import Chrome, ChromeOptions # 导入类库
option = ChromeOptions() # 初始化类
option.add_experimental_option("excludeSwitches", ['enable-automation', 'enable-logging']) # 添加参数
driver = Chrome(options=option)  # 模拟开浏览器
driver.get('https://m.xiaozhu.com/#') # 跳转网址
myDriver.maximize_window()  # 最大化窗口
```

## 2、获取对应元素

```python
driver.find_elements_by_class_name('list_con') # 通过class的方式获取，也可以使用其他方式
find_elements(By.XPATH,"//*[contains(@href, 'pdf')]").get_attribute('href')
```

`selenium`更新后，之前的获取元素的方式发生了改变，主要差异为引入了`By`,其他的参数直接点开`By`查看即可

```python
from selenium.webdriver.common.by import By
driver.find_elements(By.CLASS_NAME, 'list_con'))
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

