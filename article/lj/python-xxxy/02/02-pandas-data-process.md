
# Pandas数据操作


```python
import pandas as pd
```

* Series索引


```python
ser_obj = pd.Series(range(5), index = ['a', 'b', 'c', 'd', 'e'])
print(ser_obj.head())
```

    a    0
    b    1
    c    2
    d    3
    e    4
    dtype: int32
    


```python
# 行索引
print(ser_obj['a'])
print(ser_obj[0])
```

    0
    0
    


```python
# 切片索引
print(ser_obj[1:3])
print(ser_obj['b':'d'])
```

    b    1
    c    2
    dtype: int32
    b    1
    c    2
    d    3
    dtype: int32
    


```python
# 不连续索引
print(ser_obj[[0, 2, 4]])
print(ser_obj[['a', 'e']])
```

    a    0
    c    2
    e    4
    dtype: int32
    a    0
    e    4
    dtype: int32
    


```python
# 布尔索引
ser_bool = ser_obj > 2
print(ser_bool)
print(ser_obj[ser_bool])

print(ser_obj[ser_obj > 2])
```

    a    False
    b    False
    c    False
    d     True
    e     True
    dtype: bool
    d    3
    e    4
    dtype: int32
    d    3
    e    4
    dtype: int32
    

* DataFrame索引


```python
import numpy as np

df_obj = pd.DataFrame(np.random.randn(5,4), columns = ['a', 'b', 'c', 'd'])
print(df_obj.head())
```

              a         b         c         d
    0  1.487338 -0.131267  0.798305  0.456526
    1  0.845968  0.582888 -0.940616 -2.007079
    2  0.136282 -0.899088  0.705549 -1.411679
    3 -0.416619 -0.379917  0.518185 -0.999199
    4  0.945567 -0.548615 -0.265608 -1.448001
    


```python
# 列索引
print('列索引')
print(df_obj['a']) # 返回Series类型
#print(type(df_obj[[0]])) # 返回DataFrame类型

# 不连续索引
print('不连续索引')
print(df_obj[['a','c']])
#print(df_obj[[1, 3]])
```

    列索引
    0    1.487338
    1    0.845968
    2    0.136282
    3   -0.416619
    4    0.945567
    Name: a, dtype: float64
    不连续索引
              a         c
    0  1.487338  0.798305
    1  0.845968 -0.940616
    2  0.136282  0.705549
    3 -0.416619  0.518185
    4  0.945567 -0.265608
    

* 三种索引方式


```python
print(ser_obj)
print(df_obj)
```

    a    0
    b    1
    c    2
    d    3
    e    4
    dtype: int32
              a         b         c         d
    0  1.487338 -0.131267  0.798305  0.456526
    1  0.845968  0.582888 -0.940616 -2.007079
    2  0.136282 -0.899088  0.705549 -1.411679
    3 -0.416619 -0.379917  0.518185 -0.999199
    4  0.945567 -0.548615 -0.265608 -1.448001
    


```python
# 标签索引 loc
# Series
print(ser_obj['b':'d'])
print(ser_obj.loc['b':'d'])

# DataFrame
print(df_obj['a'])
print(df_obj.loc[0:2, 'a'])
```

    b    1
    c    2
    d    3
    dtype: int32
    b    1
    c    2
    d    3
    dtype: int32
    0    1.487338
    1    0.845968
    2    0.136282
    3   -0.416619
    4    0.945567
    Name: a, dtype: float64
    0    1.487338
    1    0.845968
    2    0.136282
    Name: a, dtype: float64
    


```python
print(ser_obj)
```

    a    0
    b    1
    c    2
    d    3
    e    4
    dtype: int32
    


```python
# 整型位置索引 iloc
print(ser_obj['b':'d'])
print(ser_obj.iloc[1:3])

# DataFrame
print(df_obj.iloc[0:2, 0]) # 注意和df_obj.loc[0:2, 'a']的区别
print(df_obj.loc[0:2, 'a'])
```

    b    1
    c    2
    d    3
    dtype: int32
    b    1
    c    2
    dtype: int32
    0    1.487338
    1    0.845968
    Name: a, dtype: float64
    0    1.487338
    1    0.845968
    2    0.136282
    Name: a, dtype: float64
    


