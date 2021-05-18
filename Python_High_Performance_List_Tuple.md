# a.Python - 高效能串列與元組 (List & Tuple)

###### tags: `High Performance Python`

## 1.時間複雜度-Table

| 串列查詢 | 時間複雜度 |
| :------: | :-----------: |
| <font color="#0080FF">**事先知道串列的順序**</font> | **O(1)** |
| <font color="#0080FF">**為串列進行線性搜尋**</font> | **O(n)** |

## 2.串列查詢

* <font color="#0080FF">**為不同尺寸的串列進行串列查詢所需耗費時間**</font>

```python=+
%timeit l = range(10)
%timeit l = range(10000000)
```

> ```The slowest run took 8.84 times longer than the fastest. This could mean that an intermediate result is being cached.```</br>
> ```10000000 loops, best of 5: 188 ns per loop```

> ```The slowest run took 6.65 times longer than the fastest. This could mean that an intermediate result is being cached.```</br>
> ```1000000 loops, best of 5: 240 ns per loop```
##
* <font color="#0080FF">**為串列進行線性搜尋**</font>

```python=+
def liner_search(needle,array):
  for i,item in enumerate(array):
    if(item == needle):
      return i
  return -1 #最壞的情況->找不到：O(n)
```



## 時間戳記

> [name=ZEOxO][time=Tue, May 18, 2020 12:30 PM][color=#907bf7]