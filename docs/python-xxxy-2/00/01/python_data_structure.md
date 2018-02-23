
# 元组

* 创建元组


```python
tup1 = 1, 2, 3
print tup1

# 嵌套元组
tup2 = (1, 2, 3), (4, 5)
print tup2
```

    (1, 2, 3)
    ((1, 2, 3), (4, 5))
    

* 转换为元组，list->tuple, string->tuple


```python
l = [1, 2, 3]
print tuple(l)

str = 'Hello ChinaHadoop'
print tuple(str)
```

    (1, 2, 3)
    ('H', 'e', 'l', 'l', 'o', ' ', 'C', 'h', 'i', 'n', 'a', 'H', 'a', 'd', 'o', 'o', 'p')
    

* 访问元组


```python
tup3 = tuple(str)
print tup3[4]
```

    o
    

* 合并元组


```python
tup1 + tup2
```




    (1, 2, 3, (1, 2, 3), (4, 5))



* 拆包


```python
a, b, c = tup1
print b
```

    2
    


```python
# 函数返回多个值
def return_multiple():
    t = (1, 2, 3)
    return t

a, _, c = return_multiple()
print c
```

    3
    


```python
# 元组列表迭代
tuple_lst = [(1, 2), (3, 4), (5, 6)]
for x, y in tuple_lst:
    print x+y
```

    3
    7
    11
    

* count 方法


```python
tup3.count('o')
```




    3



# 列表

* 创建列表


```python
lst_1 = [1, 2, 3, 'a', 'b', (4, 5)]
print lst_1

lst_2 = range(1, 9)
print lst_2
```

    [1, 2, 3, 'a', 'b', (4, 5)]
    [1, 2, 3, 4, 5, 6, 7, 8]
    

* 转换为列表, tuple->list


```python
lst_3 = list(tup3)
print lst_3
```

    ['H', 'e', 'l', 'l', 'o', ' ', 'C', 'h', 'i', 'n', 'a', 'H', 'a', 'd', 'o', 'o', 'p']
    

* 添加、移除元素


```python
lst_4 = range(10)

# 末尾添加
lst_4.append(11)
print lst_4

# 指定位置插入
lst_4.insert(5, 12)
print lst_4
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 11]
    [0, 1, 2, 3, 4, 12, 5, 6, 7, 8, 9, 11]
    


```python
# 删除指定位置的元素并返回
item = lst_4.pop(6)
print item
print lst_4
```

    5
    [0, 1, 2, 3, 4, 12, 6, 7, 8, 9, 11]
    


```python
# 删除指定的值，注意12在这里是“值”不是“位置”
lst_4.remove(12)
print lst_4
```

    [0, 1, 2, 3, 4, 6, 7, 8, 9, 11]
    

* 合并列表


```python
lst_3 = lst_1 + lst_2
print lst_3

lst_1.extend(lst_2)
print lst_1
```

    [1, 2, 3, 'a', 'b', (4, 5), 1, 2, 3, 4, 5, 6, 7, 8]
    [1, 2, 3, 'a', 'b', (4, 5), 1, 2, 3, 4, 5, 6, 7, 8]
    

* 排序操作


```python
import random
lst_5 = range(10)
random.shuffle(lst_5)
print lst_5
```

    [8, 1, 7, 3, 0, 5, 9, 6, 4, 2]
    


```python
lst_5.sort()
print lst_5
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    


```python
lst_6 = ['Welcome', 'to', 'Python', 'Data', 'Analysis', 'Course']
lst_6.sort()
print lst_6
```

    ['Analysis', 'Course', 'Data', 'Python', 'Welcome', 'to']
    


```python
lst_6.sort(key = len, reverse=True)
print lst_6
```

    ['Analysis', 'Welcome', 'Course', 'Python', 'Data', 'to']
    


```python
print lst_5
print lst_5[1:5]
print lst_5[5:]
print lst_5[:5]
print lst_5[-5:]
print lst_5[-5:-2]
print lst_5[::2]
print lst_5[::-1]
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [1, 2, 3, 4]
    [5, 6, 7, 8, 9]
    [0, 1, 2, 3, 4]
    [5, 6, 7, 8, 9]
    [5, 6, 7]
    [0, 2, 4, 6, 8]
    [9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
    

# 常用序列函数

* enumerate


```python
lst_6 = ['Welcome', 'to', 'Python', 'Data', 'Analysis', 'Course'] # (0, 'Welcome')
for i, item in enumerate(lst_6):
    print '%i-%s' %(i, item)
