
# 数据分组运算


```python
import pandas as pd
import numpy as np
```


```python
# 分组运算后保持shape
dict_obj = {'key1' : ['a', 'b', 'a', 'b', 
                      'a', 'b', 'a', 'a'],
            'key2' : ['one', 'one', 'two', 'three',
                      'two', 'two', 'one', 'three'],
            'data1': np.random.randint(1, 10, 8),
            'data2': np.random.randint(1, 10, 8)}
df_obj = pd.DataFrame(dict_obj)
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
      <th>data1</th>
      <th>data2</th>
      <th>key1</th>
      <th>key2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>6</td>
      <td>a</td>
      <td>one</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>3</td>
      <td>b</td>
      <td>one</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>3</td>
      <td>a</td>
      <td>two</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>7</td>
      <td>b</td>
      <td>three</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>1</td>
      <td>a</td>
      <td>two</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>b</td>
      <td>two</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>3</td>
      <td>a</td>
      <td>one</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>2</td>
      <td>a</td>
      <td>three</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 按key1分组后，计算data1，data2的统计信息并附加到原始表格中
k1_sum = df_obj.groupby('key1').mean().add_prefix('mean_')
k1_sum
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
      <th>mean_data1</th>
      <th>mean_data2</th>
    </tr>
    <tr>
      <th>key1</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>7.200000</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>5.333333</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 方法1，使用merge
pd.merge(df_obj, k1_sum, left_on='key1', right_index=True)
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
      <th>data1</th>
      <th>data2</th>
      <th>key1</th>
      <th>key2</th>
      <th>mean_data1</th>
      <th>mean_data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>6</td>
      <td>a</td>
      <td>one</td>
      <td>7.200000</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>3</td>
      <td>a</td>
      <td>two</td>
      <td>7.200000</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>1</td>
      <td>a</td>
      <td>two</td>
      <td>7.200000</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>3</td>
      <td>a</td>
      <td>one</td>
      <td>7.200000</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>2</td>
      <td>a</td>
      <td>three</td>
      <td>7.200000</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>3</td>
      <td>b</td>
      <td>one</td>
      <td>5.333333</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>7</td>
      <td>b</td>
      <td>three</td>
      <td>5.333333</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>b</td>
      <td>two</td>
      <td>5.333333</td>
      <td>4.0</td>
    </tr>
  </tbody>
</table>
</div>



* transform方法


```python
# 方法2，使用transform
k1_sum_tf = df_obj.groupby('key1').transform(np.mean).add_prefix('mean_')
print(k1_sum_tf)
df_obj[k1_sum_tf.columns] = k1_sum_tf
df_obj
```

       mean_data1  mean_data2
    0    7.200000           3
    1    5.333333           4
    2    7.200000           3
    3    5.333333           4
    4    7.200000           3
    5    5.333333           4
    6    7.200000           3
    7    7.200000           3
    




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
      <th>data1</th>
      <th>data2</th>
      <th>key1</th>
      <th>key2</th>
      <th>mean_data1</th>
      <th>mean_data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>6</td>
      <td>a</td>
      <td>one</td>
      <td>7.200000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>3</td>
      <td>b</td>
      <td>one</td>
      <td>5.333333</td>
      <td>4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>3</td>
      <td>a</td>
      <td>two</td>
      <td>7.200000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>7</td>
      <td>b</td>
      <td>three</td>
      <td>5.333333</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>1</td>
      <td>a</td>
      <td>two</td>
      <td>7.200000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>6</td>
      <td>2</td>
      <td>b</td>
      <td>two</td>
      <td>5.333333</td>
      <td>4</td>
    </tr>
    <tr>
      <th>6</th>
      <td>8</td>
      <td>3</td>
      <td>a</td>
      <td>one</td>
      <td>7.200000</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3</td>
      <td>2</td>
      <td>a</td>
      <td>three</td>
      <td>7.200000</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 自定义函数传入transform
def diff_mean(s):
    """
        返回数据与均值的差值
    """
    return s - s.mean()

df_obj.groupby('key1').transform(diff_mean)
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
      <th>data1</th>
      <th>data2</th>
      <th>mean_data1</th>
      <th>mean_data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.800000</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.666667</td>
      <td>-1</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.800000</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>-3.333333</td>
      <td>3</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.800000</td>
      <td>-2</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.666667</td>
      <td>-2</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0.800000</td>
      <td>0</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-4.200000</td>
      <td>-1</td>
      <td>0.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
dataset_path = './starcraft.csv'
df_data = pd.read_csv(dataset_path, usecols=['LeagueIndex', 'Age', 'HoursPerWeek', 
                                             'TotalHours', 'APM'])
```

