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

## 2.輸入和輸出重導與管線

* <font color="#0080FF">**標準輸入 / 輸出**</font>

> <font color="#EA0000">**一般標準輸出與錯誤輸出的對象為「螢幕」，所以通常會在螢幕上看到程式執行的所有訊息。而標準輸入為接受使用者指令或訊息的來源，通常設定為鍵盤。**</font>
##
* <font color="#0080FF">**輸出入重導**</font>

> <font color="#EA0000">**是將標準輸入、標準輸出與錯誤輸出的來源或對象，重新導向其他裝置或檔案。**</font>

| 類別 | 說明 |
| :------: | :-----------: |
| 輸入重導符號 "<" | 可以讀取檔案內容 |
| 輸出重導符號 ">" | 將結果輸出到檔案中(覆蓋) |
| 輸出重導符號 ">>" | 將結果輸出到檔案中(附加) |
| 管線符號 "l" | 將一個程式的輸出作為另一個程式的輸入 |

## 3.檔案重新導向 - 覆寫(只適用於命令提示視窗)

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
* <font color="#0080FF">**建立 infile.txt**</font>

```python=+
zero plus any integer is an integer.
Example : 0 + 1 = 1
```
##
* <font color="#0080FF">**命令列參數控制標準輸入 / 輸出**</font>

```python=+
#將 infile.txt 中「zero」替換為「0」並輸出為 outfile.txt
py mymodule/replace.py zero 0 < infile.txt > outfile.txt
```
##
* <font color="#0080FF">**輸出到 outfile.txt**</font>

```python=+
0 plus any integer is an integer.
Example : 0 + 1 = 1
```

## 4.檔案重新導向 - 附加(只適用於命令提示視窗)

* <font color="#0080FF">**命令列參數控制標準輸入 / 輸出**</font>

```python=+
#將 infile.txt 中「a」替換為「A」並輸出為 outfile.txt
py mymodule/replace.py a A < infile.txt >> outfile.txt
```
##
* <font color="#0080FF">**輸出到 outfile.txt**</font>

```python=+
0 plus any integer is an integer.
Example : 0 + 1 = 1
zero plus Any integer is An integer.
ExAmple : 0 + 1 = 1
```

## 5.檔案重新導向 - 管線(只適用於命令提示視窗)

* <font color="#0080FF">**命令列參數控制標準輸入 / 輸出**</font>

```python=+
#先把「0」改為「zero」，再把「1」改為「one」
py mymodule/replace.py 0 zero < infile.txt | py mymodule/replace.py 1 one > outfile.txt
```
##
* <font color="#0080FF">**輸出到 outfile.txt**</font>

```python=+
zero plus any integer is an integer.
Example : zero + one = one
```

## 時間戳記

> [name=ZEOxO][time=Wed, Sep 2, 2020 21:44 PM][color=#907bf7]

