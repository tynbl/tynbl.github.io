
# 备忘录


```python
g = lambda x:x+1
print(g(1))
print(g(2))
```

    2
    3
    


```python
foo = [2, 18, 9, 22, 17, 24, 8, 12, 27]
```


```python
print(list(filter(lambda x: x % 3 == 0, foo)))
```

    [18, 9, 24, 12, 27]
    


```python
print([x for x in foo if x % 3 == 0])  # 如果可以使用for...in...if来完成的，坚决不用lambda。
```

    [18, 9, 24, 12, 27]
    


```python
print(list(map(lambda x: x * 2 + 10, foo)))
```

    [14, 46, 28, 54, 44, 58, 26, 34, 64]
    


```python
print([x * 2 + 10 for x in foo])  # 如果可以使用for...in...if来完成的，坚决不用lambda。
```

    [14, 46, 28, 54, 44, 58, 26, 34, 64]
    


```python
from functools import reduce 
print(reduce(lambda x, y: x + y, foo))
```

    139
    

[Python NumPy 计算欧氏距离（Euclidean Distance）](http://blog.topspeedsnail.com/archives/954)


```python
import numpy as np

# 样本数据
coords1 = [1, 2, 3]
coords2 = [4, 5, 6]
np_c1 = np.array(coords1)
np_c2 = np.array(coords2)

# NumPy 内建函数
np.linalg.norm(np_c1 - np_c2)
```




    5.196152422706632




```python

```
