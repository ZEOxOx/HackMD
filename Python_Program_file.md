# Python - 程式檔

###### tags: `Python`

## 1.主程式、函式

* <font color="#0080FF">**將主程式放入主控函式**</font>

```python=+
def compare_num_of_chars(st):
    return len(st)

def main():
    word_list = ['SUSHI','RAMEN']
    word_list.sort(key = compare_num_of_chars)
    
main()
```
## 
* <font color="#0080FF">**從命令列執行 Python 程式檔**</font>

**>> SKIP**

## 2.輸入和輸出重導與管線

<font color="#0080FF">**replace.py**</font>

```python=+
import sys
def main():
    contents = sys.stdin.read() #會從標準輸入讀取字串
    sys.stdout.write(contents.replace(sys.argv[1],sys.argv[2]))
    #將傳入函式的參數值送到標準輸出
main()
```
##
* <font color="#0080FF">**控制標準輸入 / 輸出(命令列參數)**</font>

## 時間戳記

> [name=ZEOxO][time=Tue, Sep 1, 2020 16:49 PM][color=#907bf7]