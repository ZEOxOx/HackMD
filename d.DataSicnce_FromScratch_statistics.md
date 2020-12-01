# d.資料科學 - Statistics統計學

###### tags: `Data Sicnce From Scratch`

## 1.

```python=+
import random as ran
num_friends = [ran.randint(1,100) for _ in range(204)]
print(num_friends)
```

> ```[57, 18, 50, 23, 33, 61, 55, 48, 88, 53, 85, 76, 90, 71, 33, 38, 71, 63, 56, 61, 34, 28, 61, 67, 92,...]```

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

![](https://i.imgur.com/KheQ3ae.png)

> ```Counter({76: 6, 58: 6, 3: 6, 5: 6, 57: 5, 23: 5, 93: 5, 33: 4, 61: 4, 85: 4, 34: 4, 45: 4, 30: 4, 10: 4, 90: 3, 38: 3, 56: 3,...})```
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
> ```2```

## 時間戳記

> [name=ZEOxO][time=Sat, Nov 30 2020 09:50 PM][color=#907bf7]