```

    0-Welcome
    1-to
    2-Python
    3-Data
    4-Analysis
    5-Course
    


```python
str_dict = dict((i, item) for i, item in enumerate(lst_6))
print str_dict
```

    {0: 'Welcome', 1: 'to', 2: 'Python', 3: 'Data', 4: 'Analysis', 5: 'Course'}
    

* sorted


```python
import random
lst_5 = range(10)
random.shuffle(lst_5)
print lst_5

#sorted
lst_5_sorted = sorted(lst_5)
print lst_5
print lst_5_sorted
```

    [3, 6, 5, 1, 0, 8, 9, 7, 4, 2]
    [3, 6, 5, 1, 0, 8, 9, 7, 4, 2]
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    

* zip 压缩


```python
lst_6 = ['Welcome', 'to', 'Python', 'Data', 'Analysis', 'Course']
lst_7 = range(5) #[0, 1, 2, 3, 4]
lst_8 = ['a', 'b', 'c']
zip_lst = zip(lst_6, lst_8, lst_7)
print zip_lst
```

    [('Welcome', 'a', 0), ('to', 'b', 1), ('Python', 'c', 2)]
    

* zip * 解压缩


```python
zip(*zip_lst)
```




    [('Welcome', 'to', 'Python'), ('a', 'b', 'c'), (0, 1, 2)]



* reversed


```python
list(reversed(lst_6))
```




    ['Course', 'Analysis', 'Data', 'Python', 'to', 'Welcome']



# 字典 dict

* 创建字典


```python
empty_dict = {}
dict1 = {'a': 1, 2: 'b', '3': [1, 2, 3]}
print empty_dict
print dict1
```

    {}
    {'a': 1, 2: 'b', '3': [1, 2, 3]}
    

* 插入元素


```python
dict1[4] = (4, 5)
print dict1
```

    {'a': 1, 2: 'b', 4: (4, 5), '3': [1, 2, 3]}
    

* 删除元素


```python
del dict1[2]
print dict1
```

    {'a': 1, 4: (4, 5), '3': [1, 2, 3]}
    


```python
a_value = dict1.pop('a')
print a_value
print dict1
```

    1
    {4: (4, 5), '3': [1, 2, 3]}
    

* 获取键、值列表


```python
print dict1.keys()
print dict1.values()
```

    [4, '3']
    [(4, 5), [1, 2, 3]]
    

* 合并字典


```python
dict2 = {4: 'new1', 5: 'news'}
dict1.update(dict2)
print dict1
```

    {'3': [1, 2, 3], 4: 'new1', 5: 'news'}
    

* 通过多个列表创建字典


```python
# 普通方法
dict_3 = {}
l1 = range(10)
l2 = list(reversed(range(10)))
for i1, i2 in zip(l1, l2):
    dict_3[i1] = i2
print dict_3
```

    {0: 9, 1: 8, 2: 7, 3: 6, 4: 5, 5: 4, 6: 3, 7: 2, 8: 1, 9: 0}
    


```python
dict_4 = dict(zip(l1, l2))
print dict_4
```

    {0: 9, 1: 8, 2: 7, 3: 6, 4: 5, 5: 4, 6: 3, 7: 2, 8: 1, 9: 0}
    

# hash函数


```python
hash(12)
```




    12




```python
hash('test hash')
```




    -520327859




```python
hash((1, 2, 3))
```




    -378539185




```python
hash([1, 2, 3])
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-38-0b995650570c> in <module>()
    ----> 1 hash([1, 2, 3])
    

    TypeError: unhashable type: 'list'


# 集合 set


```python
a = set(range(10))
print a
b = set(range(5,15))
print b
```

    set([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
    set([5, 6, 7, 8, 9, 10, 11, 12, 13, 14])
    

* 并 交 差 异或


```python
a | b
```




    {0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14}




```python
a & b
```




    {5, 6, 7, 8, 9}




```python
a - b
```




    {0, 1, 2, 3, 4}




```python
a ^ b
```




    {0, 1, 2, 3, 4, 10, 11, 12, 13, 14}



* 判断是否为子集、父集


```python
a.issubset(b)
```




    False




```python
a.issuperset(b)
```




    False




```python

```
