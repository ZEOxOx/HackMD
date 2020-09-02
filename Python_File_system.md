# Python - 檔案系統

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

## 2.檔案系統操作

* <font color="#0080FF">**依照作業系統建立路徑**</font>

```python=+
path1 = os.path.join('mydir','bin')
path2 = os.path.join('utils','disktools','chkdisk')
print(os.path.join(path1,path2)) #為了可攜性，較長的檔案路徑應如此連接
```

> ```mydir\bin\utils\disktools\chkdisk```