
### 参考：
[线性回归之——最小二乘法](http://sbp810050504.blog.51cto.com/2799422/1269572)


```python
%matplotlib inline
```


```python
# -*- coding: utf-8 -*
import numpy as np
import os
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression

def drawScatterDiagram(fileName):
    L = [[float(x) for x in y.split(',')] for y in open('data1.csv').read().rstrip().split('\n')[:]]
    data1 = np.array(L)

    x = data1[:, 0:1]
    y = data1[:, 1:2]

    print('data review:\n', data1)
    #print(x)
    #print(x.ndim)
    #print(x.shape)
    #print(y)

    plt.scatter(x,y,s=30,c='red',marker='s')

    regr = LinearRegression()
    regr.fit(x,y)
    print('regr.coef_:\n', regr.coef_)
    plt.plot(x, regr.predict(x), color='blue')

    #a=0.1965;b=-14.486
    '''
    a = 0.1612; b = -8.6394
    x = np.arange(90.0, 250.0, 0.1)
    y = a*x+b
    plt.plot(x, y)
    '''
    plt.show()

drawScatterDiagram(r"data1.csv")

```

    data review:
     [[ 208.    21.6]
     [ 152.    15.5]
     [ 113.    10.4]
     [ 227.    31. ]
     [ 137.    13. ]
     [ 238.    32.4]
     [ 178.    19. ]
     [ 104.    10.4]
     [ 191.    19. ]
     [ 130.    11.8]]
    regr.coef_:
     [[ 0.16123404]]
    


![png](docs/images/linear-regression.png)



```python

```
