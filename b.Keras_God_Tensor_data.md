# b.神經網路的資料表示法：張量Tensor

###### tags: `Deep Learning by Keras God`

> <font color="#EA0000" >**#結論：將多個3維張量放到陣列，會成為4維張量**</font>

> <font color="#EA0000" >**#同理：將多個4維張量放到陣列，會成為5維張量**</font>

## 1.張量的關鍵屬性

* <font color="#0080FF">**匯入手寫辨識資料集(Mnist)**</font>

```python=+
from keras.datasets import mnist
(train_img,train_label),(test_img,test_label) = mnist.load_data()
```

> ```11493376/11490434 [==============================] - 0s 0us/step```
##
* <font color="#0080FF">**瞭解資料**</font>

```python=+
print(train_img.ndim,train_img.shape,train_img.dtype)
```

> ```3 (60000, 28, 28) uint8```
##
* <font color="#0080FF">**查看圖片**</font>

```python=+
import matplotlib.pyplot as plt

digit = train_img[4] #查看第5張圖片
plt.imshow(digit,cmap = plt.cm.binary)
plt.show()
```

> ![](https://i.imgur.com/tjswIZj.png)

##
* <font color="#0080FF">**擷取特定資料**</font>

```python=+
my_slice = train_img[10:100]
print(my_slice.shape)

my_slice = train_img[10:100,:,:]
print(my_slice.shape)

my_slice = train_img[10:100,0:28,0:28]
print(my_slice.shape)
```

> ```(90, 28, 28)```</br>
> ```(90, 28, 28)```</br>
> ```(90, 28, 28)```

##
* <font color="#0080FF">**擷取圖片特定範圍**</font>

```python=+
#切出每張圖片右下角14*14的像素
my_slice = train_img[:,14:,14:]
print(my_slice.shape)

#擷取每張圖片居中的14*14像素
my_slice = train_img[:,7:-7,7:-7]
print(my_slice.shape)
```

> ```(60000, 14, 14)```</br>
> ```(60000, 14, 14)```