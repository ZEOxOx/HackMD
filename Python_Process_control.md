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
##
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
