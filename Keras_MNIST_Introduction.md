# a.Keras MNIST 手寫數字辨識資料集介紹

###### tags: `Deep Learning` `Python` `Keras` 

## 1.Keras 手寫辨識介紹

* <font color="#0080FF">**匯入模組**</font>

```python=+
import numpy as np
import pandas as pd

from keras.utils import np_utils
np.random.seed(10)
```
##
* <font color="#0080FF">**讀取訓練及驗證資料**</font>

```python=+
from keras.datasets import mnist
(x_train_image,y_train_label), \
(x_test_image,y_test_label) = mnist.load_data() #第一次需下載
```

> ```11493376/11490434 [==============================] - 0s 0us/step```
##
* <font color="#0080FF">**查看資料筆數(長度)**</font>

```python=+
print('train_data =',len(x_train_image))
print(' test_data =',len(x_test_image))
```

> ```train_data = 60000```
> ``` test_data = 10000```
##
* <font color="#0080FF">**查看訓練資料**</font>

```python=+
print('測試資料:')
print('x_test_image =',x_test_image.shape)
print('y_test_label =',y_test_label.shape)
```

> ```測試資料：```
> ```x_test_image = (10000, 28, 28)```
> ```y_test_label = (10000,)```
##
* <font color="#0080FF">**查看驗證資料**</font>

```python=+
print('訓練資料:')
print('x_train_image =',x_train_image.shape)
print('y_train_label =',y_train_label.shape)
```

> ```訓練資料：```
> ```x_train_image = (60000, 28, 28)```
> ```y_train_label = (60000,)```
##
* <font color="#0080FF">**查看圖形(函式)**</font>

```python=+
import matplotlib.pyplot as plt
def plot_image(image):
    fig = plt.gcf()
    fig.set_size_inches(2,2)
    plt.imshow(image,cmap = 'binary')
    plt.show()
```
##
* <font color="#0080FF">**查看第一筆圖形**</font>

```python=+
plot_image(x_train_image[0])
```

> ![](https://i.imgur.com/6p5Nbsb.png)