# 資料科學 - Numpy 基礎篇

## 1.Numpy的基礎

* <font color="#0080FF">**Numpy 的匯入**</font>

```python=
#讀取numpy函式庫
import numpy as np
```
##
* <font color="#0080FF">**Numpy 魔術指令(Magic Command)**</font>

```python=+
#設定該檔案輸出顯示到小數點後第3位
%precision 3
```

## 2.陣列的操作

* <font color="#0080FF">**陣列**</font>

```python=+
#製作陣列
data = np.array([9,2,3,4,10,6,7,8,1,5])
data
```

> ```array([ 9,  2,  3,  4, 10,  6,  7,  8,  1,  5])```
##
* <font color="#0080FF">**資料型別**</font>

```python=+
#資料的型別
data.dtype
```

> ```dtype('int32')```
##
* <font color="#0080FF">**維度與元素數量**</font>

```python=+
print("維度:",data.ndim)
print("元素數量:",data.size)
```

> ```維度: 1 ```</br>
> ```元素數量: 10```
##
* <font color="#0080FF">**對所有的維度進行運算a**</font>

```python=+
#將各個數字乘上數倍(2倍為例)
data*2
```

> ```array([18,  4,  6,  8, 20, 12, 14, 16,  2, 10])```
## 
* <font color="#0080FF">**對所有的維度進行運算b**</font>
```python=+
print("乘法運算:",np.array([1,2,3,4,5,6,7,8,9,10]) * np.array([10,9,8,7,6,5,4,3,2,1]))
print("連乘:",np.array([1,2,3,4,5,6,7,8,9,10]) ** 2)
print("除法運算:",np.array([1,2,3,4,5,6,7,8,9,10]) / np.array([10,9,8,7,6,5,4,3,2,1]))
```

> ```乘法運算: [10 18 24 28 30 30 28 24 18 10]```</br>
> ```連乘: [  1   4   9  16  25  36  49  64  81 100]```</br>
> ```除法運算: [ 0.1    0.222  0.375  0.571  0.833  1.2    1.75   2.667  4.5   10.   ]```
##
* <font color="#0080FF">**排序**</font>

```python=+
print("排序之前:",data)
data.sort()
print("排序之後:",data)
```

> ```排序之前: [ 9  2  3  4 10  6  7  8  1  5]```</br>
> ```排序之後: [ 1  2  3  4  5  6  7  8  9 10]```

##
* <font color="#0080FF">**排序(從大到小)**</font>
```python=+
#從尾端開始逐一取出排列
data[::-1].sort()
print('排序之後:',data)
```
> ```排序之後: [10  9  8  7  6  5  4  3  2  1]```

##
* <font color="#0080FF">**最小、最大、總和、累積的計算**</font>
```python=+
#最大值
print("Min:",data.min())
#最小值
print("Max:",data.max())
#總和
print("Sum:",data.sum())
#累積和
print("CumSum:",data.cumsum())
#累積比例
print("Ratio:",data.cumsum() / data.sum())
```
> ```Min: 1``` </br>
> ```Max: 10``` </br>
> ```Sum: 55``` </br>
> ```CumSum: [10 19 27 34 40 45 49 52 54 55]``` </br>
> ```Ratio: [0.182 0.345 0.491 0.618 0.727 0.818 0.891 0.945 0.982 1.   ]``` </br>


## 時間戳記
> [name=ZEOxO][time=Mon, Aug 17, 2020 15:18 PM][color=#907bf7]