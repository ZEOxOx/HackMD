# Python - 基本資料結構(Tuple)

## 1.元組(Tuple)

* <font color="#0080FF">**數字與元組**</font>

```python=+
x = (3)
print(x,type(x))

y = (3,)
print(y,type(y))
#單一元素的元組需要加上逗號否則括弧會被忽略
```

> ```3 <class 'int'>```</br>
> ```(3,) <class 'tuple'>```
##
* <font color="#0080FF">**不可變動型別**</font>

```python=+
x = (1,3,5)

x[1] = 'd'
x
```

> ```TypeError: 'tuple' object does not support item assignment```

## 2.元組的基礎

* <font color="#0080FF">**Tuple 基礎a(可視為不可變動的List)**</font>

```python=+
x = ('a','b','c')

print(x[2])
print(x[1:])
print(len(x))
print(max(x))
print(min(x))
print(5 in x)
print(5 not in x)
```

> ```c```</br>
> ```('b', 'c')```</br>
> ```3```</br>
> ```c```</br>
> ```a```</br>
> ```False```</br>
> ```True```
## 
* <font color="#0080FF">**Tuple 基礎b(可視為不可變動的List)**</font>
```python=+
x = ('a','b','c')

print(x[:2])
print(x + x)
print(x * 2)
print(x + (1,2))
```

> ```('a', 'b')```</br>
> ```('a', 'b', 'c', 'a', 'b', 'c')```</br>
> ```('a', 'b', 'c', 'a', 'b', 'c')```</br>
> ```('a', 'b', 'c', 1, 2)```
 
## 3.元組的自動解包、自動打包

* <font color="#0080FF">**Tuple 的自動解包、自動打包a**</font>

```python=+
(one,two,three,four) = (1,2,3,4)
print(one)
print(two)

a = 9
b = 3
print('a:',a,'b:',b)
#用於交換變數
a,b = b,a
print('a:',a,'b:',b)
```

> ```1```</br>
> ```2```</br>
> ```a: 9 b: 3```</br>
> ```a: 3 b: 9```
##
* <font color="#0080FF">**Tuple 的自動解包、自動打包b**</font>

```python=+
#Python會將所有逗號分隔的資料自動打包為Tuple
a = 1,2,3
b = 1,
#多重指定變數時自動解包
v1,v2,v3 = [1,2,3]
v4,v5,v6 = 'abc'

print(a)
print(b)
print(v1)
print(v5)
```

> ```(1, 2, 3)```</br>
> ```(1,)```</br>
> ```1```</br>
> ```b```
## 
* <font color="#0080FF">**Tuple 的自動解包、自動打包c**</font>

```python=+
def get_user_info(id):
    #用id編號從資料庫取得使用者資料
    return name,age,email

#乍看之下，這個函式會傳回3個值
#實際上Python將其打包成一個Tuple，所以回傳值還是只有一個
name,age,email = get_user_info(ZEOxO)
```

## 4.其他常用及特殊的Tuple操作

* <font color="#0080FF">**用「*」號的元素吸收多餘的元素**</font>

```python=+
x = (1,2,3,4)

a,b,*c = x
print(a,b,c)

a,*b,c = x
print(a,b,c)

*a,b,c = x
print(a,b,c)

#如果沒有多餘的元素，則加「*」號標記的元素將接收到空List
a,b,c,d,*e = x
print(a,b,c,d,e)
```

> ```1 2 [3, 4]```</br>
> ```1 [2, 3] 4```</br>
> ```[1, 2] 3 4```</br>
> ```1 2 3 4 []```
## 
* <font color="#0080FF">**用「*_」號接收不感興趣的資料**</font>

```python=+
x = [1,2,3,4,5]

a,*_,b = x #例如只要資料的頭、尾
print(a)
print(b)
```

> ```1```</br>
> ```5```
## 
* <font color="#0080FF">**List 與 Tuple 的轉換**</font>

```python=+
a = list((1,2,3,4))
b = tuple([1,2,3,4])

print(a)
print(b)
```

> ```[1, 2, 3, 4]```</br>
> ```(1, 2, 3, 4)```

## 時間戳記

> [name=ZEOxO][time=Mon, Aug 24, 2020 14:52 PM][color=#907bf7]