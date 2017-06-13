
# Pandas数据结构


```python
import pandas as pd
```

* Series


```python
# 通过list构建Series
ser_obj = pd.Series(range(10, 20))
print(type(ser_obj))
```

    <class 'pandas.core.series.Series'>
    


```python
# 获取数据
print(type(ser_obj.values))

# 获取索引
print(type(ser_obj.index))
```

    <class 'numpy.ndarray'>
    <class 'pandas.core.indexes.range.RangeIndex'>
    


```python
# 预览数据
print(ser_obj.head(3))
```

    0    10
    1    11
    2    12
    dtype: int32
    


```python
print(ser_obj)
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
    


```python
#通过索引获取数据
print(ser_obj[0])
print(ser_obj[8])
```

    10
    18
    


```python
# 索引与数据的对应关系仍保持在数组运算的结果中
#print(ser_obj * 2)
print(ser_obj[ser_obj > 15])
```

    6    16
    7    17
    8    18
    9    19
    dtype: int32
    


```python
# 通过dict构建Series
year_data = {2001: 17.8, 2002: 20.1, 2003: 16.5}
ser_obj2 = pd.Series(year_data)
print(ser_obj2.head())
print(ser_obj2.index)
```

    2001    17.8
    2002    20.1
    2003    16.5
    dtype: float64
    Int64Index([2001, 2002, 2003], dtype='int64')
    


```python
# name属性
ser_obj2.name = 'temp'
ser_obj2.index.name = 'year'
print(ser_obj2.head())
```

    year
    2001    17.8
    2002    20.1
    2003    16.5
    Name: temp, dtype: float64
    

* DataFrame


```python
import numpy as np

# 通过ndarray构建DataFrame
array = np.random.randn(5,4)
print(array)

df_obj = pd.DataFrame(array)
print(df_obj.head())
```

    [[-2.13011428 -0.03070425  2.03737783  0.24664937]
     [-3.47379492 -1.07512646  1.2631355  -0.30402591]
     [ 0.30210788  0.30174435 -0.15914681  1.86588223]
     [-1.30747046 -0.06332927  1.7032972  -0.89971861]
     [ 0.31792549  0.53724585  0.23326721 -0.05687282]]
              0         1         2         3
    0 -2.130114 -0.030704  2.037378  0.246649
    1 -3.473795 -1.075126  1.263135 -0.304026
    2  0.302108  0.301744 -0.159147  1.865882
    3 -1.307470 -0.063329  1.703297 -0.899719
    4  0.317925  0.537246  0.233267 -0.056873
    


```python
# 通过dict构建DataFrame
dict_data = {'A': 1., 
             'B': pd.Timestamp('20161217'),
             'C': pd.Series(1, index=list(range(4)),dtype='float32'),
             'D': np.array([3] * 4,dtype='int32'),
             'E' : pd.Categorical(["Python","Java","C++","C#"]),
             'F' : 'ChinaHadoop' }
#print dict_data
df_obj2 = pd.DataFrame(dict_data)
print(df_obj2.head())
```

         A          B    C  D       E            F
    0  1.0 2016-12-17  1.0  3  Python  ChinaHadoop
    1  1.0 2016-12-17  1.0  3    Java  ChinaHadoop
    2  1.0 2016-12-17  1.0  3     C++  ChinaHadoop
    3  1.0 2016-12-17  1.0  3      C#  ChinaHadoop
    


```python
# 通过列索引获取列数据
print(df_obj2['A'])
print(type(df_obj2['A']))

print(df_obj2.A)
```

    0    1.0
    1    1.0
    2    1.0
    3    1.0
    Name: A, dtype: float64
    <class 'pandas.core.series.Series'>
    0    1.0
    1    1.0
    2    1.0
    3    1.0
    Name: A, dtype: float64
    


```python
# 增加列
df_obj2['G'] = df_obj2['D'] + 4
print(df_obj2.head())
```

         A          B    C  D       E            F  G
    0  1.0 2016-12-17  1.0  3  Python  ChinaHadoop  7
    1  1.0 2016-12-17  1.0  3    Java  ChinaHadoop  7
    2  1.0 2016-12-17  1.0  3     C++  ChinaHadoop  7
    3  1.0 2016-12-17  1.0  3      C#  ChinaHadoop  7
    


```python
# 删除列
del(df_obj2['G'] )
print(df_obj2.head())
```

         A          B    C  D       E            F
    0  1.0 2016-12-17  1.0  3  Python  ChinaHadoop
    1  1.0 2016-12-17  1.0  3    Java  ChinaHadoop
    2  1.0 2016-12-17  1.0  3     C++  ChinaHadoop
    3  1.0 2016-12-17  1.0  3      C#  ChinaHadoop
    

* 索引对象 Index


```python
print(type(ser_obj.index))
print(type(df_obj2.index))

print(df_obj2.index)
```

    <class 'pandas.core.indexes.range.RangeIndex'>
    <class 'pandas.core.indexes.numeric.Int64Index'>
    Int64Index([0, 1, 2, 3], dtype='int64')
    


```python
# 索引对象不可变
df_obj2.index[0] = 2
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-16-7f40a356d7d1> in <module>()
          1 # 索引对象不可变
    ----> 2 df_obj2.index[0] = 2
    

    d:\python34\lib\site-packages\pandas\core\indexes\base.py in __setitem__(self, key, value)
       1668 
       1669     def __setitem__(self, key, value):
    -> 1670         raise TypeError("Index does not support mutable operations")
       1671 
       1672     def __getitem__(self, key):
    

    TypeError: Index does not support mutable operations



```python

```