* apply


```python
def top_n(df, n=3, column='APM'):
    """
        返回每个分组按 column 的 top n 数据
    """
    return df.sort_values(by=column, ascending=False)[:n]

df_data.groupby('LeagueIndex').apply(top_n)
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
      <th></th>
      <th>LeagueIndex</th>
      <th>Age</th>
      <th>HoursPerWeek</th>
      <th>TotalHours</th>
      <th>APM</th>
    </tr>
    <tr>
      <th>LeagueIndex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="3" valign="top">1</th>
      <th>2214</th>
      <td>1</td>
      <td>20.0</td>
      <td>12.0</td>
      <td>730.0</td>
      <td>172.9530</td>
    </tr>
    <tr>
      <th>2246</th>
      <td>1</td>
      <td>27.0</td>
      <td>8.0</td>
      <td>250.0</td>
      <td>141.6282</td>
    </tr>
    <tr>
      <th>1753</th>
      <td>1</td>
      <td>20.0</td>
      <td>28.0</td>
      <td>100.0</td>
      <td>139.6362</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">2</th>
      <th>3062</th>
      <td>2</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>100.0</td>
      <td>179.6250</td>
    </tr>
    <tr>
      <th>3229</th>
      <td>2</td>
      <td>16.0</td>
      <td>24.0</td>
      <td>110.0</td>
      <td>156.7380</td>
    </tr>
    <tr>
      <th>1520</th>
      <td>2</td>
      <td>29.0</td>
      <td>6.0</td>
      <td>250.0</td>
      <td>151.6470</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">3</th>
      <th>1557</th>
      <td>3</td>
      <td>22.0</td>
      <td>6.0</td>
      <td>200.0</td>
      <td>226.6554</td>
    </tr>
    <tr>
      <th>484</th>
      <td>3</td>
      <td>19.0</td>
      <td>42.0</td>
      <td>450.0</td>
      <td>220.0692</td>
    </tr>
    <tr>
      <th>2883</th>
      <td>3</td>
      <td>16.0</td>
      <td>8.0</td>
      <td>800.0</td>
      <td>208.9500</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">4</th>
      <th>2688</th>
      <td>4</td>
      <td>26.0</td>
      <td>24.0</td>
      <td>990.0</td>
      <td>249.0210</td>
    </tr>
    <tr>
      <th>1759</th>
      <td>4</td>
      <td>16.0</td>
      <td>6.0</td>
      <td>75.0</td>
      <td>229.9122</td>
    </tr>
    <tr>
      <th>2637</th>
      <td>4</td>
      <td>23.0</td>
      <td>24.0</td>
      <td>650.0</td>
      <td>227.2272</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">5</th>
      <th>3277</th>
      <td>5</td>
      <td>18.0</td>
      <td>16.0</td>
      <td>950.0</td>
      <td>372.6426</td>
    </tr>
    <tr>
      <th>93</th>
      <td>5</td>
      <td>17.0</td>
      <td>36.0</td>
      <td>720.0</td>
      <td>335.4990</td>
    </tr>
    <tr>
      <th>202</th>
      <td>5</td>
      <td>37.0</td>
      <td>14.0</td>
      <td>800.0</td>
      <td>327.7218</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">6</th>
      <th>734</th>
      <td>6</td>
      <td>16.0</td>
      <td>28.0</td>
      <td>730.0</td>
      <td>389.8314</td>
    </tr>
    <tr>
      <th>2746</th>
      <td>6</td>
      <td>16.0</td>
      <td>28.0</td>
      <td>4000.0</td>
      <td>350.4114</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>6</td>
      <td>21.0</td>
      <td>14.0</td>
      <td>730.0</td>
      <td>323.2506</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">7</th>
      <th>3127</th>
      <td>7</td>
      <td>23.0</td>
      <td>42.0</td>
      <td>2000.0</td>
      <td>298.7952</td>
    </tr>
    <tr>
      <th>104</th>
      <td>7</td>
      <td>21.0</td>
      <td>24.0</td>
      <td>1000.0</td>
      <td>286.4538</td>
    </tr>
    <tr>
      <th>1654</th>
      <td>7</td>
      <td>18.0</td>
      <td>98.0</td>
      <td>700.0</td>
      <td>236.0316</td>
    </tr>
    <tr>
      <th rowspan="3" valign="top">8</th>
      <th>3393</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>375.8664</td>
    </tr>
    <tr>
      <th>3373</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>364.8504</td>
    </tr>
    <tr>
      <th>3372</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>355.3518</td>
    </tr>
  </tbody>
</table>
</div>




```python
# apply函数接收的参数会传入自定义的函数中
df_data.groupby('LeagueIndex').apply(top_n, n=2, column='Age')
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
      <th></th>
      <th>LeagueIndex</th>
      <th>Age</th>
      <th>HoursPerWeek</th>
      <th>TotalHours</th>
      <th>APM</th>
    </tr>
    <tr>
      <th>LeagueIndex</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">1</th>
      <th>3146</th>
      <td>1</td>
      <td>40.0</td>
      <td>12.0</td>
      <td>150.0</td>
      <td>38.5590</td>
    </tr>
    <tr>
      <th>3040</th>
      <td>1</td>
      <td>39.0</td>
      <td>10.0</td>
      <td>500.0</td>
      <td>29.8764</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">2</th>
      <th>920</th>
      <td>2</td>
      <td>43.0</td>
      <td>10.0</td>
      <td>730.0</td>
      <td>86.0586</td>
    </tr>
    <tr>
      <th>2437</th>
      <td>2</td>
      <td>41.0</td>
      <td>4.0</td>
      <td>200.0</td>
      <td>54.2166</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">3</th>
      <th>1258</th>
      <td>3</td>
      <td>41.0</td>
      <td>14.0</td>
      <td>800.0</td>
      <td>77.6472</td>
    </tr>
    <tr>
      <th>2972</th>
      <td>3</td>
      <td>40.0</td>
      <td>10.0</td>
      <td>500.0</td>
      <td>60.5970</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">4</th>
      <th>1696</th>
      <td>4</td>
      <td>44.0</td>
      <td>6.0</td>
      <td>500.0</td>
      <td>89.5266</td>
    </tr>
    <tr>
      <th>1729</th>
      <td>4</td>
      <td>39.0</td>
      <td>8.0</td>
      <td>500.0</td>
      <td>86.7246</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">5</th>
      <th>202</th>
      <td>5</td>
      <td>37.0</td>
      <td>14.0</td>
      <td>800.0</td>
      <td>327.7218</td>
    </tr>
    <tr>
      <th>2745</th>
      <td>5</td>
      <td>37.0</td>
      <td>18.0</td>
      <td>1000.0</td>
      <td>123.4098</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">6</th>
      <th>3069</th>
      <td>6</td>
      <td>31.0</td>
      <td>8.0</td>
      <td>800.0</td>
      <td>133.1790</td>
    </tr>
    <tr>
      <th>2706</th>
      <td>6</td>
      <td>31.0</td>
      <td>8.0</td>
      <td>700.0</td>
      <td>66.9918</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">7</th>
      <th>2813</th>
      <td>7</td>
      <td>26.0</td>
      <td>36.0</td>
      <td>1300.0</td>
      <td>188.5512</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>7</td>
      <td>26.0</td>
      <td>24.0</td>
      <td>1000.0</td>
      <td>219.6690</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">8</th>
      <th>3340</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>189.7404</td>
    </tr>
    <tr>
      <th>3341</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>287.8128</td>
    </tr>
  </tbody>
