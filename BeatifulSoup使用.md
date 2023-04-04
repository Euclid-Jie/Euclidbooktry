`beautifulsoup`包的主要作用是将`str`格式的网页源码转换成`soup`格式，`soup`格式可以通过类似`json`格式的方式进行索引。

# 主要流程介绍

## 解析网页源码

```Python
import requests
from bs4 import BeautifulSoup # 导入类库
response = requests.get(Url, headers=headers, timeout=60)  # 使用request获取网页
html = response.content.decode('utf-8', 'ignore')  # 将网页源码转换格式为html
soup = BeautifulSoup(html, features="lxml")  # 构建soup对象，"lxml"为设置的解析器
```

结合`selennium`处理数据

```python
idList = driver.find_elements_by_class_name('list_con') # driver查找元素
soup = BeautifulSoup(idList[0].get_attribute('outerHTML')) # 获取元素的内容彬转换为soup对象
```

## 查找标签

- `find_all`

  ```python
  soup.find_all('div', "classname")  # 查找soup中Class属性为"classname"的"div"标签
  ```

- 指定其他属性

  ```python
  soup.find_all('div', {"id":"idName"})  # 查找soup中id属性为"idName"的"div"标签
  ```

- 使用`Xpath`，下一篇有正则用法

  ```
  self.driver.find_elements(By.XPATH, '//*[@id="gs_cit-x"]/span[1]')[0].click()
  ```

## 获取文本内容

- `text`

  ```Python
  divs.text # 直接获取"div"标签下的文本信息
  ```

