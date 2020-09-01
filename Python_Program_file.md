# Python - 程式檔

###### tags: `Python`

## 1.主程式、函式

* <font color="#0080FF">**將主程式放入主控函式**</font>

```python=+
def compare_num_of_chars(st):
    return len(st)

def main():
    word_list = ['SUSHI','RAMEN']
    word_list.sort(key = compare_num_of_chars)
    
main()
```