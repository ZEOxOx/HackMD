# a.初探神經網路:第一支神經網路

###### tags: `Deep Learning by Keras God`

## 1.簡介

* <font color="#0080FF">**匯入手寫辨識資料集(Mnist)**</font>

```python=+
from keras.datasets import mnist

(train_img,train_label),(test_img,test_label) = mnist.load_data()
```

> ```11493376/11490434 [==============================] - 0s 0us/step```
##
* <font color="#0080FF">**建立模型及輸入層、輸出層**</font>

```python=+
from keras.models import Sequential
from keras.layers import Dense 

model = Sequential()
model.add(Dense(512,activation = 'relu',input_shape = (28*28,)))
model.add(Dense(10,activation = 'softmax'))
```
##
* <font color="#0080FF">**編譯模型**</font>

```python=+
model.compile(optimizer = 'rmsprop',
loss = 'categorical_crossentropy',
metrics = ['accuracy'])
```
##
* <font color="#0080FF">**資料預處理 - 將圖片正規化**</font>

```python=+
train_img = train_img.reshape(60000,28*28)
train_img = train_img.astype('float32') / 255

test_img = test_img.reshape(10000,28*28)
test_img = test_img.astype('float32') / 255
```
##
* <font color="#0080FF">**資料預處理 - 將標籤(數字)轉為one-hot**</font>

```python=+
from keras.utils import to_categorical

train_label = to_categorical(train_label)
test_label = to_categorical(test_label)
```
##
* <font color="#0080FF">**訓練模型**</font>

```python=+
model.fit(train_img,train_label,epochs = 5,batch_size = 128)
```

> ```Epoch 1/5```</br>
> ```469/469 [==============================] - 1s 3ms/step - loss: 0.2562 - accuracy: 0.9262```</br>
> ```<tensorflow.python.keras.callbacks.History at 0x7fa1e0141a58>```

##
* <font color="#0080FF">**評估模型**</font>

```python=+
test_loss,test_acc = model.evaluate(test_img,test_label)
print('test_acc:',test_acc)
```

> ```test_acc: 0.9815999865531921```

## 時間戳記

> [name=ZEOxO][time=Fri, Dec 06, 2020 15:03 PM][color=#907bf7]


