# Python - 基本資料結構(List)

## 1.串列(List)

* <font color="#0080FF">**索引與切片**</font>

```python=+
x = ['first','second','third','fourth']

x[:3] #切最開頭的3份
x[2:] #前兩份不要，然後切到最後
x[-1:2] #第二個索引位置在第一個前面
```

> ```['first', 'second', 'third']```</br>
> ```['third', 'fourth']```</br>
> ```[]```</br>
## 
* <font color="#0080FF">**串列複製與參照**</font>

```python=+
x = ['first','second','third','fourth']

y = x[:] #y複製為x串列
y[0] = 'one'
print("y:",y)
print('x:',x) #不會影響x串列

y = x #y參照到x串列
y[0] = 'one'
print("y:",y)
print('x:',x) #會影響x串列
```

> ```y: ['one', 'second', 'third', 'fourth']```</br>
> ```x: ['first', 'second', 'third', 'fourth']```</br>
> ```y: ['one', 'second', 'third', 'fourth']```</br>
> ```x: ['one', 'second', 'third', 'fourth']```</br>
## 
* <font color="#0080FF">**更改串列的元素**</font>

```python=+
x = [1,2,3,4]

#於list最後面附加多個值
x[len(x):] = [5,6,7]
print(x)

#於list前面插入多個值
x[:0] = [-1,0]
print(x)

#移除list中多個元素
x[1:-1] = []
print(x)
```

> ```[1, 2, 3, 4, 5, 6, 7]```</br>
> ```[-1, 0, 1, 2, 3, 4, 5, 6, 7]```</br>
> ```[-1, 7]```
## 
* <font color="#0080FF">**串列常用方法(method)與操作**</font>

```python=+
x = [1,2,3,4]
y = [5,6,7]

x.append(y)
x
```

> ```[1, 2, 3, 4, [5, 6, 7]]```
##
```python=+
x = [1,2,3,4]
y = [5,6,7]

x.extend(y)
x
```

> ```[1, 2, 3, 4, 5, 6, 7]```
##
```python=+
x = [1,2,3]

x.insert(-1,'hello')
print(x)

x.insert(0,'start')
print(x)
```

> ```[1, 2, 'hello', 3]```</br>
> ```['start', 1, 2, 'hello', 3]```
##
```python=+
x = ['a',2,'c',7,9,11]

del(x[1])
print(x)

del(x[:2])
print(x)
```

> ```['a', 'c', 7, 9, 11]```</br>
> ```[7, 9, 11]```
## 
```python=+
x = [1,2,3,4,3,5]
#找到第一個與指定值相同的元素
x.remove(3)
print(x)

x.remove(3)
print(x)
```

> ```[1, 2, 4, 3, 5]```</br>
> ```[1, 2, 4, 5]```