# b.Python 速成班(進階)

###### tags: `Data Sicnce From Scratch`

> <font color="#EA0000" >**#IPython有個奇妙的功能 %paste，它可以正確貼上任何你放在剪貼簿中的程式碼**</font>

## 1.函式 (Function)

* <font color="#0080FF">**頭等(First-class)函式**</font>

```python=+
#Python 的函式屬於一等(First-class)函式，也就是說，我們可以把函式指定給某個變數，然後把它傳進某個函式中
def double(x):
  return x * 2

def apply_to_one(f):
  """給予傳進來的函式「1」的參數"""
  return f(1)

my_double = double
result = apply_to_one(my_double)
print(result)
```

> ```2```

##
* <font color="#0080FF">**短匿名函式(或lambda函式)**</font>

```python=+
y = apply_to_one(lambda x:x+4)
print(y)
```

> ```5```

## 
* <font color="#0080FF">**把lambda指定給變數，不推薦**</font>

```python=+
another_double = lambda x:x*2
print(another_double(2))

def another_double(x):
  """建議改用這種作法"""
  return x*2 
print(another_double(2))
```

> ```4```</br>
> ```4```

##
* <font color="#0080FF">**指定函式內參數名稱**</font>

```python=+
def full_name(first = "What's-his-name",last = "Something"):
  return first + " " + last 

full_name("Joel","Grus")
full_name("Joel")
full_name(last = "Grus")
```

> ```What's-his-name Grus```

## 2.字串 (String)

* <font color="#0080FF">**跳脫字元**</font>

```python=+
tab_string = "\t"
print(tab_string,len(tab_string))
```

> ```	 1```
## 
* <font color="#0080FF">**建立原始字串**</font>

```python=+
r_tab_string = r"\t" #用「r」建立raw(原始)-string
print(r_tab_string,len(r_tab_string))
```

> ```\t 2```

## 3.例外處理 (Exception)

* <font color="#0080FF">**簡單的例外處理結構**</font>

```python=+
try:
  print(0 / 0)
except ZeroDivisionError:
  print("cannot divide by zero!!")
else:
  print("unexpected error!!")
finally:
  print(">>process end")
```

> ```cannot divide by zero!!```</br>
> ```>>process end```


## 4.列表 (List)

* <font color="#0080FF">**列表的新增**</font>

```python=+
x = [1,2,3]
x.extend([4,5,6]) #會更改列表本身
print(x)

x = [1,2,3]
y = x + [4,5,6] #如不想更改列表本身可用「+」
y
```
> ```[1, 2, 3, 4, 5, 6]```</br>
> ```[1, 2, 3, 4, 5, 6]```

## 5.元組 (Tuple)

> <font color="#EA0000">**#例外處理(Exception):</br>#修改元組內容 - TypeError**</font>

* <font color="#0080FF">**例外處理**</font> 

```python=+
my_list = [1,2]
my_tuple = (1,2)
other_tuple = 3,4
my_list[1] = 3

try:
  my_tuple[1] = 3
except TypeError:
  print("cannot modify tuple's content!")
```

> ```cannot modify tuple's content!```

* <font color="#0080FF">**函式回傳多個值**</font>

```python=+
def sum_and_product(x,y):
  return (x+y),(x*y) #依舊是回傳一個值，因為統一被打包成一個Tuple

sp = sum_and_product(2,3)
s,p = sum_and_product(5,10)
print("sp =",sp)
print("s =",s,"p =",p)
```

> ```sp = (5, 6)```</br>
> ```s = 15 p = 50```
##
* <font color="#0080FF">**多重賦值**</font>

```python=+
#元組和列表都可使用多重賦值(multiple assignment)
x,y = 1,2
x,y = y,x
print("x =",x)
print("y =",y)
```

> ```sp = (5, 6)```</br>
> ```s = 15 p = 50```

## 6.字典 (Dict)

> <font color="#EA0000">**#例外處理(Exception):</br>#不存在的鍵值來取值 - KeyError**</font>

* <font color="#0080FF">**例外處理**</font>

```python=+
grades = {"Joel":80, "Tim":95}

try:
  kate_grade = grades["Kate"]
except KeyError:
  print("cannot found assign key!!")
```

> ```cannot found assign key!!```
##
* <font color="#0080FF">**字典的 取值方法**</font>

