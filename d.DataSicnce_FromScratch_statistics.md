# d.資料科學 - Statistics統計學

###### tags: `Data Sicnce From Scratch`

## 1.瞭解資料

```python=+
import random as ran
num_friends = [ran.randint(1,100) for _ in range(204)]
print(num_friends)
```

> ```[59, 31, 30, 38, 89, 8, 39, 59, 57, 5, 1, 44, 87, 16, 38, 49, 2, 89, 61, 67, 2, 19, 96, 33,...]```

#
* <font color="#0080FF">**朋友數量的直方圖**</font>

```python=+
"""朋友數量直方圖"""
from collections import Counter
import matplotlib.pyplot as plt

friend_counts = Counter(num_friends)

xs = range(101)
ys = [friend_counts[x] for x in xs]

plt.bar(xs,ys)
plt.axis([0,101,0,20])
plt.title("Hisogram of Friend Counts")
plt.xlabel("# of friends")
plt.ylabel("# of people")
plt.show()
print(friend_counts)
```

> ![](https://i.imgur.com/Tyy1dux.png)


> ```Counter({38: 7, 14: 7, 16: 6, 59: 5, 67: 5, 73: 5, 90: 4, 100: 4, 22: 4, 75: 4, 64: 4, 65: 4, 3: 4, 42: 4, 31: 3,...})```
#

* <font color="#0080FF">**查看特定資料點**</font>

```python=+
num_points = len(num_friends)
largest_value = max(num_friends)
smallest_value = min(num_friends)

print(num_points)
print(largest_value)
print(smallest_value)
```

> ```204```</br>
> ```100```</br>
> ```1```
##
* <font color="#0080FF">**(續)查看特定資料點**</font>

```python=+
sorted_friends = sorted(num_friends)
largest_value = sorted_friends[-1]
smallest_value = sorted_friends[0]
second_largest_value = sorted_friends[-2]

print(largest_value)
print(smallest_value)
print(second_largest_value)
```

> ```100```</br>
> ```1```</br>
> ```100```

## 2.中央趨勢

* <font color="#0080FF">**平均值 (mean、average)**</font>

```python=+
from typing import List
def mean(xs:List[float]) -> float:
  return sum(xs) / len(xs)

mean(num_friends)
```

> ```50.205882352941174```
##
* <font color="#0080FF">**中位數 (median)**</font>

```python=+
"""針對奇數與偶數的情況，分別寫出不同函式"""
# 開頭的底線代表這兩個函式都是 private(私有的) 函式
# 因為這兩個函式主要是給中位數函式 median 使用
# 我們並不打算提供給統計函式庫外部的人使用
def _median_odd(xs:List[float]) -> float:
  """如果len(xs)是奇數，排序之後最中間那個值就是中位數"""
  return sorted(xs)[len(xs)//2]
  
def _median_even(xs:List[float]) -> float:
  """如果len(xs)是偶數，排序之後就取中間兩個值的平均值"""
  sorted_xs = sorted(xs)
  hi_midpoint = len(xs) // 2
  return mean([sorted_xs[hi_midpoint-1],sorted_xs[hi_midpoint]])
  #(或是)return (sorted_xs[hi_midpoint-1] + sorted_xs[hi_midpoint]) / 2
  
def median(v:List[float]):
  """找出v最中間的值(其實就是找出中位數)"""
  return _median_odd(v) if len(v) % 2 != 0 else _median_even(v)

assert median([1,10,2,9,5]) == 5
print(median([1,10,2,9,5]))
assert median([1,9,2,10]) == (2+9)/2
print(median([1,9,2,10]))
```

> ```5```</br>
> ```5.5```
##
* <font color="#0080FF">**(續)中位數 (median)**</font>

```python=+
"""我們可以算出朋友數量的中位數了!!"""
print(median(num_friends))
```

> ```50.5```
## 
* <font color="#0080FF">**分位數 (quantile)**</font>

```python=+
def quantile(xs:List[float],p:int) -> float:
  """送回xs裡面正好位於p百分比位置的那個數值"""
  sorted_xs = sorted(xs)

  divi = (p/100) * len(xs)
  right = int(str(divi).split(".")[1]) #查看小數點右邊是否為0
  #print(divi,"."+str(right))
  if (right != 0):
    num = int(divi)
    result = (sorted_xs[num])
  else:
    num = int(divi)
    result = (sorted_xs[num-1] + sorted_xs[num]) / 2 #(注意!!)陣列是從0開始
  return result

nums = [i for i in range(1,11)]
print(nums)

print(quantile(nums,1))
print(quantile(nums,50))
print(quantile(nums,90))
print(quantile(nums,99))
```

> ```[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]```</br>
> ```1```</br>
> ```5.5```</br>
> ```9.5```</br>
> ```10```

## 
* <font color="#0080FF">**(續)分位數 (quantile)**</font>

```python=+
"""我們可以算出朋友數量的分位數了!!"""
print(quantile(num_friends,1))
print(quantile(num_friends,50))
print(quantile(num_friends,90))
print(quantile(num_friends,99))
```

> ```1```</br>
> ```50.5```</br>
> ```90```</br>
> ```100```

## 時間戳記

> [name=ZEOxO][time=Mon, Nov 30 2020 09:50 PM][color=#907bf7]