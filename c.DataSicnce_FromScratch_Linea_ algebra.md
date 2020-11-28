# c.資料科學 - 線性代數

###### tags: `Data Sicnce From Scratch`

## 1.向量 Vector

* <font color="#0080FF">**向量(vector)**</font>

> <font color="#EA0000" >**#向量:即是一個"浮點數列表"**</font>

```python=+
from typing import List

Vector = List[float]
height_weight_age = [70,170,40] #向量:[英吋,磅,年齡]
grades = [95,80,75,62] #向量:[第一次考試成績,第二次...,...]
```
#
* <font color="#0080FF">**兩個向量相加 - add**</font>

```python=+
def add(v:Vector, w:Vector) -> Vector:
  """相應元素相加"""
  assert len(v) == len(w),"兩個向量必須具有相同的維度"

  #用zip把兩個向量壓合起來，並利用解析式列表把相應元素相加起來
  #就可以輕易達到向量相加的效果
  return [v_i + w_i for v_i,w_i in zip(v,w)]

assert add([1,2,3],[4,5,6]) == [5,7,9]
print("[1,2,3] + [4,5,6] =",add([1,2,3],[4,5,6]))
```

> ```[1,2,3] + [4,5,6] = [5, 7, 9]```
#

* <font color="#0080FF">**兩個向量相減 - subtract**</font>

```python=+
def subtract(v:Vector , w:Vector) -> Vector:
  """相應元素相減"""
  assert len(v) == len(w),"兩個向量必須具有相同的維度"

  return [v_i - w_i for v_i,w_i in zip(v,w)]

assert subtract([5,7,9],[4,5,6]) == [1,2,3]
print("[5,7,9] - [4,5,6] =",subtract([5,7,9],[4,5,6]))
```

> ```[5,7,9] - [4,5,6] = [1, 2, 3]```
##
* <font color="#0080FF">**向量列表內所有向量相加 - vector_sum**</font>

```python=+
"""針對向量列表，把其中所有的向量相加起來，也就是說最後要創建出一個新向量"""
def vector_sum(vectors:List[Vector]) -> Vector:
  """所有相應元素相加"""
  #先檢查一下 vectors 這個向量列表不是空的
  assert vectors,"列表中沒有向量"

  #檢查 vectors 列表中的向量全部具有相同的維度
  num_elements = len(vectors[0])
  assert all(len(v) == num_elements for v in vectors),"向量維度不一致!"

  #所有 vector[i] 相加起來,就是結果的第i個元素值
  return [sum(vector[i] for vector in vectors) for i in range(num_elements)]

assert vector_sum([[1,2],[3,4],[5,6],[7,8]]) == [16,20]
print("[1+3+5+7, 2+4+6+8] =",vector_sum([[1,2],[3,4],[5,6],[7,8]]))
```

> ```[1+3+5+7, 2+4+6+8] = [16, 20]```
##
* <font color="#0080FF">**向量共同乘以一個純量 - scalar_multiply**</font>

```python=+
"""讓所有向量乘以一個純量"""
def scalar_multiply(c:float ,v:Vector) -> Vector:
  """每一個元素都乘以c"""
  return [c * v_i for v_i in v]

assert scalar_multiply(2,[1,2,3]) == [2,4,6]
print("2 * [1,2,3] =",scalar_multiply(2,[1,2,3]))
```

> ```2 * [1,2,3] = [2, 4, 6]```
##
* <font color="#0080FF">**計算向量列表內所有向量(維度相同)各元素的平均值 - vector_mean**</font>

```python=+
def vector_mean(vectors : List[Vector]) -> Vector:
  """計算每個元素的平均值"""
  n = len(vectors)
  return scalar_multiply(1/n , vector_sum(vectors))

assert  vector_mean([[1,2],[3,4],[5,6]]) == [3,4]
print("[(1+3+5)/3, (2+4+6)/3] =",vector_mean([[1,2],[3,4],[5,6]]))
```

> ```[(1+3+5)/3, (2+4+6)/3] = [3.0, 4.0]```
##
* <font color="#0080FF">**兩個向量的點積 - dot**</font>

```python=+
"""計算兩個向量的點積"""
def dot(v:Vector, w:Vector) -> float:
  """計算 v_1 * w_1 + ... + v_n * w_n"""
  assert len(v) == len(w),"兩個向量必須具有相同的維度"

  return sum(v_i * w_i for v_i,w_i in zip(v,w))

assert dot([1,2,3],[4,5,6]) == 32
print("(1*4) + (2*5) + (3*6) =",dot([1,2,3],[4,5,6]))
```

> ```(1*4) + (2*5) + (3*6) = 32```
## 
* <font color="#0080FF">**單一向量的平方和 - sum_of_squares**</font>

