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
* <font color="#0080FF">**(!)物件的特殊屬性**</font>

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
        return self.radius * self.radius * self.__class__.pi  #不寫死類別名稱，就不用擔心日後更改了!
    
c1 = Circ()
print(c1.area())

c2 = Circ(3)
print(c2.area())
```

> ```3.14159```</br>
> ```28.27431```

##
* <font color="#0080FF">**類別變數與物件變數**</font>

```python=+
c1 = Circle(1)
c2 = Circle(2)

c1.pi = 3.14 #(注意!)此處為建立物件變數，而不是更改類別變數
c1.pi

#若找不到物件變數時，會自動尋找同名的類別變數
c2.pi 
```

> ```3.14```</br>
> ```3.14159```

## 4.靜態方法 (Static method) 與 類別方法 (Class method)

<font color="#0080FF">**circle.py**</font>

```python=+
'''circle 模組 : 包含 Circle 類別'''
class Circle:
    '''Circle 類別'''
    all_circles = [] #類別變數
    pi = 3.14159 #類別變數

    def __init__(self,r = 1):
        '''以給予的半徑建立圓物件'''
        self.radius = r
        self.__class__.all_circles.append(self)
    
    def area(self):
        '''計算此圓形的面積'''
        return self.__class__.pi * self.radius * self.radius

    @staticmethod
    def total_area(): #(注意!)靜態方法不會傳遞物件本身作為第一個參數
        '''用來計算 all_circles 這個 list 所有物件總面積的靜態方法'''
        total = 0
        for c in Circle.all_circles:
            total = total + c.area()
        return total
```
##
* <font color="#0080FF">**(續)呼叫靜態方法**</font>

```python=+
import circle
c1 = circle.Circle(1)
c2 = circle.Circle(2)

circle.Circle.total_area()

c2.radius = 3 #把物件變數 c2.radius 改為 3
circle.Circle.total_area()

c1.total_area() #從物件也可以呼叫到類別的靜態方法
```

> ```15.70795```</br>
> ```31.415899999999997```</br>
> ```31.415899999999997```
##
<font color="#0080FF">**circle_cm.py**</font>

```python=+
'''circle_cm 模組 : 包含 Circle 類別'''
class Circle:
    '''Circle 類別'''
    all_circles = [] #類別變數
    pi = 3.14159 #類別變數

    def __init__(self,r = 1):
        '''以給予的半徑建立圓物件'''
        self.radius = r
        self.__class__.all_circles.append(self)
    
    def area(self):
        '''計算此圓形的面積'''
        return self.__class__.pi * self.radius * self.radius

    @classmethod #類別方法class method
    def total_area(cls):
        '''用來計算 all_circles 這個 list 所有物件總面積的類別方法'''
        total = 0
        for c in cls.all_circles:
            #靜態方法是使用固定的類別名稱，類別方法是將類別本身傳遞為參數，不用擔心日後改名!!
            total = total + c.area()
        return total
```
##
* <font color="#0080FF">**(續)呼叫類別方法**</font>

```python=+
import circle_cm
c1 = circle_cm.Circle(1)
c2 = circle_cm.Circle(2)

circle_cm.Circle.total_area()

c2.radius = 3
circle_cm.Circle.total_area()
```

> ```15.70795```</br>
> ```31.415899999999997```

