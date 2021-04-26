# b.Python - 基本資料結構(List)

###### tags: `Python`

## 1.串列(List)

* <font color="#0080FF">**索引與切片**</font>

```python=+
x = ['first','second','third','fourth']

x[:3] #切最開頭的3份
x[2:] #前兩份不要，然後切到最後
x[-1:2] #第二個索引位置在第一個前面
```
[^first]:
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
* <font color="#0080FF">**<!>更改串列的元素**</font>

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

## 2.串列常用方法(method)與操作

* <font color="#0080FF">**append()**</font>

```python=+
x = [1,2,3,4]
y = [5,6,7]

x.append(y)
x
```

> ```[1, 2, 3, 4, [5, 6, 7]]```
##
* <font color="#0080FF">**extend()**</font>

```python=+
x = [1,2,3,4]
y = [5,6,7]

x.extend(y)
x
```

> ```[1, 2, 3, 4, 5, 6, 7]```
##
* <font color="#0080FF">**insert()**</font>

```python=+
x = [1,2,3]

x.insert(-1,'hello') #(注意!)insert第一個引數為-1時並不是加到最後面 
print(x)

x.insert(0,'start')
print(x)
```

> ```[1, 2, 'hello', 3]```</br>
> ```['start', 1, 2, 'hello', 3]```
##
* <font color="#0080FF">**del()**</font>

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
* <font color="#0080FF">**remove()**</font>

```python=+
x = [1,2,3,4,3,5]
#找到第一個與指定值相同的元素
x.remove(3)
print(x)

x.remove(3)
print(x)

#建議在刪除前用「in」來檢查該元素是否存在陣列
#因為若無法找到要刪除的元素，會引發錯誤
```

> ```[1, 2, 4, 3, 5]```</br>
> ```[1, 2, 4, 5]```
##
* <font color="#0080FF">**reverse()**</font>

```python=+
x = [1,3,11,7,9]

x.reverse()
x
```

> ```[9, 7, 11, 3, 1]```
##
* <font color="#0080FF">**sort()**</font>

```python=+
x = [3,8,4,0,2,1]
x.sort()
print(x)

x = [1,2,'hello',3] #不可包含數字及字串，無法比較
x.sort()
print(x)

x = ['Life','is','Enchanting']
x.sort()
print(x)

x = [[3,5],[2,9],[2,3],[4,1],[3,2],[2,3,4]] #串列內的元素是list也可以排列
x.sort()
print(x)

x = [0,1,2]
x.sort(reverse=True)
print(x)
```

> ```[0, 1, 2, 3, 4, 8]```</br>
> ```TypeError: '<' not supported between instances of 'str' and 'int'```</br>
> ```['Enchanting', 'Life', 'is']```</br>
> ```[[2, 3], [2, 3, 4], [2, 9], [3, 2], [3, 5], [4, 1]]```</br>
> ```[2, 1, 0]```
##
* <font color="#0080FF">**sorted()**</font>

```python=+
x = [4,3,2,1]

y = sorted(x) #建立了一個新的「y」串列
print('x:',x)
print('y:',y)

y[0] = 'one'
print('x:',x)
print('y:',y) #不會影響x串列
```

> ```x: [4, 3, 2, 1]```</br>
> ```y: [1, 2, 3, 4]```</br>
> ```x: [4, 3, 2, 1]```</br>
> ```y: ['one', 2, 3, 4]```

##
* <font color="#0080FF">**index()**</font>

```python=+
x = [1,3,'five',7,-2]

x.index(7)
x.index(5)
```

> ```3```</br>
> ```ValueError: 5 is not in list```
##
* <font color="#0080FF">**count()**</font>

```python=+
x = [1,2,2,3,5,2,5]

x.count(2)
x.count(5)
x.count(4)
```

> ```3```</br>
> ```2```</br>
> ```0```
##
* <font color="#0080FF">**min()、max()、sum()**</font>

