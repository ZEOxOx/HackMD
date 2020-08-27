# Python - 流程控制

## 1.簡潔的 Python 語法

* <font color="#0080FF">**Python 的 switch-case 語法**</font>

```python=+
def rank_S():
    return('Perfect!!')
def rank_A():
    return('Wonderful!!')
def rank_B():
    return('Great!!')
def rank_C():
    return('Nice!!')
def rank_D():
    return('Not Bad!!')

com = {'D':rank_D,'C':rank_C,'B':rank_B,'A':rank_A,'S':rank_S}
rank = 'A'
print(com[rank]())
```
<font color="#0080FF">**OR**</font>
```python=+
com = {'D':rank_D(),'C':rank_C(),'B':rank_B(),'A':rank_A(),'S':rank_S()}
rank = 'A'
print(com[rank])
```

> ```Wonderful!!```
## 
* <font color="#0080FF">**For 迴圈與 Tuple 解包多重設定變數**</font>

```python=+
ls = [(1,2),(3,7),(9,5)]

result = 0
for num1,num2 in ls:
    #一次設定兩個變數
    result = result + (num1 * num2)
    
print(result)
```

> ```68```

## 2.常用的 Method 與函式

* <font color="#0080FF">**enumerate()**</font>

```python=+
x = ['a','b','c']

#將list、tuple元素取出並加上索引
list(enumerate(x))
```

> ```[(0, 'a'), (1, 'b'), (2, 'c')]```
##
* <font color="#0080FF">**enumerate 與迴圈**</font>

```python=+
ls = ['ZEOxO','Andy','Bob']

for i,name in enumerate(ls):
    print("No." + str(i) + " -> " + name)
```

> ```No.0 -> ZEOxO```</br>
> ```No.1 -> Andy```</br>
> ```No.2 -> Bob```
##
* <font color="#0080FF">**zip()**</font>

```python=+
x = [1,2,3,4]
y = ('a','b','c')

z = zip(y,x) #只能結合3個對等的元素
list(z)
```

> ```[('a', 1), ('b', 2), ('c', 3)]```

## 3.布林值與運算式的真假運算

* <font color="#0080FF">**將 Python 物件作為布林值**</font>

```python=+
print('數字:',bool(0),bool(0.0),bool(0+0j))

print('字串:',bool("")) #除空字串，其餘字串皆為「True」
print('串列:',bool([])) #除空串列，其餘串列皆為「True」
print('元組:',bool(())) #除空元組，其餘元組皆為「True」
print('字典:',bool({})) #除空字典，其餘字典皆為「True」

print('None:',bool(None)) #None永遠為「False」
```

> ```數字: False False False```</br>
> ```字串: False```</br>
> ```串列: False```</br>
> ```元組: False```</br>
> ```字典: False```</br>
> ```None: False```
##
* <font color="#0080FF">**(!)將 Python 物件作邏輯運算**</font>

```python=+
[2] and [3,4] #找到「False」則停止並回傳，若無則傳回最後一個值
[] and 5
[2] or [3,4] #找到「True」則停止並回傳，若無則傳回最後一個值
[] or 5
```

> ```[3, 4]```</br>
> ```[]```</br>
> ```[2]```</br>
> ```5```
##
* <font color="#0080FF">**Short-circuit Evaluation**</font>

(SKIP)

## 
* <font color="#0080FF">**(!)將 Python 物件作布林運算**</font>

```python=+
x = [0]
y = [x,1]
print(x is y[0]) #比較參照值(id)

x = [0]
print(x is y[0])

print(x == y[0]) #兩者的值仍然相同
```

> ```True```</br>
> ```False```</br>
> ```True```

## 4.補充內容

* <font color="#0080FF">**用索引刪除 List 元素的隱藏 Bug**</font>

```python=+
x = [0,1,2,3,4,5,6,7]
for i,n in enumerate(x):
    if(i % 2 == 1):
        del(x[i]) #刪除奇數位置
        
#因陣列元素被刪除，導致元素往前遞補，結果不如預期
print(x)
```

> ```[0, 2, 3, 5, 6]```

* <font color="#0080FF">**(續)改為從 List 後面開始刪除**</font>

```python=+
x = [ele for ele in range(0,8)]
print(x)
for i in range(len(x)-1,-1,-1):
    if(i % 2 == 1):
        del(x[i]) #刪除奇數位置
        
print(x)
```

> ```[0, 2, 4, 6]```