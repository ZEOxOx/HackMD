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

> ```train_data = 60000```</br>
> ``` test_data = 10000```</br>
##
* <font color="#0080FF">**查看訓練資料**</font>

```python=+
print('測試資料:')
print('x_test_image =',x_test_image.shape)
print('y_test_label =',y_test_label.shape)
```

> ```測試資料：```</br>
> ```x_test_image = (10000, 28, 28)```</br>
> ```y_test_label = (10000,)```
##
* <font color="#0080FF">**查看驗證資料**</font>

```python=+
print('訓練資料:')
print('x_train_image =',x_train_image.shape)
print('y_train_label =',y_train_label.shape)
```

> ```訓練資料：```</br>
> ```x_train_image = (60000, 28, 28)```</br>
> ```y_train_label = (60000,)```
##
* <font color="#0080FF">**顯示圖形 的函式**</font>

```python=+
import matplotlib.pyplot as plt
def plot_image(image):
    fig = plt.gcf()
    fig.set_size_inches(2,2)
    plt.imshow(image,cmap = 'binary')
    plt.show()
```
##
* <font color="#0080FF">**顯示第一筆圖形 (Image)**</font>

```python=+
plot_image(x_train_image[0])
```

> ![](https://i.imgur.com/6p5Nbsb.png)
##
* <font color="#0080FF">**查看第一筆標籤 (Label)**</font>

```python=+
plot_image(x_train_image[0])
```

> ```5```
##
* <font color="#0080FF">**顯示多筆(Multiple)圖片 的函式**</font>

```python=+
import matplotlib.pyplot as plt
def plot_images_labels_prediction(images,labels,prediction,idx,num = 10):
  fig = plt.gcf()
  fig.set_size_inches(12,14)
  if num >= 25:num = 25
  for i in range(0,num):
    ax = plt.subplot(5,5,i+1)
    ax.imshow(images[idx],cmap='binary')
    title = 'label = ' + str(labels[idx])
    if(len(prediction)) > 0:
      title += ',predict = ' + str(prediction[idx])
    ax.set_title(title,fontsize = 10)
    ax.set_xticks([]);ax.set_yticks([])
    idx += 1
  plt.show
```
##
* <font color="#0080FF">**顯示多筆圖片**</font>

```python=+
plot_images_labels_prediction(x_train_image,y_train_label,[],0,10)
```

> ![](https://i.imgur.com/UGJ392u.png)

## 2.資料預處理 (圖片)

* <font color="#0080FF">**查看訓練及驗證資料 筆數**</font>

```python=+
print('x_train_image =',x_train_image.shape)
print('x_test_image =',x_test_image.shape)
```

> ```x_train_image = (60000, 28, 28)```</br>
> ```x_test_image = (10000, 28, 28)```
##
* <font color="#0080FF">**將圖片(二維) 轉為 數值(一維)**</font>

```python=+
x_train = x_train_image.reshape(60000,784).astype('float32')
x_test = x_test_image.reshape(10000,784).astype('float32')
```
##
* <font color="#0080FF">**轉換後的圖片 形狀(shape)**</font>
```python=+
print('x_train =',x_train.shape)
print('x_test =',x_test.shape)
```

> ```x_train = (60000, 784)```
> ```x_test = (10000, 784)```
##
* <font color="#0080FF">**轉換後的第一筆 圖片(Image)之數值**</font>
```python=+
print('x_train =',x_train.shape)
print('x_test =',x_test.shape)
```

> ```array([  0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,...,136., 253., 253., 253., 212., 135., 132.,  16.,   0.,   0.,0.,   0.,   0.,   0.,...,   0.,   0.,   0.], dtype=float32)```
##
* <font color="#0080FF">**將圖片(Image)之數值 正規化**</font>
```python=+
x_train_normalize = x_train/255
x_test_normalize = x_test/255
```
##
* <font color="#0080FF">**將圖片(Image)之數值 正規化**</font>
```python=+
x_train_normalize[0]
```
> ```array([  0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,   0.,...,0.53333336, 0.99215686, 0.99215686, 0.99215686, 0.83137256, 0.5294118, 0.5176471, 0.0627451,   0.,   0.,0.,   0.,   0.,   0.,...,   0.,   0.,   0.], dtype=float32)```

## 3.資料預處理(標籤)

* <font color="#0080FF">**查看前五筆 標籤(Label)**</font>

```python=+
y_train_label[:5]
```

> ```array([5, 0, 4, 1, 9], dtype=uint8)```

##
* <font color="#0080FF">**將標籤(Label) 進行One-Hot encoding**</font>

```python=+
y_train_onehot = np_utils.to_categorical(y_train_label)
y_test_onehot = np_utils.to_categorical(y_test_label)
```
##
* <font color="#0080FF">**查看前五筆標籤(Label) One-Hot**</font>

```python=+
y_train_onehot[:5]
```

> ```array([[0., 0., 0., 0., 0., 1., 0., 0., 0., 0.],[1., 0., 0., 0., 0., 0., 0., 0., 0., 0.],[0., 0., 0., 0., 1., 0., 0., 0., 0., 0.],[0., 1., 0., 0., 0., 0., 0., 0., 0., 0.],[0., 0., 0., 0., 0., 0., 0., 0., 0., 1.]], dtype=float32)```

## 時間戳記

> [name=ZEOxO][time=Fri, Oct 2, 2020 14:53 PM][color=#907bf7]