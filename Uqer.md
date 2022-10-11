要想使用Uqer数据库导入数据，一般要经过如下几步骤

```Python
import uqer
mytoken = 'b8a2a2a35c9a7ce2d458fb3b44cb6c0ea0bdcf14ba2ea3a8311c92aa4396b154'
client = uqer.Client(token=mytoken)
from uqer import DataAPI
DataAPI.EquGet
```