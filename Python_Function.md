# g.Python - 函式(Function)

###### tags: `Python`

## 1.特殊應用及進階技巧

* <font color="#0080FF">**用可變物件(mutable)作為引數**</font>

```python=+
def func(n,list1,list2):
    list1.append(3)
    list2 = [4,5,6]
    n = n + 1

x = 5
y = [1,2]
z = [4,5]
func(x,y,z)
x,y,z #打包成tuple
```

> ```(5, [1, 2, 3], [4, 5])```
##
* <font color="#0080FF">**傳入可變物件如何不影響函式外部**</font>

```python=+
def func(list1):
    ls = list1[:] #在函式內複製一份可變物件即可
    ls.append(3)

x = [1,2]
func(x)
x
```

> ```[1, 2]```
## 
* <font color="#0080FF">**(!)用可變物件作為參數預設值的問題**</font>

```python=+
def data_append(v,ls = []):
    #ls參照到可變的list物件，這個變數並不會隨著函式結束被刪除
    ls.append(v)
    return ls

data_append(3)
data_append(5)
```

> ```[3]```</br>
> ```[3,5]```
## 
* <font color="#0080FF">**(!)(續)用可變物件作為參數預設值的問題**</font>

```python=+
def data_append(v,ls = None):
    #不要預設ls參照到可變物件即可
    if(ls == None):
        ls = []
    ls.append(v)
    return ls

data_append(3) 
data_append(5) #不會有殘留值了
```

> ```[3]```</br>
> ```[5]```

## 2.Lambda 匿名函式

* <font color="#0080FF">**lambda 匿名函式**</font>

```python=+
tt = {'FtoK':lambda deg_f:273.15 + (deg_f - 32) * 5/9,
      'CtoK':lambda deg_c:273.15 + deg_c}

print(tt['FtoK'](32))
print(tt['CtoK'](0))
```

> ```273.15```</br>
> ```273.15```

## 3.Generator 產生器(走訪器)函式

* <font color="#0080FF">**Yield 關鍵字傳回每次走訪的值**</font>

```python=+
def four():
    x = 0
    while x < 4:
        print("in generator, x = ",x)
        yield x
        x += 1
    
for i in four():
    print(i) #產生器(走訪器)是特殊函式，要搭配For迴圈使用
```

> ```in generator, x =  0```</br>
> ```0```</br>
> ```in generator, x =  1```</br>
> ```1```</br>
> ```in generator, x =  2```</br>
> ```2```</br>
> ```in generator, x =  3```</br>
> ```3```
## 
* <font color="#0080FF">**Yield 與 Yield from (自編範例)**</font>

```python=+
#yield敘述從主產生器移到副產生器
def subgen(x):
    ls = [] 
    for i in range(x):
        ls.append(i)
        yield ls #yield會在函式執行中回傳，因此ls不會消失
        
def gen(y):
    #執行subgen(6)並取得回傳值
    yield from subgen(y)

for q in gen(6):
    #從這裡開始
    print(q)
```

> ```[0]```</br>
> ```[0, 1]```</br>
> ```[0, 1, 2]```</br>
> ```[0, 1, 2, 3]```</br>
> ```[0, 1, 2, 3, 4]```</br>
> ```[0, 1, 2, 3, 4, 5]```</br>

## 4.Decorator 修飾器函式

* <font color="#0080FF">**修飾器(原始函式)**</font>

> <font color="#EA0000">**當你想為函式新增功能，卻不想更動函式原始碼的情況下，就非常推薦使用修飾器!!**</font>

```python=+
def friedchicken():
    return 49.0

print(friedchicken()) #49.0
```

>```49.0```
##
* <font color="#0080FF">**修飾器(新增功能)**</font>

```python=+
def sidedish1(meal):
    return lambda: meal() + 30

def friedchicken():
    return 49.0

#修飾器敘述
friedchicken = sidedish1(friedchicken) 
print(friedchicken()) #新的friedchicken函式
```

>```79.0```
##
* <font color="#0080FF">**(!)修飾器(語法糖)**</font>

```python=+
def sidedish1(meal):
    return lambda: meal() + 30

@sidedish1 #等同「friedchicken = sidedish1(friedchicken)」
def friedchicken():
    return 49.0

print(friedchicken()) #新的friedchicken函式
```

>```79.0```

## 5.local、global、nonlocal變數

**(SKIP)**

## 時間戳記

> [name=ZEOxO][time=Mon, Aug 30, 2020 23:00 PM][color=#907bf7]