```python=+
grades = {"Joel":80, "Tim":95}
joels_grade = grades.get('Joel',0)
print(joels_grade)

kates_grade = grades.get("Kate",0)
print(kates_grade)

no_ones_grade = grades.get("No One") #get方法不會產生例外
print(no_ones_grade)
```
##
* <font color="#0080FF">**字典的 檢查方法**</font>

```python=+
grades = {"Joel":80, "Tim":95}
grades_keys = grades.keys()
grades_values = grades.values()

#檢查鍵值
print("Joel" in grades_keys)
print("Kate" in grades) #推薦

#檢查對應值(唯一方法)
print(95 in grades_values)
```

> ```True```</br>
> ```False```</br>
> ```True```

> <font color="#EA0000">**#(注意!)字典的鍵值必須是「可湊化的(hashable)」;尤其注意絕不能用列表(list)當作鍵值
#需要多維的鍵值，就應該使用元組，或是把鍵值轉換成一個字串!!**</font>

## 7.Defaultdict

* <font color="#0080FF">**計算整份文件的單詞數量(利用例外處理:先做再說，錯了再補救)**</font>

```python=+
word_counts = {}
def document_counts(document):
  for word in document:
    try:
      word_counts[word] += 1
    except:
      word_counts[word] = 1
  print(word_counts)
```
##
* <font color="#0080FF">**計算整份文件的單詞數量(優雅的作法)**</font>

```python=+
word_counts = {}
def document_counts(document):
  for word in document:
    previous_count = word_counts.get(word,0)
    word_counts[word] = previous_count + 1
```
##
* <font color="#0080FF">**最乾淨俐落的作法 - defaultdict**</font>

```python=+
from collections import defaultdict
word_counts = defaultdict(int) #使用前必須先指定預設 - int()會生成「0」

def document_counts(document):
  for word in document:
    word_counts[word] += 1
```
##
* <font color="#0080FF">**(續)最乾淨俐落的作法 - defaultdict**</font>

```python=+
dd_list = defaultdict(list)
dd_list[2].append(1) #先建立出空陣列{2:[]} => 再append{2:[1]} 
print(dict(dd_list)) #要轉換成dict來使用、查看

dd_dict = defaultdict(dict) 
dd_dict["Joel"]["City"] = "Seattle" #先建立出空字典{'Joel':{}} => 再{'Joel': {'City': 'Seattle'}}
print(dict(dd_dict)) #要轉換成dict來使用、查看
 
dd_pair = defaultdict(lambda : [0,0])
dd_pair[2][1] = 1
print(dict(dd_pair))
```

> ```{2: [1]}```</br>
> ```{'Joel': {'City': 'Seattle'}}```</br>
> ```{2: [0, 1]}```

## 8.計數器 (Counter)

* <font color="#0080FF">**建立一個計數器**</font>

```python=+
from collections import Counter
c = Counter([0,1,2,0]) # c = {'0':2,'1':1,'2':1}
c
```

> ```Counter({0: 2, 1: 1, 2: 1})```
##
* <font color="#0080FF">**計數最常出現的單詞(word)**</font>

```python=+
def document_counts(document):
  word_counts = Counter(document)#document 是由許多單詞(word)構成的一個列表

  for word,count in word_counts.most_common(10):
    #輸出前10個最常用的單詞(word)，及其出現次數(count)
    print(word,count)
```

## 9.集合 (Set)

> <font color="#EA0000">**#針對set進行in操作，速度非常快(因為重複的元素會被刪除)，因此檢查次數減少**</font>

## 10.控制流程 (Process Control)

> <font color="#EA0000">**#if-then-else</br>#while,for,in,continue,break**</font>

## 11.真(True)與假(False)

* <font color="#0080FF">**針對 'None' 的真假判斷**</font>

```python=+
x = None
assert x == None #True
assert x is None #推薦寫法

#assert x is False #若執行此程式碼，則產生例外
```
##
* <font color="#0080FF">**Python 的邏輯判斷**</font>

```python=+
s = 'string'
first_char = s and s[0] # True and True -> 傳回s「0」
print(first_char) 

s = ''
first_char = s and s[0] # False and True -> 傳回s
first_char
```
##
* <font color="#0080FF">**(!)(續)Python 的邏輯判斷**</font>

