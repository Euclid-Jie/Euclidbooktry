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
```

## 2、获取对应元素

```python
driver.find_elements_by_class_name('list_con') # 通过class的方式获取，也可以使用其他方式
```

## 3、处理元素数据

我习惯于使用BeatifulSoup处理，当然也可以使用selenium套件处理，等有空我再学习一下补上

```python
idList = driver.find_elements_by_class_name('list_con')
soup = BeautifulSoup(idList[0].get_attribute('outerHTML')) # 转换为soup对象
divs = soup.find_all('div', "list clearfix carnival_item") # 找到对象中数据列表
```

