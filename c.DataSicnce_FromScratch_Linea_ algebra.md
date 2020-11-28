# c.資料科學 - 線性代數

###### tags: `Data Sicnce From Scratch`

## 1.向量 Vector

* <font color="#0080FF">**向量(vector)即是一個"浮點數列表"**</font>

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

## 時間戳記

> [name=ZEOxO][time=Sat, Nov 28 2020 14:06 PM][color=#907bf7]