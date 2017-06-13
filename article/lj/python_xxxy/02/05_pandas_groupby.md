
# 分组与聚合

* GroupBy对象


```python
import pandas as pd
import numpy as np
```


```python
dict_obj = {'key1' : ['a', 'b', 'a', 'b', 
                      'a', 'b', 'a', 'a'],
            'key2' : ['one', 'one', 'two', 'three',
                      'two', 'two', 'one', 'three'],
            'data1': np.random.randn(8),
            'data2': np.random.randn(8)}
df_obj = pd.DataFrame(dict_obj)
print(df_obj)
```

          data1     data2 key1   key2
    0 -0.347611  0.118124    a    one
    1  0.527685 -1.486726    b    one
    2 -0.327329 -1.139239    a    two
    3  2.395181 -0.059415    b  three
    4  0.562707  0.471207    a    two
    5 -0.943481 -1.084524    b    two
    6 -1.101018  0.796216    a    one
    7 -1.002807 -0.485829    a  three
    


```python
# dataframe根据key1进行分组
print(type(df_obj.groupby('key1')))
print(df_obj.groupby('key1'))
```

    <class 'pandas.core.groupby.DataFrameGroupBy'>
    <pandas.core.groupby.DataFrameGroupBy object at 0x0731E0F0>
    


```python
# data1列根据key1进行分组
print(type(df_obj['data1'].groupby(df_obj['key1'])))
```

    <class 'pandas.core.groupby.SeriesGroupBy'>
    


```python
# 分组运算
grouped1 = df_obj.groupby('key1')
print(grouped1.mean())

grouped2 = df_obj['data1'].groupby(df_obj['key1'])
print(grouped2.mean())
```

             data1     data2
    key1                    
    a    -0.443212 -0.047904
    b     0.659795 -0.876888
    key1
    a   -0.443212
    b    0.659795
    Name: data1, dtype: float64
    


```python
# size
print(grouped1.size())
print(grouped2.size())
```

    key1
    a    5
    b    3
    dtype: int64
    key1
    a    5
    b    3
    Name: data1, dtype: int64
    


```python
# 按列名分组
df_obj.groupby('key1')
```




    <pandas.core.groupby.DataFrameGroupBy object at 0x0731E170>




```python
# 按自定义key分组，列表
self_def_key = [1, 1, 2, 2, 2, 1, 1, 1]
df_obj.groupby(self_def_key).size()
```




    1    5
    2    3
    dtype: int64




```python
# 按自定义key分组，多层列表
df_obj.groupby([df_obj['key1'], df_obj['key2']]).size()
```




    key1  key2 
    a     one      2
          three    1
          two      2
    b     one      1
          three    1
          two      1
    dtype: int64




```python
# 按多个列多层分组
grouped2 = df_obj.groupby(['key1', 'key2'])
print(grouped2.size())
```

    key1  key2 
    a     one      2
          three    1
          two      2
    b     one      1
          three    1
          two      1
    dtype: int64
    


```python
# 多层分组按key的顺序进行
grouped3 = df_obj.groupby(['key2', 'key1'])
print(grouped3.mean())
print()
print(grouped3.mean().unstack())
```

                   data1     data2
    key2  key1                    
    one   a    -0.724315  0.457170
          b     0.527685 -1.486726
    three a    -1.002807 -0.485829
          b     2.395181 -0.059415
    two   a     0.117689 -0.334016
          b    -0.943481 -1.084524
    
              data1               data2          
    key1          a         b         a         b
    key2                                         
    one   -0.724315  0.527685  0.457170 -1.486726
    three -1.002807  2.395181 -0.485829 -0.059415
    two    0.117689 -0.943481 -0.334016 -1.084524
    

* GroupBy对象分组迭代


```python
# 单层分组
for group_name, group_data in grouped1:
    print(group_name)
    print(group_data)
```

    a
          data1     data2 key1   key2
    0 -0.347611  0.118124    a    one
    2 -0.327329 -1.139239    a    two
    4  0.562707  0.471207    a    two
    6 -1.101018  0.796216    a    one
    7 -1.002807 -0.485829    a  three
    b
          data1     data2 key1   key2
    1  0.527685 -1.486726    b    one
    3  2.395181 -0.059415    b  three
    5 -0.943481 -1.084524    b    two
    


