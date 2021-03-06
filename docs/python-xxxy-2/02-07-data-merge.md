
# 数据连接 merge


```python
import pandas as pd
import numpy as np
```


```python
df_obj1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                        'data1' : np.random.randint(0,10,7)})
df_obj2 = pd.DataFrame({'key': ['a', 'b', 'd'],
                        'data2' : np.random.randint(0,10,3)})

print(df_obj1)
print(df_obj2)
```

       data1 key
    0      7   b
    1      9   b
    2      6   a
    3      9   c
    4      3   a
    5      2   a
    6      0   b
       data2 key
    0      0   a
    1      2   b
    2      5   d
    


```python
# 默认将重叠列的列名作为“外键”进行连接
pd.merge(df_obj1, df_obj2)
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
      <th>key</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>a</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# on显示指定“外键”
pd.merge(df_obj1, df_obj2, on='key')
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
      <th>key</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>a</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# left_on，right_on分别指定左侧数据和右侧数据的“外键”

# 更改列名
df_obj1 = df_obj1.rename(columns={'key':'key1'})
df_obj2 = df_obj2.rename(columns={'key':'key2'})
```


```python
pd.merge(df_obj1, df_obj2, left_on='key1', right_on='key2')
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
      <th>key1</th>
      <th>data2</th>
      <th>key2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>b</td>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>b</td>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>b</td>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6</td>
      <td>a</td>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>a</td>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>a</td>
      <td>0</td>
      <td>a</td>
    </tr>
  </tbody>
</table>
</div>




```python
# “外连接”
pd.merge(df_obj1, df_obj2, left_on='key1', right_on='key2', how='outer')
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
      <th>key1</th>
      <th>data2</th>
      <th>key2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.0</td>
      <td>b</td>
      <td>2.0</td>
      <td>b</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.0</td>
      <td>b</td>
      <td>2.0</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>b</td>
      <td>2.0</td>
      <td>b</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6.0</td>
      <td>a</td>
      <td>0.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.0</td>
      <td>a</td>
      <td>0.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2.0</td>
      <td>a</td>
      <td>0.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>6</th>
      <td>9.0</td>
      <td>c</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>5.0</td>
      <td>d</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 左连接
pd.merge(df_obj1, df_obj2, left_on='key1', right_on='key2', how='left')
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
      <th>key1</th>
      <th>data2</th>
      <th>key2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7</td>
      <td>b</td>
      <td>2.0</td>
      <td>b</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9</td>
      <td>b</td>
      <td>2.0</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>6</td>
      <td>a</td>
      <td>0.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>3</th>
      <td>9</td>
      <td>c</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3</td>
      <td>a</td>
      <td>0.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2</td>
      <td>a</td>
      <td>0.0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>6</th>
      <td>0</td>
      <td>b</td>
      <td>2.0</td>
      <td>b</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 右连接
pd.merge(df_obj1, df_obj2, left_on='key1', right_on='key2', how='right')
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
      <th>key1</th>
      <th>data2</th>
      <th>key2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>7.0</td>
      <td>b</td>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>1</th>
      <td>9.0</td>
      <td>b</td>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>b</td>
      <td>2</td>
      <td>b</td>
    </tr>
    <tr>
      <th>3</th>
      <td>6.0</td>
      <td>a</td>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>4</th>
      <td>3.0</td>
      <td>a</td>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2.0</td>
      <td>a</td>
      <td>0</td>
      <td>a</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>5</td>
      <td>d</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 处理重复列名
df_obj1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                        'data' : np.random.randint(0,10,7)})
df_obj2 = pd.DataFrame({'key': ['a', 'b', 'd'],
                        'data' : np.random.randint(0,10,3)})

pd.merge(df_obj1, df_obj2, on='key', suffixes=('_left', '_right'))
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
      <th>data_left</th>
      <th>key</th>
      <th>data_right</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>6</td>
      <td>b</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>7</td>
      <td>b</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>8</td>
      <td>b</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>a</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0</td>
      <td>a</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 按索引连接
df_obj1 = pd.DataFrame({'key': ['b', 'b', 'a', 'c', 'a', 'a', 'b'],
                        'data1' : np.random.randint(0,10,7)})
df_obj2 = pd.DataFrame({'data2' : np.random.randint(0,10,3)}, index=['a', 'b', 'd'])
```


```python
pd.merge(df_obj1, df_obj2, left_on='key', right_index=True)
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
      <th>key</th>
      <th>data2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>b</td>
      <td>9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>b</td>
      <td>9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>b</td>
      <td>9</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>a</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>9</td>
      <td>a</td>
      <td>3</td>
    </tr>
    <tr>
      <th>5</th>
      <td>8</td>
      <td>a</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
