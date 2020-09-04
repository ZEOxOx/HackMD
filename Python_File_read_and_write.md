# Python - 檔案讀寫

###### tags: `Python`

## 1.開啟檔案

* <font color="#0080FF">**絕對路徑、讀取**</font>

```python=+
import os
file_name = os.path.join('C:\\','Users','tonyc','pythonwork','document','test.txt')

with open(file_name,'r') as file:
    line = file.readline() #讀取一整行(包含「\n」)
    print(line)
```

> ```Hello World!!!!!!!!!```</br>
> ``` ```
##
* <font color="#0080FF">**寫入模式**</font>

```python=+
file = open('C:\\Users\\tonyc\\pythonwork\\document\\hello.txt','w')
file.write('Hello World!')
file.close()
```

<font color="#0080FF">**hello.txt**</font>

```python=+
Hello World!
```
##
* <font color="#0080FF">**附加模式**</font>

```python=+
file = open('C:\\Users\\tonyc\\pythonwork\\document\\hello.txt','a')
file.write('\nHello Python!')
file.close()
```

<font color="#0080FF">**hello.txt**</font>

```python=+
Hello World!
Hello Python!
```
##
* <font color="#0080FF">**編碼格式 encoding**</font>

> <font color="#EA0000">**open()函式會以作業系統預設編碼來開啟檔案，而繁體中文 Windows 預設編碼格式為「cp950」。通常都會改設為「utf-8」和「utf-8-sig」( 大小寫均可，「-」可換成「_」)</br></br>utf-8-sig : 檔案最前面加上BOM( Byte-order mark )，以便辨識此檔案的編碼方式，不過若軟體、程式不支援則會變成亂碼**</font>

## 2.讀寫文字檔和二進位檔案

* <font color="#0080FF">**readline() 讀取一行**</font>

```python=+
file = open('C:\\Users\\tonyc\\pythonwork\\document\\test.txt','r')
count = 0
while file.readline() != '':
    #計算檔案行數
    count += 1
print(count)
file.close()
```

> ```3```
##
* <font color="#0080FF">**readlines() 讀取所有行**</font>

```python=+
file = open('C:\\Users\\tonyc\\pythonwork\\document\\test.txt','r')
print(len(file.readlines()))
file.close() #readline 和 readlines 皆可用參數指定每次讀取資料量
```

> ```3```
##
* <font color="#0080FF">**用 For 迴圈逐行讀取檔案**</font>

```python=+
file = open('C:\\Users\\tonyc\\pythonwork\\document\\test.txt','r')
count = 0
for line in file: #會包含換行符號
    print(line)
file.close()
```

> ```Hello World!!!!!!!!!```</br>
> ``` ```</br>
> ```!!!!!!!!!Hello World```</br>
> ``` ```</br>
> ```!!!!Hello World!!!!!```</br>
> ``` ```
##
* <font color="#0080FF">**處理換行符號**</font>

```python=+
#強制只將「\n」視為換行符號 (關閉自動轉換功能)
input_file = open('myfile',newline = '\n')
```
