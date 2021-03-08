# a.資料科學 - Numpy 基礎篇

###### tags: `Data Science Tokyo`

## 1.函式庫

* <font color="#0080FF">**Magic Command 魔術指令 (Numpy及Matplotlib)**</font>

```python=+
%precision 3 #設定該檔案輸出顯示到小數點後第3位
%matplotlib inline #設定在該位置顯示圖表，而不是另開視窗
```

##
* <font color="#0080FF">**匯入本章節函式庫**</font>

```python=+
#為了使用下面的函式庫，請預先匯入
import numpy as np
import numpy.random as ran
import scipy as sp
import pandas as pd
from pandas import Series, DataFrame

#視覺化函式庫
import matplotlib.pyplot as plt
import matplotlib as mpl
import seaborn as sns
%matplotlib inline

#顯示到小數點第三位
%precision 3 
```

## 2.Numpy 的基礎

* <font color="#0080FF">**陣列的操作**</font>

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
* <font color="#0080FF">**對所有的維度進行運算**</font>

```python=+
#將各個數字乘上數倍(2倍為例)
data*2
```

> ```array([18,  4,  6,  8, 20, 12, 14, 16,  2, 10])```
## 
* <font color="#0080FF">**(續)對所有的維度進行運算**</font>
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
* <font color="#0080FF">**(續)排序**</font>
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

## 3.亂數

* <font color="#0080FF">**亂數**</font>

> <font color="#EA0000">**Python也有亂數功能，但資料科學領域通常使用「Numpy」的亂數功能**</font>

```python=+
import numpy.random as ran
ran.seed(0)

rand_data = random.randn(10)
print('含有10個亂數的陣列:',rand_data)
```

> ```含有10個亂數的陣列: [ 1.764  0.4    0.979  2.241  1.868 -0.977  0.95  -0.151 -0.103  0.411]```
##
* <font color="#0080FF">**資料的隨機取出**</font>

```python=+
data = np.array([9,2,3,4,10,6,7,8,1,5])

#取出10個(允許重複，放回抽樣)
print(ran.choice(data,10))

#取出10個(不允許重複，不放回抽樣)
print(ran.choice(data,10,replace=False))
```

> ```[ 7  8  8  1  2  6  5  1  5 10]```</br>
> ```[10  2  7  8  3  1  6  5  9  4]```
##
* <font color="#0080FF">**(!)Numpy非常快**</font>

```python=+
n = 10*6
normal_data = [ran.random() for _ in range(n)]

#Numpy版
numpy_random_data = np.array(normal_data)

#calc time:總和
#一般的處理
%timeit sum(normal_data)

#使用Numpy的處理
%timeit np.sum(numpy_random_data)
```

> ```The slowest run took 5.40 times longer than the fastest. This could mean that an intermediate result is being cached.1000000 loops, best of 3: 422 ns per loop```</br>
> ```The slowest run took 120.44 times longer than the fastest. This could mean that an intermediate result is being cached.100000 loops, best of 3: 4.14 µs per loop```

## 4.矩陣

* <font color="#0080FF">**矩陣的基礎**</font>

```python=+
array1 = np.arange(9).reshape(3,3)
print(array1)
```

> ```[[0 1 2]```</br>
> ```[3 4 5]```</br>
> ```[6 7 8]]```</br>
##
* <font color="#0080FF">**(續)矩陣的基礎**</font>

```python=+
print(array1[0,:]) #第一列，全部的行
array1[:,0] #所有列，第一行
```

> ```[0 1 2]```</br>
> ```array([0, 3, 6])```
##
* <font color="#0080FF">**矩陣的運算**</font>

```python=+
array2 = np.arange(9,18).reshape(3,3)
np.dot(array1,array2) #矩陣之積
```

> ```array([[ 42,  45,  48],```</br>
> ```[150, 162, 174],```</br>
> ```[258, 279, 300]])```
##
* <font color="#0080FF">**(續)矩陣的運算**</font>

```python=+
array1 * array2 #各自的元素進行乘法
```

> ```array([[  0,  10,  22],```</br>
> ```[ 36,  52,  70],```</br>
> ```[ 90, 112, 136]])```
## 
* <font color="#0080FF">**製作元素為0或1的矩陣**</font>

```python=+
print(np.zeros((2,3),dtype = np.int64))
print(np.ones((2,3),dtype = np.float64))
```

> ```[[0 0 0]```</br>
> ``` [0 0 0]]```</br>
> ```[[1. 1. 1.]```</br>
> ``` [1. 1. 1.]]```

## 時間戳記
> [name=ZEOxO][time=Mon, Mar 8, 2021 17:50 PM][color=#907bf7]