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

globals() #增加了一些新的數值
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

* <font color="#0080FF">**名稱的可視範圍**</font>

```python=+
import scopetest

z = 2
scopetest.f(z)
#命名空間不包含交談模式中建立的變數z，因此無須擔心
#模組外部的名稱會影響內部程式碼的運作
```

> ```global:  ['__name__', '__doc__', '__package__', '__loader__', '__spec__', '__file__', '__cached__', '__builtins__', 'v', 'f']```</br>
> ```進入 local:  {'x': 2}```</br>
> ```離開 local:  dict_keys(['x', 'y', 'w'])```