```python=+
min(3,7,0,-2,11)

max('Hello','World','!!')
max(4,'OxO',[1,2]) #不可包含數字及字串，無法比較

sum([1,5,6,7,8])
```

> ```-2```</br>
> ```'World'```</br>
> ```TypeError: '>' not supported between instances of 'str' and 'int'```</br>
> ```27```

## 3.其他常用及特殊的list操作

* <font color="#0080FF">**將字串分解成字元**</font>

```python=+
list("Hello")
```

> ```['H', 'e', 'l', 'l', 'o']```
##
* <font color="#0080FF">**<!>自定義排序**</font>

```python=+
def campare_num_of_chars(st):
    return len(st)

word_list = ['HELLO','my','name','is','ZEOxO']
word_list.sort()
print(word_list)

word_list = ['HELLO','my','name','is','ZEOxO']
word_list.sort(key = campare_num_of_chars)
#只要設為key的函式會回傳大小就可以做比較!
print(word_list)
```

> ```['HELLO', 'ZEOxO', 'is', 'my', 'name']```</br>
> ```['my', 'is', 'name', 'HELLO', 'ZEOxO']```
##
* <font color="#0080FF">**使用「in」算符測試某元素值是否存在**</font>

```python=+
3 in [1,3,4,5]
3 not in [1,3,4,5]

3 in ['one','two','three','four']
3 not in ['one','two','three','four']
```

> ```True```</br>
> ```False```</br>
> ```False```</br>
> ```True```
##
* <font color="#0080FF">**使用「*」算符將list初始化**</font>

```python=+
x = [None] * 4
y = [[0] * 3] * 3

print(x)
print(y)
```

> ```[None, None, None, None]```</br>
> ```[[0, 0, 0], [0, 0, 0], [0, 0, 0]]```
##
* <font color="#0080FF">**使用「+」算符來串聯list**</font>

```python=+
z = [1,2,3] + [4,5]
print(z)
```

> ```[1, 2, 3, 4, 5]```</br>

## 4.多層List與深層拷貝(deepcopy)

* <font color="#0080FF">**<!>多層陣列 元素參照**</font>

```python=+
nested = [0]
original = [nested,1]
print(original)

nested[0] = 'zero'
#不可寫成「nested = 'zero'」這樣nested會參照到新的字串
print('nested:',nested)
print('original:',original)

#nested與original互相連結
original[0][0] = 0
print('nested:',nested)
print('original:',original)

#nested參照到新陣列，使原本的連結破壞
nested = [2]
print('nested:',nested)
print('original:',original)
```

> ```[[0], 1]```</br>
> ```nested: ['zero']```</br>
> ```original: [['zero'], 1]```</br>
> ```nested: [0]```</br>
> ```original: [[0], 1]```</br>
> ```nested: [2]```</br>
> ```original: [[0], 1]```
##
* <font color="#0080FF">**<!>深層拷貝(deepcopy)**</font>

```python=+
original = [[0],1]
shallow = original[:]#[淺層拷貝]並不會將第二層以上的list複製一份，而是參照到原list
import copy
deep = copy.deepcopy(original)
#[深層拷貝]則是獨立於原始list，更改deep的list不會對original造成影響

shallow[1] = 2
print("shallow:",shallow)
print("original:",original)

shallow[0][0] = 'zero'
#不可寫成「shallow[0] = ['zero']」因為會參照到新的陣列
print("shallow:",shallow)
print("original:",original)

deep[0][0] = 5
print("deep:",deep)
print("original:",original)
```

> ```shallow: [[0], 2]```</br>
> ```original: [[0], 1]```</br>
> ```shallow: [['zero'], 2]```</br>
> ```original: [['zero'], 1]```</br>
> ```deep: [[5], 1]```</br>
> ```original: [['zero'], 1]```

## 時間戳記

> [name=ZEOxO][time=Mon, Aug 24, 2020 13:12 PM][color=#907bf7]