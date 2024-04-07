将自己的工作，构建为`python`的`Package`并上传至[PYPI](https://pypi.org/)，使得其他开发者可以通过`pip`安装并使用。这是我一直想做的事情，最近我成功将[微博数据](https://github.com/Euclid-Jie/Euclidweibo-search)采集项目封装并上传至[PYPI](https://pypi.org/project/EuclidSearchPackage/)。为使得后续维护工作顺利开展，并方便上传新的`Package`，特此记录工作要点。

## 如何将项目组织成`Package`

最重要的两个点就是`__init__.py`文件和相对引用

首先我展示目前的`Package-dev`目录

```tex
D:PackageName_dev
│  .gitignore
│  LICENSE
│  list.txt
│  pyproject.toml
│  README.md
│          
├─dist
│      EuclidSearchPackage-0.5.0-py3-none-any.whl
│      EuclidSearchPackage-0.5.0.tar.gz
│      
└─src
    ├─EuclidSearchPackage
    │  │  __init__.py
    │  │  
    │  ├─Demo
    │  │  │  WeiboClassV2.py
    │  │  │  WeiboClassV3.py
    │  │  │  __init__.py
    │  │          
    │  ├─Utils
    │  │  │  EuclidDataTools.py
    │  │  │  EuclidDataTools_test.py
    │  │  │  MongoClient.py
    │  │  │  Set_header.py
    │  │  │  Utils.py
    │  │  │  __init__.py
    │  │          
    │  ├─WeiboSearch
    │  │  │  Get_item_url_list.py
    │  │  │  Get_longTextContent.py
    │  │  │  Get_single_weibo_data.py
    │  │  │  Get_single_weibo_data_async.py
    │  │  │  Get_single_weibo_details.py
    │  │  │  Get_user_all_weibo.py
    │  │  │  Get_user_info.py
    │  │  │  Set_cookie.py
    │  │  │  __init__.py
    │  │          
    │          
    ├─EuclidSearchPackage.egg-info
    │      dependency_links.txt
    │      PKG-INFO
    │      SOURCES.txt
    │      top_level.txt
    │      
    └─Test
        │  cookie.txt
        │  DemoTest.py
        │  test.csv
        │  Test.py
        │  WeiboClassV2.py
```

### 一级目录说明

可以看到`dev`一级路径下有

- `src`: 开发代码将写在这个文件夹下，后一节将展开讲解
- `dist`：当`package`被正式`build`时，该目录被自动创建，并生成whl文件在此目录下

- `pyproject.toml`：软件包架构参数设定，建议按照官方[建议](https://packaging.python.org/en/latest/tutorials/packaging-projects/#creating-pyproject-toml)撰写
- `README.md`：说明文档，将同步到PYPI的项目介绍中，例如[project description](https://pypi.org/project/EuclidSearchPackage/)
- `LICENSE`：版权信息，[可以按照网上的教程选择](http://www.ruanyifeng.com/blog/2011/05/how_to_choose_free_software_licenses.html)

- `.gitignore`：`git`控制中的`ignore`，如果不使用git可以忽略

### `scr`说明

`src`下有三个文件夹

- `EuclidSearchPackage`：包里面的程序，当包发布后，包的内容就是此文件夹中的文件
- `EuclidSearchPackage.egg-info`：当`package`被正式`build`时，该目录被自动创建，将存储`info`
- `Test`：非必须，可以用于模拟`package`被安装后的调用过程，作为测试

### 关于`__init__.py`

我们提取package的部分来看，如何写`__init__.py`

```tex
├─Demo
│  │  WeiboClassV2.py
│  │  WeiboClassV3.py
│  │  __init__.py
```

这是package中的一个`subpackage`，名字为`demo`，下有三个文件，其中`WeiboClassV2.py`和`WeiboClassV3.py`是代码，`__init__.py`的内容为：

```python
from .WeiboClassV2 import WeiboClassV2
from .WeiboClassV3 import WeiboClassV3
```

简单来说`init`的作用就是初始化，在调用时，`init`会被首先执行，将`WeiboClassV2`和`WeiboClassV3`调入代码空间，使其可以被调用。需要注意的是相对位置的引用规则，即得加一个`.`

下面展示一个完整的`__init__.py`，变量`__all__`展示了，使用`import *`能被调用的方法或变量

```python
from .Get_item_url_list import Get_item_url_list
from .Get_user_info import Get_user_info
from .Set_cookie import Set_cookie
from .Get_single_weibo_data import Get_single_weibo_data
from .Get_user_all_weibo import Get_user_all_weibo
from .Get_single_weibo_data_async import Get_single_weibo_data_async
from .Get_longTextContent import Get_longTextContent

# 未完成
from .Get_single_weibo_details import Get_single_weibo_details

__all__ = ['Get_user_all_weibo', 'Get_user_info', 'Set_cookie',
           'Get_item_url_list', 'Get_single_weibo_data',
```

### 关于相对位置引用

在上一节的`init`写法中已经讲到了得加`.`，但是有一种情况是需要另外注意的，提取目录的部分进行说明：

```tex
├─Utils
│  │  MongoClient.py
│  │  Set_header.py      
│  │  __init__.py
├─WeiboSearch
│  │  Get_item_url_list.py
```

具体场景为，在`Get_item_url_list.py`中需要调用`Set_header.py` 中的`Set_header`函数，那么需要

- 首先确保`__init__.py`中

    ```python
    from .Set_header import Set_header
    from .Set_header import *  # 二选一，更推荐上面的写法
    ```

- 在`Get_item_url_list.py`中，使用如下方式引用`Set_header`函数

  ```python
  from ..Utils import Set_header
  ```

### 关于`Test`目录

此目录可以模拟包被安装后的使用过程，不过导入还是有些微差别，需要加上`src.`：

```python
import src.EuclidSearchPackage as ESP
```

后续的写法就完全一致了，建议发布前都测试一下。

## 打包发布Package

建议参照[官方教程](https://packaging.python.org/en/latest/tutorials/packaging-projects/)，总结起来有这么关键的几步：

- `Creating pyproject.toml`，即软件包架构参数设定，建议按照官方[建议](https://packaging.python.org/en/latest/tutorials/packaging-projects/#creating-pyproject-toml)撰写
- `Creating README.md`：代码说明，建议还是写清楚，会同步到PYPI的project description
- Creating a LICENSE：官方的[示例](https://packaging.python.org/en/latest/tutorials/packaging-projects/#creating-a-license)
- `build`：构建包`python -m build`，生成的文件会在`dist`目录下，版本迭代后，记得删掉旧版本
- `upload`：将`package`上传至`PYPI`，`python twine upload dist/*`，需要输入用户名和密码，如果没有账号需要提前创建。

## 更新维护

建议同步将`package_dev`开源至`github`，方便接受`issue`，对`package`更新后，记得更新版本号，然后重新build上传就好。
