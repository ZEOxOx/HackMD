# g.Python - 函式(Function)

> <font color="#EA0000">**在某些程式語言中，沒有傳回值的就稱為「程序(Procedure)」，有回傳的就稱為「函式(Function)」**</font>

> <font color="#EA0000">**但在Python中均稱為「函式(Function)」，如果函式沒有return，則會自動傳回'None'**</font>

###### tags: `Python`

## 1.函式的進階

* <font color="#0080FF">**用可變物件(mutable)作為引數**</font>

```python=+
def func(n,list1,list2):
    list1.append(3) #(更改陣列)
    list2 = [4,5,6] #(建立變數)
    n = n + 1 #(建立變數)

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
* <font color="#0080FF">**<!>用可變物件作為參數預設值的問題**</font>

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
* <font color="#0080FF">**<!>用可變物件作為參數預設值的問題(續)**</font>

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

## 2. * 和 ** 的參數

* <font color="#0080FF">**'*' 用來接收多個引數 (打包成Tuple)**</font>

```python=+
def maximum(*num):
    if len(num) == 0:
        return None
    else:
        maxNum = num[0]
        for n in num:
            if n > maxNum:
                maxNum = n
        return maxNum
    
maximum(1,3,5,4,2) #多個引數
maximum() #沒有引數也可以
```

> ```5```</br>
> ``` ```
##
* <font color="#0080FF">**<!> ** 用來接收多個指名引數 (打包成字典)**</font>

```python=+
def exam(x,*y,**other):
    result = ("x:{0}, y:{1} ,字典 'other' 內的鍵: {2}").format(x,y,list(other.keys()))
    return result
    
exam(2,3,4,foo=3,bar=5)  #多個指名引數
```

> ```x:2, y:(3, 4) ,字典 'other' 內的鍵: ['foo', 'bar']```

## 3.Lambda 匿名函式

* <font color="#0080FF">**lambda 匿名函式**</font>

```python=+
tt = {'FtoK':lambda deg_f:273.15 + (deg_f - 32) * 5/9,
      'CtoK':lambda deg_c:273.15 + deg_c}

print(tt['FtoK'](32)) #從字典查到'FtoK'這個key的值是lambda函式
print(tt['CtoK'](0)) #透過tt['CtoK']取得lambda函式
```

> ```273.15```</br>
> ```273.15```
##
* <font color="#0080FF">**lambda 匿名函式(續)**</font>

```python=+
word_list = ['Python','is','better','than','C']

word_list.sort(key = lambda s:len(s))
#word_list.sort(key = len) #這樣寫其實更好，因此濫用lambda可能影響程式可讀性
word_list
```

> ```['C', 'is', 'than', 'Python', 'better']```

## 4.Generator 產生器(走訪器)函式

* <font color="#0080FF">**Yield 關鍵字傳回每次走訪的值**</font>

```python=+
def four():
    x = 0
    while x < 4:
        yield x
        x += 1
    
four() #產生器(走訪器)是特殊函式，要搭配For迴圈使用

list(four())
2 in four() #可搭配'in'使用
```

> ```<generator object four at 0x7ff72944fad0>```</br>

> ```[0, 1, 2, 3]```</br>
> ```True```

## 
* <font color="#0080FF">**Yield 與 Yield from (自編範例)**</font>

```python=+
#yield from敘述從主產生器移到副產生器
def subgen(x):
    ls = [] 
    for i in range(x):
        ls.append(i)
        yield ls #yield會在函式執行中回傳，因此ls不會消失
        
#主產生器
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

## 5.Decorator 修飾器函式

* <font color="#0080FF">**修飾器(原始函式)**</font>

> <font color="#EA0000">**當你想為函式新增功能，卻不想更動函式原始碼的情況下，就非常推薦使用修飾器!!**</font>

> <font color="#EA0000">**函式是 Python 的 first-class object(第一級物件)，</br>因此我們可以將函式指定給變數，也可作為引數傳遞給其他函式，甚至當作傳回值**</font>

```python=+
def friedchicken():
    return 49.0

print(friedchicken()) #49.0
```

>```49.0```
##
* <font color="#0080FF">**<!>修飾器(新增功能)**</font>

```python=+
def sidedish1(meal):
    return lambda: meal() + 30 #回傳為函式(lambda)
    #return meal() + 30 #這樣寫會變成回傳數值(float)

def friedchicken():
    return 49.0

#修飾器敘述
friedchicken = sidedish1(friedchicken) #(!)注意 friedchicken 還是一個函式!!
print(friedchicken()) #新的friedchicken函式
```

>```79.0```
##
* <font color="#0080FF">**<!>修飾器(語法糖)**</font>

```python=+
def sidedish1(meal):
    return lambda: meal() + 30

@sidedish1 #等同「friedchicken = sidedish1(friedchicken)」
def friedchicken():
    return 49.0

print(friedchicken()) #新的friedchicken函式
```

>```79.0```

## 6.global、local、nonlocal變數

**(SKIP)**

## 時間戳記

> [name=ZEOxO][time=Mon, Aug 30, 2020 23:00 PM][color=#907bf7]