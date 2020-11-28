# b.資料科學 - matplotlib資料視覺化

###### tags: `Data Sicnce From Scratch`

## 1.matplotlib函式庫

* <font color="#0080FF">**折線圖：一個簡單的折線圖**</font>

```python=+
"""1950年-2010年的"名義GDP"(隨機)"""
import random
from matplotlib import pyplot as plt

years = [year for year in range(1950,2011,10)]
gdp = []

for _ in range(len(years)):
  gdp.append(random.uniform(300,15000))

plt.plot(years,gdp,color = 'green',marker = 'o',linestyle = 'solid')
plt.title("Nominal GDP")
plt.ylabel("Billions of $")
plt.show() 
#或可用savefig將圖片存起來

print('years = ',years)
print('gdp = ',gdp)
```

> ![](https://i.imgur.com/YHCC7ik.png)</br>
> `years =  [1950, 1960, 1970, 1980, 1990, 2000, 2010]`</br>
> `gdp =  [6734.843618957465, 8517.466737974524, 3780.230438534374, 14288.651167138727, 11342.248822669268, 8132.800795505929, 13064.560618823463]`
## 

## 2.長條圖

* <font color="#0080FF">**長條圖：一個簡單的長條圖**</font>

> <font color="#EA0000" >**#長條圖：適合呈現離散項目間的數量變化**</font>

```python=+
"""我喜歡的電影"""
movies = ['Annie Hall','Ben-hur','Casablanca','Gandhi','West Side Story']
num_oscars = [5,11,3,8,10]

#以[0,1,2,3,4]為x軸
#以[5,11,3,8,10]為y軸
plt.bar(range(len(movies)),num_oscars)

plt.title("My Favorite Movies")
plt.ylabel("# of Academy Awards") #得獎次數

plt.xticks(range(len(movies)),movies)#把電影名稱當作x軸的標籤

plt.show()
```

> ![](https://i.imgur.com/zHHIJ5I.png)

##

* <font color="#0080FF">**長條圖：用長條圖來繪製直方圖**</font>

```python=+
"""第一次考試的分數分布"""
from collections import Counter #計數器

grades = [83,95,91,87,70,0,85,82,100,67,73,77,0]

histogram = Counter(min(grade // 10 * 10, 90) for grade in grades)

plt.bar([x + 5 for x in histogram.keys()], #將長條圖全部向右移動5個單位
    histogram.values(),
    10, #長條圖寬度設定為10(bar的第三個參數設定寬度)
    edgecolor = (0,0,0)) #將長條圖加上黑色邊框

plt.axis([-5,105,0,5]) #x軸範圍[-5到105],y軸範圍[0到5]

plt.xticks([10 * i for i in range(11)])
plt.xlabel('Decile')
plt.ylabel('# of students')
plt.title('Distribution of Exam 1 Grades')
plt.show()
 
print(histogram)
```

> ![](https://i.imgur.com/wAnLyvu.png)

> ```Counter({80: 4, 90: 3, 70: 3, 0: 2, 60: 1})```
##
* <font color="#0080FF">**長條圖：y軸會造成誤導的一張圖形**</font>

```python=+
"""看看增加的量多麼大呀!"""
mentions = [500,505]
years = [2017,2018]

plt.bar(years,mentions,0.8)
plt.xticks(years)
plt.ylabel("# of times I heard someone say 'data science'")

#如果不這麼做的話，
plt.ticklabel_format(useOffset = False)

plt.axis([2016.5,2018.5,499,506])
plt.title("Look at the 'Huge' Increase")
plt.show()
```

> ![](https://i.imgur.com/rbMGTqb.png)
##
* <font color="#0080FF">**(續)長條圖：不在y軸刻意造成誤導效果的同一張圖形**</font>

```python=+
"""看起來沒這麼大了"""
mentions = [500,505]
years = [2017,2018]

plt.bar(years,mentions,0.8)
plt.xticks(years)
plt.ylabel("# of times I heard someone say 'data science'")

#如果不這麼做的話，
plt.ticklabel_format(useOffset = False)

plt.axis([2016.5,2018.5,0,550])
plt.title("Not So Huge Anymore")
plt.show() #把y軸範圍調整較合理的座標軸
```

>![](https://i.imgur.com/wz7LUUI.png)

## 3.折線圖

* <font color="#0080FF">**折線圖：帶有圖例說明的多條折線圖**</font>

> <font color="#EA0000" >**#折線圖：適合用來呈現趨勢**</font>

```python=+
"""「偏差」與「變異」之間的取捨"""
def sequence(times,ls = [1]):
  for i in range(1,times):
    ls.append(ls[i-1] * 2)
  return ls 

variance = sequence(9)
bias_squared = sorted(variance,reverse = True)
total_error = [x+y for x,y in zip(variance,bias_squared)]
xs = [i for i,_ in enumerate(variance)]

plt.plot(xs,variance,'g-', label = 'variance') #綠色實線
plt.plot(xs,bias_squared,'r-.', label = 'bias^2') #紅色點虛線
plt.plot(xs,total_error,'b:', label = 'total error') #藍色點線

plt.legend(loc = 9)
plt.xlabel("model complexity")
plt.xticks([])
plt.title("The Bias-Variance Tradeoff")
plt.show()

print("variance = ",variance)
print("bias_squared = ",bias_squared)
print("total_error = ",total_error)
```

> ![](https://i.imgur.com/F1xT2uc.png)</br>
> ```variance =  [1, 2, 4, 8, 16, 32, 64, 128, 256]```</br>
> ```bias_squared =  [256, 128, 64, 32, 16, 8, 4, 2, 1]```</br>
> ```total_error =  [257, 130, 68, 40, 32, 40, 68, 130, 257]```

## 4.散點圖

* <font color="#0080FF">**散點圖：朋友數量與網站使用時間**</font>

> <font color="#EA0000" >**#散點圖：適合呈現兩組成對資料的關係**</font>

```python=+
"""每日分鐘數vs朋友數量"""
friends = [70,65,72,63,71,64,60,64,67]
minutes = [175,170,205,120,220,130,105,145,190]
labels = ['a','b','c','d','e','f','g','h','i']

plt.scatter(friends,minutes)

#每個點的標籤
for label,friends_count,minute_count in zip(labels,friends,minutes):
  plt.annotate(label,
        xy = (friends_count,minute_count), #把標籤放到相應的點上
        xytext = (5,-5), #稍微平移一下
        textcoords = 'offset points')

plt.title("Daily Minutes vs. Number of Friends")
plt.xlabel("# of friends")
plt.ylabel("daily minutes spent on the site")
plt.show()
```

>![](https://i.imgur.com/5gqDjU3.png)
##
* <font color="#0080FF">**散點圖：坐標軸無法進行比較的散點圖**</font>

```python=+
"""座標軸無法進行比較"""
test1_grades = [99,90,85,97,80]
test2_grades = [100,85,60,90,70] #比較兩次考試的成績

plt.scatter(test1_grades,test2_grades)
plt.title("Axes Aren't Comparable")
plt.xlabel("test 1 grade")
plt.ylabel("test 2 grade")
plt.show() #如果製作散點圖，讓matplotlib自動設定刻度的話，可能會產生具有誤導性的圖形
```

>![](https://i.imgur.com/IA8ky1J.png)
## 
* <font color="#0080FF">**(續)散點圖：坐標軸設定為相同尺度後的同一個散點圖**</font>
```python=+
"""坐標軸可以進行比較"""
test1_grades = [99,90,85,97,80]
test2_grades = [100,85,60,90,70] #比較兩次考試的成績

plt.scatter(test1_grades,test2_grades)
plt.title("Axes Are Comparable")
plt.xlabel("test 1 grade")
plt.ylabel("test 2 grade")
plt.axis('equal')
plt.show() #使用「plt.axis('equal')」就可以讓x,y的起訖點都相同
```

> ![](https://i.imgur.com/2WXN4ll.png)

## 時間戳記

> [name=ZEOxO][time=Sat, Nov 28 2020 13:50 PM][color=#907bf7]
