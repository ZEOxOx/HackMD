# Python - 命名空間(namespace)

###### tags: `Python`

## 1.命名空間

* <font color="#0080FF">**三種類型的命名空間**</font>

| 類別 | 說明 |
| :------: | :-----------: |
| 內建(builtin)| Python解釋器進行時，會建立一個名為 __ builtin __ 的模組，此模組包含所有內建函式，例如 len()、min()、max()、str() 等 |
| 全域(global) | 建立其他模組時，模組所帶的命名空間被稱為全域命名空間，放在這個空間中的變數即為「全域變數」。 |
| 區域(local)  | 呼叫函式時，Python 會為這個函式建立一個區域命名空間，</br>放在這個空間中的變數即為「區域變數」。</br>函式結束後，這個命名空間會隨之刪除 |
##
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
```

> ```{'__name__': '__main__',...,'_i': 'del z,math,cos','_ii': 'z = 2\nimport math\nfrom cmath import cos\n\nglobals()','_iii': 'globals()','_i1': 'locals()','_1': {...},'_i2': 'globals()','_2': {...},'_i3': 'z = 2\nimport math\nfrom cmath import cos\n\nglobals()','_3': {...},'_i4': 'del z,math,cos','_i5': 'globals()'}```
> 
> ```NameError: name 'math' is not defined```