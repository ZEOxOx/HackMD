# k.Python - 檔案系統(File System)

###### tags: `Python`

## 1.工作目錄

* <font color="#0080FF">**取得目前工作目錄**</font>

```python=+
import os
os.getcwd()
```

>```'C:\\Users\\tonyc\\pythonwork\\Python_dev'```
##
* <font color="#0080FF">**取得目前工作目錄 - pathlib**</font>

```python=+
import pathlib
cur_path = pathlib.Path() #建立路徑物件
cur_path.cwd()
```

>```WindowsPath('C:/Users/tonyc/pythonwork/Python_dev')```

##
* <font color="#0080FF">**工作目錄下的子目錄與檔案清單**</font>

```python=+
os.listdir(os.curdir) #os.curdir 會傳回「目前目錄」的符號
#務必使用 os.curdir 而不是 '.' 確保同一份程式碼才可在不同系統運作
```

> ```['.ipynb_checkpoints','File_System(2020_0902).ipynb','Module(2020_0831).ipynb','namespace(2020_0831).ipynb','Program_File(2020_0901).ipynb',...]```
## 
* <font color="#0080FF">**切換目前工作目錄**</font>

```python=+
os.chdir("C:\\") #注意要兩個反斜線
os.getcwd()
```

>```'C:\\'```
## 
* <font color="#0080FF">**Windows 系統下的路徑**</font>

```python=+
os.chdir('C:\\Windows\\temp')
os.chdir('C:/Windows/temp') #這兩種路徑在 Windows 都可以使用
```

>```'C:\\'```

## 2.檔案系統操作(import os)

* <font color="#0080FF">**os.path.join() 依照作業系統自動建立路徑**</font>

```python=+
import os
path1 = os.path.join('mydir','bin')
path2 = os.path.join('utils','disktools','chkdisk')
print(os.path.join(path1,path2)) #為了可攜性，較長的檔案路徑應如此連接
```

> ```mydir/bin/utils/disktools/chkdisk```

##
* <font color="#0080FF">**os.path.split()**</font>

```python=+
print(os.path.split(os.path.join('some','directory','cat.jpg')))
#split會將basename與其他路徑切割開來，並傳回tuple
#basename:路徑最後指向的資料夾或檔案名稱
```

> ```('some\\directory', 'cat.jpg')```
## 
* <font color="#0080FF">**os.path.basename()、os.path.dirname()**</font>

```python=+
#取得檔案或資料夾名稱
os.path.basename(os.path.join('some','directory','cat.jpg'))
#取得路徑中不包括basename的部分
os.path.dirname(os.path.join('some','directory','cat.jpg'))
```

> ```'cat.jpg'```</br>
> ```'some\\directory'```
## 
* <font color="#0080FF">**os.path.splitext()**</font>

```python=+
#取得副檔名
os.path.splitext(os.path.join('some','directory','cat.jpg'))
```

> ```('some\\directory\\cat', '.jpg')```
## 
* <font color="#0080FF">**os.path.abspath()**</font>

```python=+
#取得絕對路徑
os.path.abspath(os.path.join('some','directory','cat.jpg'))
```

> ```'C:\\Users\\tonyc\\pythonwork\\Python_dev\\some\\directory\\cat.jpg'```
## 
* <font color="#0080FF">**os.path.commonprefix()**</font>

```python=+
#找出多個檔案的共通目錄
os.path.commonprefix(['C:\\temp\\a.jpg','C:\\temp\\b.jpg'])
```

> ```'C:\\temp\\'```
## 
* <font color="#0080FF">**os.path.expanduser()**</font>

```python=+
#將路徑中「~」符號轉換為使用者個人資料夾
os.path.expanduser('~\\temp')
```

> ```'C:\\Users\\tonyc\\temp'```

## 3.檔案系統操作 - pathlib

* <font color="#0080FF">**路徑名稱處理**</font>

```python=+
from pathlib import Path
cur_path = Path() #建立路徑物件
print(cur_path.joinpath('bin','utils','disktools'))

#pathlib 路徑物件支援「/」算符，可得到上面同樣的效果
cur_path / 'bin' / 'utils' / 'disktools'
```

> ```bin\utils\disktools```</br>
> ```WindowsPath('bin/utils/disktools')```
##
* <font color="#0080FF">**將所有資料夾或檔案拆開**</font>

```python=+
a_path = Path('bin/utils/disktools')
print(a_path.parts)
```

> ```('bin', 'utils', 'disktools')```
##
* <font color="#0080FF">**相對路徑轉為絕對路徑**</font>

```python=+
a_path = Path('.')
a_path.resolve()
```

> ```WindowsPath('C:/Users/tonyc/pythonwork/Python_dev')```
##
* <font color="#0080FF">**取得路徑、basename、副檔名**</font>

```python=+
a_path = Path('some','directory','path.jpg')

a_path.name #取得basename
print(a_path.parent) #取得不包含basename的路徑
a_path.suffix #取得副檔名
```

> ```'path.jpg'```</br>
> ```some\directory```</br>
> ```'.jpg'```

## 4.有用的操作與函式

* <font color="#0080FF">**os.pardir (parent) 上層目錄、os.curdir (current) 當前目錄**</font>
 
```python=+
os.path.join('C:\\Windows\\temp',os.pardir,os.curdir)

#檢查路徑的終點是否為目錄
os.path.isdir(os.path.join('C:\\Windows\\temp',os.pardir,os.curdir))
```

> ```'C:\\Windows\\temp\\..\\.' #此路徑實際指向 C:\Windows```</br>
> ```True```
##
* <font color="#0080FF">**os.name 作業系統名稱**</font>

```python=+
import os
os.name #大多數 Windows 作業系統都被標識為「nt」
```

> ```'nt'```
##
* <font color="#0080FF">**(!)利用 os.name 決定根目錄的形式**</font>

```python=+
import os
if os.name == 'posix': #「OS X」或「Linux / UNIX」
    root_dir = '/'
elif os.name == 'nt': #除了「Windows CE」以外大部分版本
    root_dir = "C:\\"
else:
    print("無法判定目前所處的作業系統!!")
```
##
* <font color="#0080FF">**sys.platform 更精確的作業系統名稱**</font>

```python=+
import sys
sys.platform #只要是 win10 都會顯示 'win32'(執行64位元也一樣)
```
> ```'win32'```
##
* <font color="#0080FF">**查看Shell環境變數**</font>

```python=+
import os
os.environ['PATH'] #可用來設定執行檔的搜尋路徑
```

> ```'C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu;C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu\\Library\\mingw-w64\\bin;C:\\Users\\tonyc\\anaconda3\\envs\\tensorflow-gpu\\Library\\usr\\bin;```
> ```...```

## 時間戳記

> [name=ZEOxO][time=Wed, Sep 3, 2020 20:53 PM][color=#907bf7]