```python
# 多层分组
for group_name, group_data in grouped2:
    print(group_name)
    print(group_data)
```

    ('a', 'one')
          data1     data2 key1 key2
    0 -0.347611  0.118124    a  one
    6 -1.101018  0.796216    a  one
    ('a', 'three')
          data1     data2 key1   key2
    7 -1.002807 -0.485829    a  three
    ('a', 'two')
          data1     data2 key1 key2
    2 -0.327329 -1.139239    a  two
    4  0.562707  0.471207    a  two
    ('b', 'one')
          data1     data2 key1 key2
    1  0.527685 -1.486726    b  one
    ('b', 'three')
          data1     data2 key1   key2
    3  2.395181 -0.059415    b  three
    ('b', 'two')
          data1     data2 key1 key2
    5 -0.943481 -1.084524    b  two
    


```python
# GroupBy对象转换list
list(grouped1)
```




    [('a',       data1     data2 key1   key2
      0 -0.347611  0.118124    a    one
      2 -0.327329 -1.139239    a    two
      4  0.562707  0.471207    a    two
      6 -1.101018  0.796216    a    one
      7 -1.002807 -0.485829    a  three), ('b',       data1     data2 key1   key2
      1  0.527685 -1.486726    b    one
      3  2.395181 -0.059415    b  three
      5 -0.943481 -1.084524    b    two)]




```python
# GroupBy对象转换dict
dict(list(grouped1))
```




    {'a':       data1     data2 key1   key2
     0 -0.347611  0.118124    a    one
     2 -0.327329 -1.139239    a    two
     4  0.562707  0.471207    a    two
     6 -1.101018  0.796216    a    one
     7 -1.002807 -0.485829    a  three, 'b':       data1     data2 key1   key2
     1  0.527685 -1.486726    b    one
     3  2.395181 -0.059415    b  three
     5 -0.943481 -1.084524    b    two}




```python
# 按列分组
print(df_obj.dtypes)

# 按数据类型分组
df_obj.groupby(df_obj.dtypes, axis=1).size()
df_obj.groupby(df_obj.dtypes, axis=1).sum()
```

    data1    float64
    data2    float64
    key1      object
    key2      object
    dtype: object
    




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
      <th>float64</th>
      <th>object</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>-0.229487</td>
      <td>aone</td>
    </tr>
    <tr>
      <th>1</th>
      <td>-0.959040</td>
      <td>bone</td>
    </tr>
    <tr>
      <th>2</th>
      <td>-1.466568</td>
      <td>atwo</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.335765</td>
      <td>bthree</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1.033914</td>
      <td>atwo</td>
    </tr>
    <tr>
      <th>5</th>
      <td>-2.028005</td>
      <td>btwo</td>
    </tr>
    <tr>
      <th>6</th>
      <td>-0.304802</td>
      <td>aone</td>
    </tr>
    <tr>
      <th>7</th>
      <td>-1.488635</td>
      <td>athree</td>
    </tr>
  </tbody>
</table>
</div>



* 其他分组方法


```python
df_obj2 = pd.DataFrame(np.random.randint(1, 10, (5,5)),
                       columns=['a', 'b', 'c', 'd', 'e'],
                       index=['A', 'B', 'C', 'D', 'E'])
df_obj2.ix[1, 1:4] = np.NaN
df_obj2
```

    d:\python34\lib\site-packages\ipykernel\__main__.py:4: DeprecationWarning: 
    .ix is deprecated. Please use
    .loc for label based indexing or
    .iloc for positional indexing
    
    See the documentation here:
    http://pandas.pydata.org/pandas-docs/stable/indexing.html#deprecate_ix
    




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
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>6</td>
      <td>7.0</td>
      <td>3.0</td>
      <td>7.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>B</th>
      <td>3</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>7</td>
    </tr>
    <tr>
      <th>C</th>
      <td>5</td>
      <td>1.0</td>
      <td>8.0</td>
      <td>4.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>D</th>
      <td>6</td>
      <td>8.0</td>
      <td>9.0</td>
      <td>1.0</td>
      <td>7</td>
    </tr>
    <tr>
      <th>E</th>
      <td>9</td>
      <td>9.0</td>
      <td>4.0</td>
      <td>9.0</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过字典分组
