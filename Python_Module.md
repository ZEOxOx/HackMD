# h.Python - 模組(Module)

###### tags: `Python`

## 1.自訂模組

* <font color="#0080FF">**第一個自訂模組**</font>

<font color="#0080FF">**mymath.py**</font>

```python=+
'''mymath-自訂數學模組'''
pi = 3.14159

def area(r):
    '''area(r)-傳回半徑r的圓形面積'''
    return r * r * pi
```

## 
* <font color="#0080FF">**引入模組並使用**</font>

<font color="#0080FF">**test.py**</font>

```python=+
import mymath

print(mymath.__doc__) #查看模組的文字字串
print(mymath.pi)

print(mymath.area.__doc__) #查看模組內函式的文字字串
print(mymath.area(3))
```

> ```mymath-自訂數學模組```</br>
> ```3.14159```</br>
> ```area(r)-傳回半徑r的圓形面積```</br>
> ```28.27431```

## 2.模組相關操作

* <font color="#0080FF">**重新匯入模組**</font>

> <font color="#EA0000">**模組已經被載入後，重複執行 import 不會再次從檔案載入模組(效率考量)。
> 若想要邊修邊測試時，必須使用 importlib 模組中的 reload() 函式**</font>

```python=+
import mymath, importlib
importlib.reload(mymath)
```

> ```<module 'mymath' from 'C:\\Users\\tonyc\\pythonwork\\Python_dev\\mymath.py'>```

##
* <font color="#0080FF">**模組搜尋路徑**</font>

> <font color="#EA0000">**import 模組時，會先從當前目錄開始尋找，接著依序為系統設定路徑
> 可透過 sys.path 查看模組搜尋的路徑**</font>

```python=+
import sys
sys.path
```

> ```['C:\\Users\\tonyc\\pythonwork\\Python_dev','C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu\\python37.zip','C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu\\DLLs','C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu\\lib',...]```

## 3.推薦的自訂模組存放目錄
* <font color="#0080FF">**(!)推薦的自訂模組存放目錄(.pth檔)**</font>

> <font color="#EA0000">**在 Windows 中，「.pth檔」可存放在 sys.prefix 變數所指向的目錄中**</font>

```python=+
import sys
sys.prefix
```

> ```'C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu'```
##
<font color="#0080FF">**mypath.pth (C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu)**</font>

> <font color="#EA0000">**在 sys.prefix 指向目錄新增「mypath.pth」。下次啟動 Python 直譯器時，「.pth檔」內容的路徑將會附加到 sys.path 裡面，即可在此指定目錄下存放模組**</font>

```python=+
mymodule #相對路徑
C:\Users\tonyc\pythonwork\mymodule #絕對路徑
#(注意)這兩個是不同路徑喔!!
```
##
<font color="#0080FF">**sys.path**</font>

```python=+
sys.path
```

>```[...,'C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu\\mymodule','C:\\Users\\tonyc\\pythonwork\\mymodule',...]```

## 4.模組中的私有名稱

<font color="#0080FF">**modtest.py**</font>

```python=+
'''modtest - my test module'''
def f(x):
    return x

def _g(x): #以「_底線」開頭命名，避免被「import *」自動匯入
    return x

a = 1
_b = 2 #以「_底線」開頭命名，避免被「import *」自動匯入
```
##
* <font color="#0080FF">**匯入私有名稱a**</font>

```python=+
from modtest import *
a
f(3)
_g(5) #私有名稱不會被「import *」自動匯入
```
> ```1```</br>
> ```3```</br>
> ```NameError: name '_g' is not defined```
## 
* <font color="#0080FF">**匯入私有名稱b**</font>

```python=+
#必須直接指定私有名稱，才可匯入使用
import modtest
modtest._b 

from modtest import _g
_g(5)
```

> ```2```</br>
> ```5```

## 5.用 argparse 模組解析命令列參數

**(SKIP)**

## 時間戳記

> [name=ZEOxO][time=Mon, Aug 31, 2020 14:05 PM][color=#907bf7]