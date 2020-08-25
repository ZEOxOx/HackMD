# Python - 字串(String)

## 1.字串(String)

* <font color="#0080FF">**字串為字元序列**</font>

```python=+
x = "Hello"

print(x[0])
print(x[-1])
print(x[1:])
print(len(x))
```

> ```H```
> ```o```
> ```ello```
> ```5```
##
* <font color="#0080FF">**字串物件修改**</font>

```python=+
x = "GoodBye~"
print(x,id(x))

x = x[:-1] #不能修改，直接成為新的字串
print(x,id(x))
```

> ```GoodBye~ 1928774669296```
> ```GoodBye 1928774658672```

## 2.基本的字串操作(String)

* <font color="#0080FF">**連接多個字串**</font>

```python=+
x = "Hello " + "World"
print(x)

x = "Hello "  "World" #自動將多個空白相隔的字串連接在一起
print(x)
```

> ```Hello World```
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