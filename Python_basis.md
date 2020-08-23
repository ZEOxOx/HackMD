# Python - 基礎篇

## 1.變數及其設定 Assignment

* <font color="#0080FF">**變數名稱參照到不同型別物件(不推薦，易混淆)**</font>

```python=+
#變數名稱參照到字串
x = 'Hello'
print(x,type(x))

#變數名稱參照到數字
x = 5
print(x,type(x))
```

> ```Hello <class 'str'>```
> ```5 <class 'int'>```

## 2.數字

* <font color="#0080FF">**整數、浮點數、複數、布林值**</font>

```python=+
5 + 2 - 3 * 2
5 / 2
5 / 2.0
5 // 2 #取整數
5.0 // 2 #取整數再轉浮點數

int(200.2)
int(2e2)
float(200)
```

> ```1```
> ```2.5```
> ```2.5```
> ```2```
> ```2.0```
> ```200```
> ```200.0```
> ```200.0```

## 3.字串

* <font color="#0080FF">**長字串a**</font>

```python
#使用「"""」的缺點是會將換行字元也包含進來
long_string = 'Lions are often called the "king of the' \
'beasts". They are used as symbols representing courage.' \
'They appear in heraldry more often than any other animal.' \
'They are an icon of courage and royalty.'

#注意:「\」後面要直接換行，不得有空格或其他字元
print(long_string)
```

> ```Lions are often called the "king of thebeasts". ``` 
> ```They are used as symbols representing courage.```
> ```They appear in heraldry more often than any other ```
> ```animal.They are an icon of courage and royalty.```
##
* <font color="#0080FF">**長字串b**</font>

```python=+
long_string = (
'Lions are often called the "king of the' 
'beasts". They are used as symbols representing courage.' 
'They appear in heraldry more often than any other animal.' 
'They are an icon of courage and royalty.')

#Python會將括弧內的敘述視為一行
print(long_string)
```

> ```Lions are often called the "king of thebeasts". ``` 
> ```They are used as symbols representing courage.```
> ```They appear in heraldry more often than any other ```
> ```animal.They are an icon of courage and royalty.```

## 4.複數

* <font color="#0080FF">**複數計算**</font>

```python=+
3 + 2j
3 + 2j - (4+4j)
(1+2j) * (3+4j)
1j * 1j

#Python會用括弧來顯示複數的運算結果，表示是單一物件的值
z = (3+5j)
print(z.real)
print(z.imag)
```

> ```(3+2j)```
> ```(-1-2j)```
> ```(-5+10j)```
> ```(-1+0j)```
> ```3.0```
> ```5.0```
##
* <font color="#0080FF">**進階的複數函式(cmath模組)**</font>

```python=+
#math模組中的函式不支援複數，理由是使用者希望計算-1的平方根結果
#會產生一個錯誤，而不是1j這種答案!(改用cmath模組進行複數運算)
from math import *
sqrt(-1)

#用「import *」會使cmath中的函式覆蓋掉math模組的同名函式(如sqrt)
from cmath import *
sqrt(-1)
```

> ```ValueError```
> ```<ipython-input-26-cb0fd01d820b> in <module>```
> ``` 　　　36 from math import *```
> ```----> 37 sqrt(-1)```
> ```ValueError: math domain error```
> ```1j```

## 5.None值

* <font color="#0080FF">**None值**</font>

```python=+
None == False
None == 0
#「None」只等於自己
None == None

#「False」等於0
False == 0
bool(0)
```

> ```False```
> ```False```
> ```True```
> ```True```
> ```False```

## 6.基本Python風格與命名慣例

* <font color="#0080FF">**底線開頭或結尾的名稱**</font>
> <font color="#EA0000">**Py之父 Guido van Rossum 的一個重要見解是:『閱讀程式碼的頻率遠高於撰寫』**</font>

| 類別 | 說明 |
| :------: | :-----------: |
| _前單底線   | 模組的私有變數或函式，用*匯入模組時無法匯入以(_底線)開頭的名稱</p>類別或物件的私有變數或方法，外部仍然可以存取|
| __前雙底線 | 類別或物件的私有變數或方法，會被 Python 改名，外部無法直接使用原本名稱存取 |
| 前後雙底線  | 保留給 Python 內部使用的名稱，請避免使用 |
| 後單底線_  | 避免與 Python 關鍵字衝突。如想用 str 這個名稱，可取名為 str_ |
| 單底線(_)  | 不重要、暫時性的資料 |