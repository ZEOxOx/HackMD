# o.Python - 常規表達式(regular_expression)

###### tags: `Python`

## 1.常規表達式基礎

<font color="#0080FF">**hello.txt**</font>

```python=+
Hello World!
Hello Python!
```
##
* <font color="#0080FF">**給予特定字串樣式做配對**</font>

```python=+
import re,os
regexp = re.compile('Hello') #指定字串樣式
count = 0

path = os.path.join(os.pardir,'document','hello.txt')
file = open(path,'r')
print('開啟檔案 :',path)

for line in file:
    if regexp.search(line): #尋找該字串內是否有指定字串
        count = count + 1
file.close()

print('>> 共找到',count,'行包含有 "Hello"')
```

> ```開啟檔案 : ..\document\hello.txt```</br>
> ```>> 共找到 2 行包含有 "Hello"```