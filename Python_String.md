# Python - 字串(String)

###### tags: `Python`

## 1.字串(String)

* <font color="#0080FF">**字串為字元序列**</font>

```python=+
x = "Hello"

print(x[0])
print(x[-1])
print(x[1:])
print(len(x))
```

> ```H```</br>
> ```o```</br>
> ```ello```</br>
> ```5```
##
* <font color="#0080FF">**字串物件修改**</font>

```python=+
x = "GoodBye~"
print(x,id(x))

x = x[:-1] #字串不能修改，會直接成為新物件
print(x,id(x))
```

> ```GoodBye~ 1928774669296```</br>
> ```GoodBye 1928774658672```

## 2.基本的字串操作(String)

* <font color="#0080FF">**連接多個字串**</font>

```python=+
x = "Hello " + "World"
print(x)

x = "Hello "  "World" #自動將多個空白相隔的字串連接在一起
print(x)
```

> ```Hello World```</br>
> ```Hello World```

## 3.特殊字元和轉義字元

* <font color="#0080FF">**基本轉義字元**</font>

| 類別 | 說明 |
| :------: | :-----------: |
| \\'  | 單引號(')|
| \\" | 雙引號(") |
| \\\\ | 反斜線(\\) |
| \\a | 發出嗶聲(Bell) |
| \\b | 倒退鍵(Backspace) |
| \\f | 換頁 |
| \\n | 換行 |
| \\r | 歸位符號(Carriage Return) |
| \\t | 定位符號(Tab) |
| \\v | 垂直定位符號(Vertical Tab) |
##
* <font color="#0080FF">**數值(八進位和十六進位)以及Unicode轉義字元**</font>

(SKIP)

## 4.字串常用的 Method 與函式

* <font color="#0080FF">**join()**</font>

```python=+
x = " ".join(['HI,','my','name','is','ZEOxO','!!'])
print(x)
```

> ```HI, my name is ZEOxO !!```
##
* <font color="#0080FF">**split()**</font>

```python=+
x = 'HI, \t\tmy \nname \tis \n\rZEOxO !!'
print(x.split()) #預設為切割空白字元(空格、換行、定位等)

x = 'Mississippi'
print(x.split('ss'))

x = 'a b c d'
print(x.split(' ',2))
print(x.split(' ',9))

x = 'a\nb c d'
print(x.split(' ',2)) #指定只切「空白」字元(不會切轉義字元)
print(x.split(None,2))
```

> ```['HI,', 'my', 'name', 'is', 'ZEOxO', '!!']```</br>
> ```['Mi', 'i', 'ippi']```</br>
> ```['a', 'b','c d']```</br>
> ```['a', 'b', 'c', 'd']```</br>
> ```['a\nb', 'c', 'd']```</br>
> ```['a', 'b', 'c d']```
##
* <font color="#0080FF">**float()**</font>

```python=+
float('123.456')
float('123')
float('xxyy')
```

> ```123.456```</br>
> ```123.0```</br>
> ```ValueError: could not convert string to float: 'xxyy'```
##
* <font color="#0080FF">**int()**</font>

```python=+
int('3333')
int('123.456') #不可有小數點

int('10000',8) #用8進位的基底來解釋10進位整數(10000)
int('101',2) #用2進位的基底來解釋10進位整數(101)
int('ff',16) #用16進位的基底來解釋10進位整數(ff)
int('123456',6) #6進位為「0~5」，不包含「6」
```

> ```3333```</br>
> ```ValueError: invalid literal for int() with base 10: '123.456'```</br>
> ```4096```</br>
> ```5```</br>
> ```255```</br>
> ```ValueError: invalid literal for int() with base 6: '123456'```
##
* <font color="#0080FF">**strip()、lstrip()、rstrip()**</font>

```python=+
x = ' Hello World\t\t'

x.strip()
x.lstrip()
x.rstrip()
```

> ```'Hello World'```</br>
> ```'Hello World\t\t'```</br>
> ```' Hello World'```
## 
* <font color="#0080FF">**strip() 指定字元**</font>

```python=+
x = 'www.python.org'

x.strip('w')
x.strip('.gorw')

x.strip("go")
x.strip("gr")
```

> ```.python.org```</br>
> ```python```</br>
> ```www.python.or```</br>
> ```www.python.o```
## 
* <font color="#0080FF">**isdigit()、isalpha()、islower()、isupper()**</font>

```python=+
x = '123'

x.isdigit()
x.isalpha()

x = 'MM'
x.islower()
x.isupper()
```

> ```True```</br>
> ```False```</br>
> ```False```</br>
> ```True```

## 5.字串的搜尋

* <font color="#0080FF">**in 算符**</font>

```python=+
x = 'The string'

print('str' in x)
print('sTr' in x)
print('e s' in x)
```

> ```True```</br>
> ```False```</br>
> ```True```
## 
* <font color="#0080FF">**find()、rfind()、index()、rindex()**</font>