```python=+
"""透過點積運算，可以輕鬆計算出向量元素的平方和"""
def sum_of_squares(v:Vector) -> float:
  """送回 v_1 * v_1 + ... + v_n * v_n"""
  return dot(v,v)

assert sum_of_squares([1,2,3]) == 14
print("1*1 + 2*2 + 3*3 =",sum_of_squares([1,2,3]))
```

> ```1*1 + 2*2 + 3*3 = 14```
##
* <font color="#0080FF">**單一向量的長度(大小) - magnitude**</font>

```python=+
import math

def magnitude(v:Vector) -> float:
  """送回 v 的長度(或大小)"""
  #a^2 = 根號(b^2 + c^2)
  return math.sqrt(sum_of_squares(v)) #sqrt是一個計算平方根的函式

assert magnitude([3,4]) == 5
print("sqrt(3*3 + 4*4) =",magnitude([3,4]))
```

> ```sqrt(3*3 + 4*4) = 5.0```
##
* <font color="#0080FF">**計算兩個向量間的距離 - distance**</font>

```python=+
def squared_distance(v:Vector,w:Vector) -> float:
  """計算 (v_1 - w_1) ** 2 + ... + (v_2 - w_2) ** 2"""
  return sum_of_squares(subtract(v,w))

def distance(v:Vector, w:Vector) -> float:
  """計算v和w之間的距離"""
  return math.sqrt(squared_distance(v,w))
```
##
* <font color="#0080FF">**(續)計算兩個向量間的距離 - distance**</font>

```python=+
"""如果寫成下面的樣子會比較好"""
def distance(v:Vector ,w:Vector) -> float:
  """等價的作法"""
  return magnitude(subtract(v,w))
```

## 2.矩陣 Matrix

* <font color="#0080FF">**矩陣(matrix)**</font>

> <font color="#EA0000" >**#矩陣：由多個"向量"所組成**</font>

```python=+
#這又是另一個型別別名
Matrix = List[List[float]] #通常用列表的列表(list of list)來表示

A = [[1,2,3],[4,5,6]]
B = [[1,2],[3,4],[5,6]]
```
##
* <font color="#0080FF">**矩陣的形狀 - shape**</font>

```python=+
from typing import Tuple

def shape(A:Matrix) -> Tuple[int,int]:
  """送回A的 (橫行數量,縱列數量)"""
  num_rows = len(A)
  num_cols = len(A[0]) if A else 0 #第一橫行的元素數量
  return num_rows,num_cols

assert shape([[1,2,3],[4,5,6]]) == (2,3) #2橫行，3縱列
print(shape([[1,2,3],[4,5,6]]))
```

> ```(2, 3)```
## 
* <font color="#0080FF">**取得矩陣內特定向量 - get_row、get_column**</font>

```python=+
def get_row(A:Matrix, i:int) -> Vector:
  """送回 A 的第i行 (結果是一個 Vector 向量)"""
  return A[i]

def get_column(A:Matrix, j:int) -> Vector:
  """送回A的第j列 (結果是一個 Vector 向量)"""
  return [A_i[j] for A_i in A]
```
##
* <font color="#0080FF">**生成矩陣 - make_matrix**</font>

```python=+
"""根據矩陣形狀，再加上一個能生成矩陣元素的函式，來創造出一個矩陣"""
from typing import Callable

def make_matrix(num_rows : int,
        num_cols : int,
        entry_fn : Callable[[int,int],float]) -> Matrix:
  """
  送回第一個 num_rows x num_cols 的矩陣
  其中第(i,j)項就是 entry_fn(i,j)
  """

  return [[entry_fn(i,j) #只要給定i，就建立一個長度為j的列表
      for j in range(num_cols)] #[entry_fn(i,0),...]
      for i in range(num_rows)] #針對每個i都建立一個列表
```
##
* <font color="#0080FF">**(續)生成矩陣 - make_matrix**</font>

```python=+
"""有了這個函式，你就可以輕易建立一個5*5的單位矩陣(對角元素都是1，其餘元素都是0)"""
def identity_matrix(n :int) -> Matrix:
  """送回一個 n * n 的單位矩陣"""
  return make_matrix(n,n, lambda i,j : 1 if i == j else 0)

assert identity_matrix(5) == [[1,0,0,0,0],
                              [0,1,0,0,0],
                              [0,0,1,0,0],
                              [0,0,0,1,0],
                              [0,0,0,0,1]]

print("identity_matrix(5) =",identity_matrix(5))
```

> ```identity_matrix(5) = [[1, 0, 0, 0, 0], [0, 1, 0, 0, 0], [0, 0, 1, 0, 0], [0, 0, 0, 1, 0], [0, 0, 0, 0, 1]]```
##
> <font color="#EA0000" >**#矩陣非常重要，理由有好幾個...不告訴你，請自行體會~=OwO=~**</font>

## 時間戳記

> [name=ZEOxO][time=Sat, Nov 28 2020 15:10 PM][color=#907bf7]