```python=+
#all()函式 -> 其一為False，則結果為False，否則True
a = all([True,1,{3}]) #True
b = all([True,1,{}]) #False

#any()函式 -> 其一為True，則結果為True，否則False
c = any([True,1,{}]) #True
d = any([None,0,{}]) #False

e = all([]) #Ture，因為沒有代表「False」的元素
f = any([]) #False，因為沒有代表「True」的元素
print(a,b,c,d,e,f)
```

## 11.排序 (Sort)

* <font color="#0080FF">**指定函式條件 (Ex.abs) 進行排序**</font>

```python=+
x = [-4,1,-2,3]
x.sort(key = abs,reverse = True)
x
```

> ```[-4, 3, -2, 1]```
##
* <font color="#0080FF">**自訂函式條件 進行排序**</font>

```python=+
def return_Length(ele):
  return len(ele)

x = ['Lion','Frog','Dog','Elephant']
y = sorted(x,key = return_Length,reverse = True)
y
```

> ```['Elephant', 'Lion', 'Frog', 'Dog']```
##
* <font color="#0080FF">**(續)自訂函式條件 進行排序**</font>

```python=+
word_counts = {'Lion':3,'Rabbit':5,'Cat':10,"Dog":6}
sort_by_length = sorted(word_counts.items(),key = lambda word_and_counts:len(word_and_counts[0]))
sort_by_counts = sorted(word_counts.items(),key = lambda word_and_counts:word_and_counts[1])

print(sort_by_length) #依照字串長度排列
print(sort_by_counts) #依照出現次數排列
```

> ```[('Cat', 10), ('Dog', 6), ('Lion', 3), ('Rabbit', 5)]```</br>

> ```[('Lion', 3), ('Rabbit', 5), ('Dog', 6), ('Cat', 10)]```

## 12.解析式列表 (List Comprehension)

* <font color="#0080FF">**解析式列表 套入條件判斷**</font>

```python=+
evens = [x for x in range(5) if x%2 == 0]
evens
```

> ```[0, 2, 4]```
##
* <font color="#0080FF">**解析式字典 與 解析式集合**</font>

```python=+
square_dict = {x:x*x for x in range(5)}
square_dict

square_set = {x*x for x in [-2,-1,0,1,2]}
square_set
```

> ```{0: 0, 1: 1, 2: 4, 3: 9, 4: 16}```</br>
> ```{0, 1, 4}```
##
* <font color="#0080FF">**<!>解析式列表 套入多重迴圈**</font>

```python=+
#可有多個for迴圈
pairs = [(i,j) for i in range(5) for j in range(2)]
pairs
```

> ```[(0, 0),(0, 1),(1, 0),(1, 1),(2, 0),(2, 1),(3, 0),(3, 1),(4, 0),(4, 1)]```
##
* <font color="#0080FF">**<!>(續)解析式列表 套入多重迴圈**</font>

```python=+
#後面的迴圈可以使用前面的結果
increasing_pairs = [(x,y) for x in range(5) for y in range(x,x+1)]
increasing_pairs
```

> ```[(0, 0), (1, 1), (2, 2), (3, 3), (4, 4)]```

## 13.斷言 (Assert)

* <font color="#0080FF">**assert(斷言) 若條件不成立則產生例外**</font>

```python=+
def smallest_items(xs):
  assert xs,"空項目不會有最小項" #AssertionError: 空項目不會有最小項(自訂的輸出內容)
  return min(xs)

assert smallest_items([5,10,15,20]) == 5
assert smallest_items([])
```

> ```AssertionError: 空項目不會有最小項```

## zip(參數壓合) 與 *(參數拆分)

* <font color="#0080FF">**參數壓合 與 參數拆分**</font>

```python=+
list1 = ['a','b','c']
list2 = [1,2,3]

#zip參數壓合
x = [ele for ele in zip(list1,list2)]
print(x)

#zip參數拆分
alpha,num = zip(*x)
print(alpha,num)
```

> ```[('a', 1), ('b', 2), ('c', 3)]```</br>
> ```('a', 'b', 'c') (1, 2, 3)```
##
* <font color="#0080FF">**(續)參數壓合 與 參數拆分**</font>

```python=+
def add(x,y):return x+y

result = add(*[2,3]) #把list[2,3] 拆分成 2,3
result
```

> ```5```

## 時間戳記

> [name=ZEOxO][time=Tue, Sep 8, 2020 16:15 PM][color=#907bf7]
