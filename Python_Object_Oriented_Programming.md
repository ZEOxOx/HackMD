# n.Python - 類別與物件導向程式設計

###### tags: `Python`

## 1.物件變數與__init__特殊 method

* <font color="#0080FF">**可隨時建立的物件變數 (不好的方式)**</font>

```python=+
class Circle:
    '''Circle : An Empty Class'''
    pass

c1 = Circle()
c1.radius = 3 
#計算圓的周長
print(2 * 3.14 * c1.radius)

c2 = Circle()
c2.r = 5
#計算圓的周長
print(2 * 3.14 * c2.r)

print(Circle().__doc__)
```

> ```18.84```</br>
> ```31.400000000000002```</br>
> ```Circle : An Empty Class```
##
* <font color="#0080FF">**初始化物件變數**</font>

```python=+
class Circle:
    def __init__(self): # <-- c1被傳進這裡的self
        self.radius = 1
        
c1 = Circle() #(注意!)c1物件會自動被傳入到上面的self
print(2 * 3.14 * c1.radius)

c1.radius = 5
print(2 * 3.14 * c1.radius)
```

> ```6.28```</br>
> ```31.400000000000002```

## 2.物件的函式 (method)

* <font color="#0080FF">**定義及呼叫方法**</font>

```python=+
class Circle:
    def __init__(self):
        self.radius = 1
    def area(self):
        return self.radius * self.radius * 3.14159
    
c1 = Circle()
print(c1.area())
c1.radius = 3
print(c1.area())

print(Circle.area(c1)) #(注意!)另外一種呼叫 c 物件 area 的方法
```

> ```3.14159```</br>
> ```28.27431```</br>
> ```28.27431```
##
* <font color="#0080FF">**建立物件時傳遞引數、預設值**</font>

```python=+
class Circle:
    def __init__(self,r = 1):#未給予引數的情況下使用預設值
        self.radius = r
    def area(self):
        return self.radius * self.radius * 3.14159
    
c1 = Circle()
print(c1.area())

c2 = Circle(3)
print(c2.area())
```

> ```3.14159```</br>
> ```28.27431```

## 3.類別變數 (class variables)

* <font color="#0080FF">**建立物件時傳遞引數、預設值**</font>

```python=+
class Circle:
    pi = 3.14159 #建立類別變數 pi
    def __init__(self,r = 1):
        self.radius = r
    def area(self):
        return self.radius * self.radius * Circle.pi #使用類別變數 pi
    
c1 = Circle()
print(c1.area())

c2 = Circle(3)
print(c2.area())
```

> ```3.14159```</br>
> ```28.27431```
##
* <font color="#0080FF">**物件的特殊屬性**</font>

```python=+
Circle
c1.__class__
c1.__class__.pi
```

> ```__main__.Circle```</br>
> ```__main__.Circle```</br>
> ```3.14```
##
* <font color="#0080FF">**(!)避免日後更改類別名稱的方法**</font>

```python=+
class Circ:
    pi = 3.14159 
    def __init__(self,r = 1):
        self.radius = r
    def area(self):
        return self.radius * self.radius * self.__class__.pi 
        #不寫死類別名稱，就不用擔心日後更改了!
    
c1 = Circ()
print(c1.area())

c2 = Circ(3)
print(c2.area())
```