# Python - 命名空間(namespace)

###### tags: `Python`

## 1.命名空間

* <font color="#0080FF">**三種類型的命名空間**</font>

| 類別 | 說明 |
| :------: | :-----------: |
| 內建(builtin)| Python解釋器進行時，會建立一個名為 __ builtin __ 的模組，此模組包含所有內建函式，例如 len()、min()、max()、str() 等 |
| 全域(global) | 建立其他模組時，模組所帶的命名空間被稱為全域命名空間，放在這個空間中的變數即為「全域變數」。 |
| 區域(local)  | 呼叫函式時，Python 會為這個函式建立一個區域命名空間，</br>放在這個空間中的變數即為「區域變數」。</br>函式結束後，這個命名空間會隨之刪除 |

## 2.命名空間相關操作

* <font color="#0080FF">**查詢區域 ( local ) 命名空間**</font>

```python=+
locals() #因為沒有建立變數或引入函式，因此內容和global()相似
```

> ```{'__name__': '__main__','__doc__': 'Automatically created module for IPython interactive environment','__package__': None,'__loader__': None,'__spec__': None,'__builtin__': <module 'builtins' (built-in)>,'__builtins__': <module 'builtins' (built-in)>,'_ih': ['', 'locals()'],'_oh': {},...}```
## 
* <font color="#0080FF">**查詢全域 ( global ) 命名空間**</font>

```python=+
globals() #因為沒有建立變數或引入函式，因此內容和locals()相似
```

> ```{'__name__': '__main__','__doc__': 'Automatically created module for IPython interactive environment','__package__': None,'__loader__': None,'__spec__': None,'__builtin__': <module 'builtins' (built-in)>,'__builtins__': <module 'builtins' (built-in)>,'_ih': ['', 'locals()', 'globals()'],'_oh': {1: {...}},...}```
##
* <font color="#0080FF">**建立新變數並匯入模組**</font>

```python=+
z = 2
import math
from cmath import cos

globals() #因為有新變數，增加了一些新的數值
```

> ```{'__name__': '__main__',...,'_i': 'globals()','_ii': 'locals()','_iii': '','_i1': 'locals()','_1': {...},'_i2': 'globals()','_2': {...},'_i3': 'z = 2\nimport math\nfrom cmath import cos\n\nglobals()','z': 2,'math': <module 'math' (built-in)>,'cos': <function cmath.cos(z, /)>}```
## 
* <font color="#0080FF">**將名稱從命名空間刪除**</font>

```python=+
del z,math,cos

globals() #命名空間看不到z,math,cos且模組內函式也變得不可用
math.ceil(3.4)

#重新匯入
import math
math.ceil(3.4)
```

> ```{'__name__': '__main__',...,'_i': 'del z,math,cos','_ii': 'z = 2\nimport math\nfrom cmath import cos\n\nglobals()','_iii': 'globals()','_i1': 'locals()','_1': {...},'_i2': 'globals()','_2': {...},'_i3': 'z = 2\nimport math\nfrom cmath import cos\n\nglobals()','_3': {...},'_i4': 'del z,math,cos','_i5': 'globals()'}```</br></br>
> ```NameError: name 'math' is not defined```</br>
> ```4```
##
* <font color="#0080FF">**查看函式內區域變數**</font>

```python=+
def f(x):
    #可以看到模組函式f的位址
    print('globals:',globals())
    print('進入 local:',locals())
    y = x
    print('離開 local:',locals())
    
z = 2
f(z)
#locals() <-這裡使用locals()已看不到變數
```

> ```globals: {'__name__': '__main__',..., '_i': '', '_ii': '', '_iii': '', '_i1': "def f(x):\n    print('globals:',globals())\n    print('進入 local:',locals())\n    y = x\n    print('離開 local:',locals())\n    \nz = 2\nf(z)", 'f': <function f at 0x00000205C393C438>, 'z': 2}```</br></br>
> ```進入 local: {'x': 2}```</br>
> ```離開 local: {'x': 2, 'y': 2}```

## 3.已匯入模組的命名空間