```python
print(ser_obj)
```

    a    0
    b    1
    c    2
    d    3
    e    4
    dtype: int32
    


```python
# 混合索引 ix
print(ser_obj.ix[1:3])
print(ser_obj.ix['b':'c'])

# DataFrame
print(df_obj.ix[0:2, 0]) # 先按标签索引尝试操作，然后再按位置索引尝试操作
```

    b    1
    c    2
    dtype: int32
    b    1
    c    2
    dtype: int32
    0    1.487338
    1    0.845968
    2    0.136282
    Name: a, dtype: float64
    

    d:\python34\lib\site-packages\ipykernel\__main__.py:2: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate_ix
      from ipykernel import kernelapp as app
    d:\python34\lib\site-packages\ipykernel\__main__.py:6: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate_ix
    

* 运算与对齐


```python
s1 = pd.Series(range(10, 20), index = range(10))
s2 = pd.Series(range(20, 25), index = range(5))

print('s1: ' )
print(s1)

print('') 

print('s2: ')
print(s2)
```

    s1: 
    0    10
    1    11
    2    12
    3    13
    4    14
    5    15
    6    16
    7    17
    8    18
    9    19
    dtype: int32
    
    s2: 
    0    20
    1    21
    2    22
    3    23
    4    24
    dtype: int32
    


```python
# Series 对齐运算
s1 + s2
```




    0    30.0
    1    32.0
    2    34.0
    3    36.0
    4    38.0
    5     NaN
    6     NaN
    7     NaN
    8     NaN
    9     NaN
    dtype: float64




```python
import numpy as np

df1 = pd.DataFrame(np.ones((2,2)), columns = ['a', 'b'])
df2 = pd.DataFrame(np.ones((3,3)), columns = ['a', 'b', 'c'])

print('df1: ')
print(df1)

print('') 
print('df2: ')
print(df2)
```

    df1: 
         a    b
    0  1.0  1.0
    1  1.0  1.0
    
    df2: 
         a    b    c
    0  1.0  1.0  1.0
    1  1.0  1.0  1.0
    2  1.0  1.0  1.0
    


```python
# DataFrame对齐操作
df1 + df2
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>2.0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 填充未对齐的数据进行运算
print(s1)
print(s2)

s1.add(s2, fill_value = -1)
```

    0    10
    1    11
    2    12
    3    13
    4    14
    5    15
    6    16
    7    17
    8    18
    9    19
    dtype: int32
    0    20
    1    21
    2    22
    3    23
    4    24
    dtype: int32
    




    0    30.0
    1    32.0
    2    34.0
    3    36.0
    4    38.0
    5    14.0
    6    15.0
    7    16.0
    8    17.0
    9    18.0
    dtype: float64




```python
df1.sub(df2, fill_value = 2.)
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
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.0</td>
      <td>1.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 填充NaN
s3 = s1 + s2
print(s3)
```

    0    30.0
    1    32.0
    2    34.0
    3    36.0
    4    38.0
    5     NaN
    6     NaN
    7     NaN
    8     NaN
    9     NaN
    dtype: float64
    


```python
s3_filled = s3.fillna(-1)
print(s3_filled)
```

    0    30.0
    1    32.0
    2    34.0
    3    36.0
    4    38.0
    5    -1.0
    6    -1.0
    7    -1.0
    8    -1.0
    9    -1.0
    dtype: float64
    


```python
df3 = df1 + df2
print(df3)
```

         a    b   c
    0  2.0  2.0 NaN
    1  2.0  2.0 NaN
    2  NaN  NaN NaN
    


```python
df3.fillna(100, inplace = True)
print(df3)
```

           a      b      c
    0    2.0    2.0  100.0
    1    2.0    2.0  100.0
    2  100.0  100.0  100.0
    

* 函数应用


```python
# Numpy ufunc 函数
df = pd.DataFrame(np.random.randn(5,4) - 1)
print(df)

print(np.abs(df))
```

              0         1         2         3
    0 -1.278841 -0.441358 -0.918558  1.086543
    1  0.355898 -0.841866 -2.527455  0.355916
    2 -1.455938 -0.485170 -0.427544 -1.265602
    3 -0.509453 -1.181119 -1.544357 -3.855732
    4 -1.197029  0.076550 -1.092266 -0.578271
              0         1         2         3
    0  1.278841  0.441358  0.918558  1.086543
    1  0.355898  0.841866  2.527455  0.355916
    2  1.455938  0.485170  0.427544  1.265602
    3  0.509453  1.181119  1.544357  3.855732
    4  1.197029  0.076550  1.092266  0.578271
    


