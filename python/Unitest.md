## 目录结构

其中 `stats.py` 为函数实现，`test_stats.py` 为测试文件

```markdown
- toolkit [project folder]
 - src [sorce folder]
 	- init.py
 	- stats.py
 - tests [test folder]
 	- test_stats.py
```

## 以下为 `test_stats.py` 内容

```python
import unittest
import numpy as np
from toolkit.stats import f_trapezoid
class StatsUtilsTest(unittest.TestCase):
    def test_f_trapezoid(self):
        a = np.array([-5.5, -4.5, -3.5, -2.5, -1.5, -0.5, 0.5, 1.5, 2.5, 3.5, 4.5, 5.5])
        realized_a = f_trapezoid(a, 2, 3, 5)
        expected_a = np.array([-0.5, -1, -1, -0.5, 0, 0, 0, 0, 0.5, 1, 1, 0.5])
        np.testing.assert_almost_equal(realized_a, expected_a, decimal=7)
if __name__ == "__main__":
unittest.main()
        
```

## 运行测试

### 测试整个文件中的所有测试单元

```cmd
python -m unittest tests.test_stats.StatsUtilsTest
```

或

```cmd
python -m unittest tests/test_stats.py
```

### 测试文件中的指定测试单元

```cmd
python -m unittest tests.test_stats.StatsUtilsTest.test_f_trapezoid
```

### 测试整个 `tests` 目录下的所有文件中的所有测试

```cmd
python -m unittest discover -s tests
```

