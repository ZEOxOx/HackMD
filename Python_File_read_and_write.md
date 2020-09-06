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
* <font color="#0080FF">**用 For 迴圈逐行讀取檔案 ( 推薦，不會耗盡記憶體 )**</font>

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

## 2.寫入檔案

* <font color="#0080FF">**write() 寫入字串資料**</font>

```python=+
myfile.write('Hello\nWorld')
```
##
* <font color="#0080FF">**writelines() 寫入陣列資料**</font>

```python=+
#檔案內容複製( 驗證 writelines() 是 readlines() 的反函式 )
input_file = open(path,'r')
lines = input_file.readlines() #readlines為陣列格式
input_file.close()

print('>> 寫入output_file...\n內容 :',lines)

path = os.path.join(os.pardir,'document','myfile2.txt')
output_file = open(path,'w')
output_file.writelines(lines) # writelines不會在陣列中加入換行,必須手動

print('>> 寫入成功...')
output_file.close()
```

> ```>> 寫入output_file...```</br>
> ```內容 : ['Hello Python!!!!!!!!!\n', '!!!!!!!!!Hello Python\n', '!!!!Hello Python!!!!!']```</br>
> ```>> 寫入成功...```
## 
* <font color="#0080FF">**myfile.txt、myfile2.txt**</font>

```python=+
Hello Python!!!!!!!!!
!!!!!!!!!Hello Python
!!!!Hello Python!!!!!
```

## 3.讀取與寫入 - pathlib

* <font color="#0080FF">**建立 Path 物件處理文字檔與二進位檔**</font>

```python=+
from pathlib import Path
p_text = Path('my_text_file')
p_text.write_text('Text file contents') #傳回寫入的字串長度
p_text.read_text() #傳回字串內容

p_binary = Path('my_binary_file')
p_binary.write_bytes(b'Binary file contents') #傳回寫入的位元組長度
p_binary.read_bytes() #傳回位元組內容
```

> ```18```</br>
> ```Text file contents```</br>
> ```20```</br>
> ```b'Binary file contents'```

## 4.標準輸入 / 輸出與重新導向

* <font color="#0080FF">**將標準輸出「重新導向」及回復其原始值**</font>

```python=+
import sys,os
savedout = sys.stdout #(注意!)IDLE中sys.stdout初值為PseudoOutputFile物件，與sys.__stdout__並不相同
path = os.path.join(os.pardir,'document','outfile2.txt')
f = open(path,'w')

sys.stdout = f #將標準輸出「重新導向」到檔案
sys.stdout.writelines(['A first line.\n','A second line.\n'])
print('A line from the print function.')
3 + 4 #(注意!)在IDLE情況下，似乎無法寫入檔案

sys.stdout = savedout #將標準輸出回復為原始值
f.close()

print('Hello')
3 + 4
```

> ```Hello```</br>
> ```7```
##
* <font color="#0080FF">**不改變標準輸出，並重新導向至檔案**</font>

```python=+
import os
path = os.path.join(os.pardir,'document','outfile3.txt')
f = open(path,'w')

print('A first line.','\nA second line.',file = f) #這兩個字串會輸出到檔案物件f
pritn(3 + 4)
f.close()
3 + 4
```

> ```7```</br>
> ```7```

## 5.讀取結構化二進位資料

* <font color="#0080FF">**struct 模組**</font>

## 時間戳記

> [name=ZEOxO][time=Wed, Sep 6, 2020 14:34 PM][color=#907bf7]