```python=+
x = 'Mississippi'

print(x.find('is'))
print(x.find('zz')) #不存在傳回-1

print(x.find('s',2)) #從指定索引值開始搜尋
print(x.find('s',4,5)) #到指定索引值之前停止搜尋
print(x.find('ss',3))
print(x.find('ss',0,3))

print(x.rfind('ss'))
#index和rindex與find、rfind相同，但找不到文字時會引發例外錯誤
```
> ```1```</br>
> ```-1```</br>
> ```2```</br>
> ```5```</br>
> ```-1```</br>
> ```5```</br>
> ```-1```</br>
> ```5```
## 
* <font color="#0080FF">**count()**</font>

```python=+
x =  "Mississippi"

x.count('ss')
```

> ```2```
## 
* <font color="#0080FF">**startswith()、endswith()**</font>

```python=+
x =  "Mississippi"

print(x.startswith('Miss'))
print(x.startswith('Mist'))

print(x.endswith('pi'))
print(x.endswith('p'))
print(x.endswith(('i','u'))) #可以tuple形式傳入多筆搜尋文字
```

> ```True```</br>
> ```False```</br>
> ```True```</br>
> ```False```</br>
> ```True```

## 6.字串的修改

* <font color="#0080FF">**replace()**</font>

```python=+
x =  "Mississippi"
x.replace('ss','zzz')
```

> ```'Mizzzizzzippi'```
##
* <font color="#0080FF">**maketrans()、translate()**</font>

```python=+
x = '~x ^ (y % z)'

table = x.maketrans('~^()','!&[]')
x.translate(table)
```

> ```'!x & [y % z]'```
## 
* <font color="#0080FF">**capitalize()、title()**</font>

```python=+
x = 'hi, my name is ZEOxO !!'

print(x.capitalize()) #將字串的第一個字元為大寫、其餘小寫
print(x.title()) #將所有單字的第一個字元為大寫、其餘小寫
```

> ```Hi, my name is zeoxo !!```</br>
> ```Hi, My Name Is Zeoxo !!```

* <font color="#0080FF">**swapcase()、expandtabs()**</font>

```python=+
x = 'hi,\tmy\tname\tis\tZEOxO !!'

print(x.swapcase()) #將字串內所有字母大寫轉小寫、小寫轉大寫
print(x.expandtabs(1)) #將字串內定位符號轉為指定數目的空格(如1個空格)
```

> ```HI,	　MY	　NAME	　is 　zeoXo !!```</br>
> ```hi, my name is ZEOxO !!```

* <font color="#0080FF">**ljust()、rjust()**</font>

```python=+
x = 'Hello World'

print(x.ljust(20,'!'))
print(x.rjust(20,'!'))
print(x.center(20,'!'))
```

> ```Hello World!!!!!!!!!```</br>
> ```!!!!!!!!!Hello World```</br>
> ```!!!!Hello World!!!!!```

## 7.其他常用及特殊的 String 操作

* <font color="#0080FF">**repr()、str()將物件轉換成字串表示**</font>

```python=+
repr([1,2,3])

x = [1]
x.append(2)
x.append([3,4])
'the list x is ' + repr(x)
```

> ```'[1, 2, 3]'```</br>
> ```'the list x is [1, 2, [3, 4]]'```
##
* <font color="#0080FF">**repr() 傳入物件參數a**</font>
> <font color="#EA0000">**(!)repr非常適合用來程式除錯**</font>

```python=+
repr(len) #將系統內建方法、物件作為參數傳入
```

> ```'< built-in function len >'```
##
* <font color="#0080FF">**repr() 傳入物件參數b**</font>

```python=+
from datetime import datetime
now = datatime.now()


now
str(now)
repr(now)
```

> ```'2020-08-26 15:18:40.695042'```</br>
> ```'2020-08-26 15:18:40.695042'```</br>
> ```'datetime.datetime(2020, 8, 26, 15, 18, 40, 695042)'```
## 
* <font color="#0080FF">**指名參數格式化輸出(字典)**</font>

```python=+
"NO.{rank} is {name}!!".format(name = 'ZEOxO',rank = '1')
```

> ```'NO.1 is ZEOxO!!'```
## 
* <font color="#0080FF">**指名參數格式化輸出(陣列)**</font>

```python=+
"User name:{info[0]} ID:{info[1]} addr:{info[2]}".format(info = ['ZEOxO','123456','Taipei'])
```

> ```'User name:ZEOxO ID:123456 addr:Taipei'```

## 8.Python 字串模組

* <font color="#0080FF">**(!)被 Python 定義的空白字元**</font>

```python=+
import string
string.whitespace #可透過存取「string.whitespace」常數找到

' \t\n\r\v\f'
```

> ```' \t\n\r\x0b\x0c'```</br>
> ```' \t\n\r\x0b\x0c'```

##
* <font color="#0080FF">**(!)其他被 Python 定義的字元**</font>

```python=+
import string

string.digits
string.hexdigits
string.octdigits
string.ascii_lowercase
string.ascii_uppercase
string.ascii_letters #包含lowercase和uppercase所有字元
```

> ```'0123456789'```</br>
> ```'0123456789abcdefABCDEF'```</br>
> ```'01234567'```</br>
> ```'abcdefghijklmnopqrstuvwxyz'```</br>
> ```'ABCDEFGHIJKLMNOPQRSTUVWXYZ'```</br>
> ```'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'```

## 時間戳記

> [name=ZEOxO][time=Wed, Aug 26, 2020 16:00 PM][color=#907bf7]