mapping_dict = {'a':'python', 'b':'python', 'c':'java', 'd':'C', 'e':'java'}
df_obj2.groupby(mapping_dict, axis=1).size()
df_obj2.groupby(mapping_dict, axis=1).count() # 非NaN的个数
df_obj2.groupby(mapping_dict, axis=1).sum()
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
      <th>C</th>
      <th>java</th>
      <th>python</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>A</th>
      <td>7.0</td>
      <td>10.0</td>
      <td>13.0</td>
    </tr>
    <tr>
      <th>B</th>
      <td>NaN</td>
      <td>7.0</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>C</th>
      <td>4.0</td>
      <td>15.0</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>D</th>
      <td>1.0</td>
      <td>16.0</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>E</th>
      <td>9.0</td>
      <td>12.0</td>
      <td>18.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 通过函数分组
df_obj3 = pd.DataFrame(np.random.randint(1, 10, (5,5)),
                       columns=['a', 'b', 'c', 'd', 'e'],
                       index=['AA', 'BBB', 'CC', 'D', 'EE'])
df_obj3
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
      <th>e</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>AA</th>
      <td>1</td>
      <td>5</td>
      <td>4</td>
      <td>3</td>
      <td>9</td>
    </tr>
    <tr>
      <th>BBB</th>
      <td>3</td>
      <td>6</td>
      <td>7</td>
      <td>4</td>
      <td>4</td>
    </tr>
    <tr>
      <th>CC</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>7</td>
      <td>4</td>
    </tr>
    <tr>
      <th>D</th>
      <td>4</td>
      <td>3</td>
      <td>3</td>
      <td>9</td>
      <td>6</td>
    </tr>
    <tr>
      <th>EE</th>
      <td>1</td>
      <td>8</td>
      <td>9</td>
      <td>1</td>
      <td>4</td>
    </tr>
  </tbody>
</table>
</div>




```python
def group_key(idx):
    """
        idx 为列索引或行索引
    """
    #return idx
    return len(idx)

df_obj3.groupby(group_key).size()

# 以上自定义函数等价于
#df_obj3.groupby(len).size()
```




    1    1
    2    3
    3    1
    dtype: int64




```python
# 通过索引级别分组
columns = pd.MultiIndex.from_arrays([['Python', 'Java', 'Python', 'Java', 'Python'],
                                     ['A', 'A', 'B', 'C', 'B']], names=['language', 'index'])
df_obj4 = pd.DataFrame(np.random.randint(1, 10, (5, 5)), columns=columns)
df_obj4
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
    <tr>
      <th>language</th>
      <th>Python</th>
      <th>Java</th>
      <th>Python</th>
      <th>Java</th>
      <th>Python</th>
    </tr>
    <tr>
      <th>index</th>
      <th>A</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
      <th>B</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3</td>
      <td>5</td>
      <td>6</td>
      <td>3</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>4</td>
      <td>6</td>
      <td>8</td>
      <td>1</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>1</td>
      <td>9</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>9</td>
      <td>8</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>6</td>
      <td>8</td>
      <td>9</td>
      <td>9</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 根据language进行分组
df_obj4.groupby(level='language', axis=1).sum()
df_obj4.groupby(level='index', axis=1).sum()
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
      <th>index</th>
      <th>A</th>
      <th>B</th>
      <th>C</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>8</td>
      <td>11</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10</td>
      <td>10</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>15</td>
      <td>6</td>
    </tr>
    <tr>
      <th>3</th>
      <td>13</td>
      <td>15</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>14</td>
      <td>17</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
</div>



* 聚合


```python
dict_obj = {'key1' : ['a', 'b', 'a', 'b', 
                      'a', 'b', 'a', 'a'],
            'key2' : ['one', 'one', 'two', 'three',
                      'two', 'two', 'one', 'three'],
            'data1': np.random.randint(1,10, 8),
            'data2': np.random.randint(1,10, 8)}
