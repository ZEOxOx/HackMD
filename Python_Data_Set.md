# Python - 基本資料結構(Set)

###### tags: `Python`

## 1.集合(Set)

* <font color="#0080FF">**重複的資料會被自動刪除**</font>

```python=+
x = {1,2,1,2,1,2,1,2}
print(x)
```

>```{1, 2}```
## 
* <font color="#0080FF">**邏輯運算**</font>

```python=+
x = {1,2,3,6}
y = set([1,7,8,9])

print(x | y) #聯集(OR)
print(x & y) #交集(AND)
print(x ^ y) #對稱差(XOR)
```

> ```{1, 2, 3, 6, 7, 8, 9}```</br>
> ```{1}```</br>
> ```{2, 3, 6, 7, 8, 9}```

## 2.集合常用方法(method)與操作

* <font color="#0080FF">**Set 無序的資料型態 - 不支援切片、索引及「順序相關」的「+」及「*」操作**</font>

```python=+
x = set([1,2,3,1,3,5])
print(x)

x.add(6) #新增元素
print(x)

x.remove(5) #刪除元素
print(x)

print(1 in x)
print(4 in x)
```

> ```{1, 2, 3, 5}```</br>
> ```{1, 2, 3, 5, 6}```</br>
> ```{1, 2, 3, 6}```</br>
> ```True```</br>
> ```False```

* <font color="#0080FF">**frozenset()**</font>

```python=+
x = set([1,2,3,1,3,5])
z = frozenset(x)
print(z)

z.add(6) #frozenset為不可變動型別，產生錯誤
x.add(z) #set裡面只可存放不可變動物件(如frozenset)
print(x)
```

> ```frozenset({1, 2, 3, 5})```</br>
> ```AttributeError: 'frozenset' object has no attribute 'add'```</br>
> ```{1, 2, 3, 5, frozenset({1, 2, 3, 5})}```

## 時間戳記

> [name=ZEOxO][time=Mon, Aug 24, 2020 15:46 PM][color=#907bf7]