</table>
</div>



* 禁止分组 group_keys=False


```python
df_data.groupby('LeagueIndex', group_keys=False).apply(top_n)
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
      <th>LeagueIndex</th>
      <th>Age</th>
      <th>HoursPerWeek</th>
      <th>TotalHours</th>
      <th>APM</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2214</th>
      <td>1</td>
      <td>20.0</td>
      <td>12.0</td>
      <td>730.0</td>
      <td>172.9530</td>
    </tr>
    <tr>
      <th>2246</th>
      <td>1</td>
      <td>27.0</td>
      <td>8.0</td>
      <td>250.0</td>
      <td>141.6282</td>
    </tr>
    <tr>
      <th>1753</th>
      <td>1</td>
      <td>20.0</td>
      <td>28.0</td>
      <td>100.0</td>
      <td>139.6362</td>
    </tr>
    <tr>
      <th>3062</th>
      <td>2</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>100.0</td>
      <td>179.6250</td>
    </tr>
    <tr>
      <th>3229</th>
      <td>2</td>
      <td>16.0</td>
      <td>24.0</td>
      <td>110.0</td>
      <td>156.7380</td>
    </tr>
    <tr>
      <th>1520</th>
      <td>2</td>
      <td>29.0</td>
      <td>6.0</td>
      <td>250.0</td>
      <td>151.6470</td>
    </tr>
    <tr>
      <th>1557</th>
      <td>3</td>
      <td>22.0</td>
      <td>6.0</td>
      <td>200.0</td>
      <td>226.6554</td>
    </tr>
    <tr>
      <th>484</th>
      <td>3</td>
      <td>19.0</td>
      <td>42.0</td>
      <td>450.0</td>
      <td>220.0692</td>
    </tr>
    <tr>
      <th>2883</th>
      <td>3</td>
      <td>16.0</td>
      <td>8.0</td>
      <td>800.0</td>
      <td>208.9500</td>
    </tr>
    <tr>
      <th>2688</th>
      <td>4</td>
      <td>26.0</td>
      <td>24.0</td>
      <td>990.0</td>
      <td>249.0210</td>
    </tr>
    <tr>
      <th>1759</th>
      <td>4</td>
      <td>16.0</td>
      <td>6.0</td>
      <td>75.0</td>
      <td>229.9122</td>
    </tr>
    <tr>
      <th>2637</th>
      <td>4</td>
      <td>23.0</td>
      <td>24.0</td>
      <td>650.0</td>
      <td>227.2272</td>
    </tr>
    <tr>
      <th>3277</th>
      <td>5</td>
      <td>18.0</td>
      <td>16.0</td>
      <td>950.0</td>
      <td>372.6426</td>
    </tr>
    <tr>
      <th>93</th>
      <td>5</td>
      <td>17.0</td>
      <td>36.0</td>
      <td>720.0</td>
      <td>335.4990</td>
    </tr>
    <tr>
      <th>202</th>
      <td>5</td>
      <td>37.0</td>
      <td>14.0</td>
      <td>800.0</td>
      <td>327.7218</td>
    </tr>
    <tr>
      <th>734</th>
      <td>6</td>
      <td>16.0</td>
      <td>28.0</td>
      <td>730.0</td>
      <td>389.8314</td>
    </tr>
    <tr>
      <th>2746</th>
      <td>6</td>
      <td>16.0</td>
      <td>28.0</td>
      <td>4000.0</td>
      <td>350.4114</td>
    </tr>
    <tr>
      <th>1810</th>
      <td>6</td>
      <td>21.0</td>
      <td>14.0</td>
      <td>730.0</td>
      <td>323.2506</td>
    </tr>
    <tr>
      <th>3127</th>
      <td>7</td>
      <td>23.0</td>
      <td>42.0</td>
      <td>2000.0</td>
      <td>298.7952</td>
    </tr>
    <tr>
      <th>104</th>
      <td>7</td>
      <td>21.0</td>
      <td>24.0</td>
      <td>1000.0</td>
      <td>286.4538</td>
    </tr>
    <tr>
      <th>1654</th>
      <td>7</td>
      <td>18.0</td>
      <td>98.0</td>
      <td>700.0</td>
      <td>236.0316</td>
    </tr>
    <tr>
      <th>3393</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>375.8664</td>
    </tr>
    <tr>
      <th>3373</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>364.8504</td>
    </tr>
    <tr>
      <th>3372</th>
      <td>8</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>355.3518</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
