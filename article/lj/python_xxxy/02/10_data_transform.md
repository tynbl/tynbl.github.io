
# 数据转换


```python
import numpy as np
import pandas as pd
```

* 重复数据


```python
df_obj = pd.DataFrame({'data1' : ['a'] * 4 + ['b'] * 4,
                       'data2' : np.random.randint(0, 4, 8)})
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>b</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>b</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>b</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_obj.duplicated()
```




    0    False
    1    False
    2    False
    3     True
    4    False
    5    False
    6     True
    7     True
    dtype: bool




```python
df_obj.drop_duplicates()
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>b</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_obj.drop_duplicates('data2')
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>a</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



* map函数


```python
ser_obj = pd.Series(np.random.randint(0,10,10))
ser_obj
```




    0    7
    1    9
    2    1
    3    0
    4    8
    5    1
    6    6
    7    3
    8    9
    9    4
    dtype: int32




```python
ser_obj.map(lambda x : x ** 2)
```




    0    49
    1    81
    2     1
    3     0
    4    64
    5     1
    6    36
    7     9
    8    81
    9    16
    dtype: int64



* 数据替换repalce


```python
# 替换单个值
ser_obj.replace(0, -100)
```




    0      7
    1      9
    2      1
    3   -100
    4      8
    5      1
    6      6
    7      3
    8      9
    9      4
    dtype: int32




```python
# 替换多个值
ser_obj.replace([0, 2], -100)
```




    0      7
    1      9
    2      1
    3   -100
    4      8
    5      1
    6      6
    7      3
    8      9
    9      4
    dtype: int32




```python
# 替换多个值
ser_obj.replace([0, 2], [-100, -200])
```




    0      7
    1      9
    2      1
    3   -100
    4      8
    5      1
    6      6
    7      3
    8      9
    9      4
    dtype: int64




```python

```