df_obj5 = pd.DataFrame(dict_obj)
print(df_obj5)
```

       data1  data2 key1   key2
    0      8      3    a    one
    1      7      3    b    one
    2      4      8    a    two
    3      9      8    b  three
    4      4      8    a    two
    5      4      7    b    two
    6      1      5    a    one
    7      8      5    a  three
    


```python
# 内置的聚合函数
print(df_obj5.groupby('key1').sum())
print(df_obj5.groupby('key1').max())
print(df_obj5.groupby('key1').min())
print(df_obj5.groupby('key1').mean())
print(df_obj5.groupby('key1').size())
print(df_obj5.groupby('key1').count())
print(df_obj5.groupby('key1').describe())
```

          data1  data2
    key1              
    a        25     29
    b        20     18
          data1  data2 key2
    key1                   
    a         8      8  two
    b         9      8  two
          data1  data2 key2
    key1                   
    a         1      3  one
    b         4      3  one
             data1  data2
    key1                 
    a     5.000000    5.8
    b     6.666667    6.0
    key1
    a    5
    b    3
    dtype: int64
          data1  data2  key2
    key1                    
    a         5      5     5
    b         3      3     3
         data1                                              data2                 \
         count      mean       std  min  25%  50%  75%  max count mean       std   
    key1                                                                           
    a      5.0  5.000000  3.000000  1.0  4.0  4.0  8.0  8.0   5.0  5.8  2.167948   
    b      3.0  6.666667  2.516611  4.0  5.5  7.0  8.0  9.0   3.0  6.0  2.645751   
    
                                   
          min  25%  50%  75%  max  
    key1                           
    a     3.0  5.0  5.0  8.0  8.0  
    b     3.0  5.0  7.0  7.5  8.0  
    


```python
# 自定义聚合函数
def peak_range(df):
    """
        返回数值范围
    """
    #print type(df) #参数为索引所对应的记录
    return df.max() - df.min()

print(df_obj5.groupby('key1').agg(peak_range))
#print(df_obj.groupby('key1').agg(lambda df : df.max() - df.min()))
```

          data1  data2
    key1              
    a         7      5
    b         5      5
    


```python
# 应用多个聚合函数

# 同时应用多个聚合函数
print(df_obj.groupby('key1').agg(['mean', 'std', 'count', peak_range])) # 默认列名为函数名
```

             data1                                data2                           
              mean       std count peak_range      mean       std count peak_range
    key1                                                                          
    a    -0.443212  0.667139     5   1.663725 -0.047904  0.773364     5   1.935455
    b     0.659795  1.673247     3   3.338662 -0.876888  0.735961     3   1.427310
    


```python
print(df_obj.groupby('key1').agg(['mean', 'std', 'count', ('range', peak_range)])) # 通过元组提供新的列名
```

             data1                               data2                          
              mean       std count     range      mean       std count     range
    key1                                                                        
    a    -0.443212  0.667139     5  1.663725 -0.047904  0.773364     5  1.935455
    b     0.659795  1.673247     3  3.338662 -0.876888  0.735961     3  1.427310
    


```python
# 每列作用不同的聚合函数
dict_mapping = {'data1':'mean',
                'data2':'sum'}
print(df_obj.groupby('key1').agg(dict_mapping))
```

             data1     data2
    key1                    
    a    -0.443212 -0.239520
    b     0.659795 -2.630665
    


```python
dict_mapping = {'data1':['mean','max'],
                'data2':'sum'}
print(df_obj.groupby('key1').agg(dict_mapping))
```

             data1               data2
              mean       max       sum
    key1                              
    a    -0.443212  0.562707 -0.239520
    b     0.659795  2.395181 -2.630665
    


```python

```
