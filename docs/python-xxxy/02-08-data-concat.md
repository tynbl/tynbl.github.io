
# 数据合并 concat


```python
import numpy as np
import pandas as pd
```

* NumPy的concat


```python
arr1 = np.random.randint(0, 10, (3, 4))
arr2 = np.random.randint(0, 10, (3, 4))

print(arr1)
print(arr2)
```

    [[8 7 2 4]
     [5 6 5 6]
     [4 1 0 2]]
    [[0 3 1 6]
     [6 0 1 3]
     [0 6 8 2]]
    


```python
np.concatenate([arr1, arr2])
```




    array([[8, 7, 2, 4],
           [5, 6, 5, 6],
           [4, 1, 0, 2],
           [0, 3, 1, 6],
           [6, 0, 1, 3],
           [0, 6, 8, 2]])




```python
np.concatenate([arr1, arr2], axis=1)
```




    array([[8, 7, 2, 4, 0, 3, 1, 6],
           [5, 6, 5, 6, 6, 0, 1, 3],
           [4, 1, 0, 2, 0, 6, 8, 2]])



* Series上的concat


```python
# index 没有重复的情况
ser_obj1 = pd.Series(np.random.randint(0, 10, 5), index=range(0,5))
ser_obj2 = pd.Series(np.random.randint(0, 10, 4), index=range(5,9))
ser_obj3 = pd.Series(np.random.randint(0, 10, 3), index=range(9,12))

print(ser_obj1)
print(ser_obj2)
print(ser_obj3)
```

    0    6
    1    2
    2    0
    3    1
    4    2
    dtype: int32
    5    5
    6    5
    7    8
    8    4
    dtype: int32
    9     1
    10    7
    11    2
    dtype: int32
    


```python
pd.concat([ser_obj1, ser_obj2, ser_obj3])
```




    0     6
    1     2
    2     0
    3     1
    4     2
    5     5
    6     5
    7     8
    8     4
    9     1
    10    7
    11    2
    dtype: int32




```python
pd.concat([ser_obj1, ser_obj2, ser_obj3], axis=1)
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>5.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>5.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>8.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>4.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>2.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# index 有重复的情况
ser_obj1 = pd.Series(np.random.randint(0, 10, 5), index=range(5))
ser_obj2 = pd.Series(np.random.randint(0, 10, 4), index=range(4))
ser_obj3 = pd.Series(np.random.randint(0, 10, 3), index=range(3))

print(ser_obj1)
print(ser_obj2)
print(ser_obj3)
```

    0    8
    1    8
    2    8
    3    0
    4    0
    dtype: int32
    0    3
    1    5
    2    5
    3    1
    dtype: int32
    0    6
    1    1
    2    6
    dtype: int32
    


```python
pd.concat([ser_obj1, ser_obj2, ser_obj3])
```




    0    8
    1    8
    2    8
    3    0
    4    0
    0    3
    1    5
    2    5
    3    1
    0    6
    1    1
    2    6
    dtype: int32




```python
pd.concat([ser_obj1, ser_obj2, ser_obj3], axis=1, join='inner')
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
      <th>0</th>
      <th>1</th>
      <th>2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>3</td>
      <td>6</td>
    </tr>
    <tr>
      <th>1</th>
      <td>8</td>
      <td>5</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>5</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
</div>



* DataFrame上的concat


```python
df_obj1 = pd.DataFrame(np.random.randint(0, 10, (3, 2)), index=['a', 'b', 'c'],
                       columns=['A', 'B'])
df_obj2 = pd.DataFrame(np.random.randint(0, 10, (2, 2)), index=['a', 'b'],
                       columns=['C', 'D'])
print(df_obj1)
print(df_obj2)
```

       A  B
    a  3  4
    b  7  9
    c  7  9
       C  D
    a  5  4
    b  3  6
    


```python
pd.concat([df_obj1, df_obj2])
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>3.0</td>
      <td>4.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>b</th>
      <td>7.0</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>c</th>
      <td>7.0</td>
      <td>9.0</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>a</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.0</td>
      <td>6.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.concat([df_obj1, df_obj2], axis=1)
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
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>D</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>a</th>
      <td>3</td>
      <td>4</td>
      <td>5.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>b</th>
      <td>7</td>
      <td>9</td>
      <td>3.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>c</th>
      <td>7</td>
      <td>9</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
