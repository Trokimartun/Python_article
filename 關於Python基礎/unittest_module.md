### 參數：assertNotIn()接受以下說明的三個參數：  

* key：在給定容器中檢查其存在性的字符串  
* container：在其中搜索關鍵字符串的字符串  
* message：作為測試消息失敗時顯示的消息的字符串語句。  
下麵列出了兩個不同的示例，它們說明了給定assert函數的正面和負面測試案例：  

```py
# test suite 
import unittest 
  
class TestStringMethods(unittest.TestCase):
    # test function to test whether key is present in container 
    def test_negative(self):
        key = "geeks"
        container = "geeksforgeeks"
        # error message in case if test case got failed 
        message = "key is present in container."
        # assertNotIn() to check if key is in container 
        self.assertNotIn(key, container, message) 
  
if __name__ == '__main__':
    unittest.main()
```

輸出：
F
======================================================================
FAIL:test_negative (__main__.TestStringMethods)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "/home/e99e85838dde0c8ef29ab17fef478979.py", line 12, in test_negative
    self.assertNotIn(key, container, message)
AssertionError:'geeks' unexpectedly found in 'geeksforgeeks':key is present in container.

----------------------------------------------------------------------
Ran 1 test in 0.000s

FAILED (failures=1)]

### 示例2：正測試用例

```py
import unittest 
  
  
class TestStringMethods(unittest.TestCase):
    # test function to test whether key is present in container 
    def test_positive(self):
        key = "gfgs"
        container = "geeksforgeeks"
        # error message in case if test case got failed 
        message = "key is present in container."
        # assertNotIn() to check if key is in container 
        self.assertNotIn(key, container, message) 
  
  
if __name__ == '__main__':
    unittest.main()
```
輸出：

.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