<font color="#0080FF">**scopetest.py**</font>

```python=+
'''scopetest - 可視範圍測試模組'''
v = 6
def f(x):
    '''f - scope test function'''
    print('global: ',list(globals().keys()))
    print('進入 local: ',locals())
    y = x
    w = v
    print('離開 local: ',locals().keys())
```
##
* <font color="#0080FF">**名稱的可視範圍**</font>

```python=+
import scopetest

z = 2
scopetest.f(z)
#命名空間不包含交談模式中建立的變數z，因此無須擔心
#模組外部的名稱會影響內部程式碼的運作
```

> ```global:  ['__name__', '__doc__', '__package__', '__loader__', '__spec__', '__file__', '__cached__', '__builtins__', 'v', 'f']```</br></br>
> ```進入 local:  {'x': 2}```</br>
> ```離開 local:  dict_keys(['x', 'y', 'w'])```

## 4.(!)從模組 import 變數容易發生的問題


<font color="#0080FF">**counter.py**</font>

```python=+
num = 0
def add():
    global num
    num += 1
```
##
* <font color="#0080FF">**使用 import 匯入**</font>

```python=+
import counter

print(counter.num)
counter.add()
print(counter.num)
```

> ```0```</br>
> ```1```
##
* <font color="#0080FF">**使用 from ... import ... 匯入**</font>

```python=+
from counter import num,add #直接掛在主程式命名空間中
print(num)
add()
print(num)

import counter
print(counter.num)
```

> ```0```</br>
> ```0```</br>
> ```1```

## (!)5.建立與內建函式同名的變數

* <font color="#0080FF">**(!)全域變數名稱覆蓋同名稱內建函式**</font>

```python=+
list('SUSHI RAMEN')
list = [1,3,5,7]

list('SUSHI RAMEN') #已被同名變數名稱覆蓋

del list #刪除全域命名空間的list
list('SUSHI RAMEN')
```

> ```['S', 'U', 'S', 'H', 'I', ' ', 'R', 'A', 'M', 'E', 'N']```</br>
> ```TypeError: 'list' object is not callable```</br>
> ```['S', 'U', 'S', 'H', 'I', ' ', 'R', 'A', 'M', 'E', 'N']```
##
* <font color="#0080FF">**相同名稱重複使用 (新值覆蓋舊值)**</font>

```python=+
import mymath #為先前撰寫的自訂模組

mymath = mymath.area # mymath參照到模組的 area 函式
mymath(3)
mymath.pi
```

> ```28.27431```</br>
> ```AttributeError: 'function' object has no attribute 'pi'```

## 6.其他常用及特殊的操作

* <font color="#0080FF">**用 dir() 列出模組內所有名稱**</font>

```python=+
dir(__builtins__)
```

> ```['ArithmeticError','AssertionError','AttributeError','BaseException','BlockingIOError','BrokenPipeError','BufferError','BytesWarning',...,'str','sum','super','tuple','type','vars','zip']```
##
* <font color="#0080FF">**查看函式內的說明文件**</font>

```python=+
help(max)
print(max.__doc__)
```

> ```Help on built-in function max in module builtins:```</br>
> ```max(...)```</br>
> ```    max(iterable, *[, default=obj, key=func]) -> value```</br>
> ``` max(arg1, arg2, *args, *[, key=func]) -> value```
> ```...```</br></br>
> ```max(iterable, *[, default=obj, key=func]) -> value```</br>
> ```max(arg1, arg2, *args, *[, key=func]) -> value```
> ```...```
##
* <font color="#0080FF">**(!)變數名稱偵錯**</font>

```python=+
x1 = 6
xl = x1 - 2 #左邊名稱將數字 1 誤打成英文字母 l 
x1

dir() #(注意!)在沒有參數的情況下傳回區域命名空間中的名稱

#最後面可以看到變數竟然有兩個!!
```

> ```6```</br>
> ```['In','Out','_','_1','_14',...,'mymath','quit','x1','xl']```

## 時間戳記

> [name=ZEOxO][time=Tue, Sep 1, 2020 15:13 PM][color=#907bf7]