```python
# 使用apply应用行或列数据
#f = lambda x : x.max()
def f(x):
    return x.max()

print(df.apply(f))
```

    0    0.355898
    1    0.076550
    2   -0.427544
    3    1.086543
    dtype: float64
    


```python
# 指定轴方向
print(df.apply(lambda x : x.max(), axis=1))
```

    0    1.086543
    1    0.355916
    2   -0.427544
    3   -0.509453
    4    0.076550
    dtype: float64
    


```python
# 使用applymap应用到每个数据
f2 = lambda x : '%.2f' % x
print(df.applymap(f2))
```

           0      1      2      3
    0  -1.28  -0.44  -0.92   1.09
    1   0.36  -0.84  -2.53   0.36
    2  -1.46  -0.49  -0.43  -1.27
    3  -0.51  -1.18  -1.54  -3.86
    4  -1.20   0.08  -1.09  -0.58
    

* 排序


```python
s4 = pd.Series(range(10, 15), index = np.random.randint(5, size=5))
print(s4)
```

    3    10
    0    11
    0    12
    3    13
    1    14
    dtype: int32
    


```python
# 索引排序
s4.sort_index(ascending=False)
```




    3    10
    3    13
    1    14
    0    11
    0    12
    dtype: int32




```python
df4 = pd.DataFrame(np.random.randn(3, 4), 
                   index=np.random.randint(3, size=3),
                   columns=np.random.randint(4, size=4))
print(df4)
```

              0         3         1         3
    1 -1.074869  0.256095  0.136766 -0.606702
    2 -1.115481  0.739818  1.292220  0.711678
    0  0.245830 -0.144434 -1.078077  0.406480
    


```python
#df4.sort_index(ascending=False)
df4.sort_index(axis=1)
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
      <th>3</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>-1.074869</td>
      <td>0.136766</td>
      <td>0.256095</td>
      <td>-0.606702</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.115481</td>
      <td>1.292220</td>
      <td>0.739818</td>
      <td>0.711678</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0.245830</td>
      <td>-1.078077</td>
      <td>-0.144434</td>
      <td>0.406480</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 按值排序
df4.sort_values(by=0)
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
      <th>3</th>
      <th>1</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>-1.115481</td>
      <td>0.739818</td>
      <td>1.292220</td>
      <td>0.711678</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-1.074869</td>
      <td>0.256095</td>
      <td>0.136766</td>
      <td>-0.606702</td>
    </tr>
    <tr>
      <th>0</th>
      <td>0.245830</td>
      <td>-0.144434</td>
      <td>-1.078077</td>
      <td>0.406480</td>
    </tr>
  </tbody>
</table>
</div>



* 处理缺失数据


```python
df_data = pd.DataFrame([np.random.randn(3), [1., np.nan, np.nan],
                       [4., np.nan, np.nan], [1., np.nan, 2.]])
df_data.head()
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
      <td>-0.013522</td>
      <td>0.22717</td>
      <td>-0.202574</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.000000</td>
      <td>NaN</td>
      <td>2.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# isnull
df_data.isnull()
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
      <td>False</td>
      <td>False</td>
      <td>False</td>
    </tr>
    <tr>
      <th>1</th>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>2</th>
      <td>False</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <th>3</th>
      <td>False</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>




```python
# dropna
df_data.dropna()
#df_data.dropna(axis=1)
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
      <td>-0.013522</td>
      <td>0.22717</td>
      <td>-0.202574</td>
    </tr>
  </tbody>
</table>
</div>




```python
# fillna
df_data.fillna(-100.)
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
      <td>-0.013522</td>
      <td>0.22717</td>
      <td>-0.202574</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1.000000</td>
      <td>-100.00000</td>
      <td>-100.000000</td>
    </tr>
    <tr>
      <th>2</th>
      <td>4.000000</td>
      <td>-100.00000</td>
      <td>-100.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1.000000</td>
      <td>-100.00000</td>
      <td>2.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
