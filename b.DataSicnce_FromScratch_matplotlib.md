# b. 資料視覺化

###### tags: `Data Sicnce From Scratch`

## 1.折線圖

```python=+
"""一個簡單的折線圖"""
import random
from matplotlib import pyplot as plt

years = [year for year in range(1950,2011,10)]
gdp = []

for _ in range(len(years)):
  gdp.append(random.uniform(300,15000))

plt.plot(years,gdp,color = 'green',marker = 'o',linestyle = 'solid')
plt.title("Normal GDP")
plt.ylabel("Billions of $")
plt.show()

print('years = ',years)
print('gdp = ',gdp)
```

> ![](https://i.imgur.com/qxMPvzj.png)</br>
> `years =  [1950, 1960, 1970, 1980, 1990, 2000, 2010]`</br>
> `gdp =  [5225.591334178381, 6996.385220343473, 3034.1321408808244, 1532.847161442601, 5937.372812363477, 310.1199318349262, 5948.25556659076]`

