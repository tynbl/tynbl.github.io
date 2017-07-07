
# Pandas统计计算和描述


```python
import numpy as np
import pandas as pd
```

* 常用的统计计算


```python
df_obj = pd.DataFrame(np.random.randn(5,4), columns = ['a', 'b', 'c', 'd'])
df_obj
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.281460</td>
      <td>-0.458650</td>
      <td>-1.102619</td>
      <td>0.226367</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.045202</td>
      <td>-0.801324</td>
      <td>-2.910940</td>
      <td>-1.249168</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.260569</td>
      <td>-0.262852</td>
      <td>1.348291</td>
      <td>-0.103332</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-0.688225</td>
      <td>-0.658354</td>
      <td>-1.498003</td>
      <td>-1.288892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>-0.415888</td>
      <td>2.523040</td>
      <td>0.107214</td>
      <td>-0.849228</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_obj.sum()
```




    a   -0.170205
    b    0.341860
    c   -4.056056
    d   -3.264252
    dtype: float64




```python
df_obj.max()
```




    a    1.260569
    b    2.523040
    c    1.348291
    d    0.226367
    dtype: float64




```python
df_obj.min(axis=1)
```




    0   -1.102619
    1   -2.910940
    2   -0.262852
    3   -1.498003
    4   -0.849228
    dtype: float64



* 统计描述


```python
df_obj.describe()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
      <td>5.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>-0.034041</td>
      <td>0.068372</td>
      <td>-0.811211</td>
      <td>-0.652850</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.760118</td>
      <td>1.387206</td>
      <td>1.618056</td>
      <td>0.684416</td>
    </tr>
    <tr>
      <th>min</th>
      <td>-0.688225</td>
      <td>-0.801324</td>
      <td>-2.910940</td>
      <td>-1.288892</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>-0.415888</td>
      <td>-0.658354</td>
      <td>-1.498003</td>
      <td>-1.249168</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>-0.281460</td>
      <td>-0.458650</td>
      <td>-1.102619</td>
      <td>-0.849228</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>-0.045202</td>
      <td>-0.262852</td>
      <td>0.107214</td>
      <td>-0.103332</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.260569</td>
      <td>2.523040</td>
      <td>1.348291</td>
      <td>0.226367</td>
    </tr>
  </tbody>
</table>
</div>




```python

```


```python

```
