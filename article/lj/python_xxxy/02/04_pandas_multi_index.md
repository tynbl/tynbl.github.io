
# Pandas层级索引


```python
import pandas as pd
import numpy as np
```


```python
ser_obj = pd.Series(np.random.randn(12),
                    index=[['a', 'a', 'a', 'b', 'b', 'b', 'c', 'c', 'c', 'd', 'd', 'd'],
                           [0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2]])
print(ser_obj)
```

    a  0   -1.075449
       1   -0.412114
       2    1.203992
    b  0    2.653719
       1   -0.991895
       2    0.177218
    c  0    0.585722
       1   -0.132374
       2   -0.370093
    d  0    0.845672
       1   -2.273390
       2   -1.461719
    dtype: float64
    

* MultiIndex索引对象


```python
print(type(ser_obj.index))
print(ser_obj.index)
```

    <class 'pandas.core.indexes.multi.MultiIndex'>
    MultiIndex(levels=[['a', 'b', 'c', 'd'], [0, 1, 2]],
               labels=[[0, 0, 0, 1, 1, 1, 2, 2, 2, 3, 3, 3], [0, 1, 2, 0, 1, 2, 0, 1, 2, 0, 1, 2]])
    

* 选取子集


```python
# 外层选取
print(ser_obj['c'])
```

    0    0.585722
    1   -0.132374
    2   -0.370093
    dtype: float64
    


```python
# 内层选取
print(ser_obj[:, 2])
```

    a    1.203992
    b    0.177218
    c   -0.370093
    d   -1.461719
    dtype: float64
    

* 交换分层顺序


```python
print(ser_obj.swaplevel())
```

    0  a   -1.075449
    1  a   -0.412114
    2  a    1.203992
    0  b    2.653719
    1  b   -0.991895
    2  b    0.177218
    0  c    0.585722
    1  c   -0.132374
    2  c   -0.370093
    0  d    0.845672
    1  d   -2.273390
    2  d   -1.461719
    dtype: float64
    

* 交换并排序分层


```python
print(ser_obj.swaplevel().sortlevel())
```

    0  a   -1.075449
       b    2.653719
       c    0.585722
       d    0.845672
    1  a   -0.412114
       b   -0.991895
       c   -0.132374
       d   -2.273390
    2  a    1.203992
       b    0.177218
       c   -0.370093
       d   -1.461719
    dtype: float64
    

    d:\python34\lib\site-packages\ipykernel\__main__.py:1: FutureWarning: sortlevel is deprecated, use sort_index(level=...)
      if __name__ == '__main__':
    


```python

```
