# o.Python - 常規表達式(regular_expression)

###### tags: `Python`

## 1.常規表達式基礎

<font color="#0080FF">**hello.txt**</font>

```python=+
Hello World!
Hello Python!
```
##
* <font color="#0080FF">**(續)給予特定字串樣式做配對**</font>

```python=+
import re,os
regexp = re.compile('Hello') #指定字串樣式
count = 0

path = os.path.join(os.pardir,'document','hello.txt')
file = open(path,'r')
print('開啟檔案 :',path)

for line in file:
    if regexp.search(line): #尋找該字串內是否有指定字串
        count = count + 1
file.close()

print('>> 共找到',count,'行包含有 "Hello"')
```

> ```開啟檔案 : ..\document\hello.txt```</br>
> ```>> 共找到 2 行包含有 "Hello"```
## 
* <font color="#0080FF">**(!)具有特殊字元的常規表達式**</font>

```python=+
#下列三個表達式意思都一樣
regexp = re.compile('Hello|hello')
regexp = re.compile('(H|h)ello')
regexp = re.compile('[Hh]ello') #推薦，不用寫一堆「|」

#要找「-」字元必須寫在前面。如 [-012]代表 -、0、1、2
#[0-12]則變成 0~1、2
```

## 2.轉義字元與原始字串

* <font color="#0080FF">**含有轉義字元的常規表達式**</font>

```python=+
# 在re.compile中轉義字元將會先被替換
regexp = re.compile('第一行\n第二行')
'''
第一行
第二行
'''
regexp = re.compile('\\\\ten')
'''\\ten'''
```
##
* <font color="#0080FF">**使用原始字串避免轉義字元的問題**</font>

```python=+
r'Hello'
r'''12345'''

r'\the' == '\\the'
print('\the')
print(r'C:\\some\\directory\\cat.jpg') #搜尋指定目錄或檔案
```

> ```'Hello'```</br>
> ```'12345'```</br>
> ```True```</br>
> ```	he```</br>
> ```C:\\some\\directory\\cat.jpg```

## 時間戳記

> [name=ZEOxO][time=Wed, Sep 9, 2020 17:40 PM][color=#907bf7]