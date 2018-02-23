
# 集合推导式

* 列表推导式


```python
%%timeit
#普通方法
result1 = []
for i in range(10000):
    if i%2 == 0:
        result1.append(i)
```

    1000 loops, best of 3: 1.21 ms per loop
    


```python
%%timeit
#列表推导式方法
result2 = [i for i in range(10000) if i%2 == 0]
```

    1000 loops, best of 3: 866 µs per loop
    


```python
str_lst = ['Welcome', 'to', 'Python', 'Data', 'Analysis', 'Course']
result3 = [x.upper() for x in str_lst if len(x) > 4]
print result3
```

    ['WELCOME', 'PYTHON', 'ANALYSIS', 'COURSE']
    

* 字典推导式


```python
dict1 = {key : value for key, value in enumerate(reversed(range(10)))}
print dict1
```

    {0: 9, 1: 8, 2: 7, 3: 6, 4: 5, 5: 4, 6: 3, 7: 2, 8: 1, 9: 0}
    

* 集合推导式


```python
set1 = {i for i in range(10)}
print set1
```

    set([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
    

* 嵌套推导式


```python
lists = [range(10), range(10, 20)]
print lists
```

    [[0, 1, 2, 3, 4, 5, 6, 7, 8, 9], [10, 11, 12, 13, 14, 15, 16, 17, 18, 19]]
    


```python
evens = [item for lst in lists for item in lst if item % 2 == 0]
print evens
```

    [0, 2, 4, 6, 8, 10, 12, 14, 16, 18]
    

# 多函数模式


```python
# 处理字符串
str_lst = ['$1.123', ' $1123.454', '$899.12312']

def remove_space(str):
    """
        remove space
    """
    str_no_space = str.replace(' ', '')
    return str_no_space

def remove_dollar(str):
    """
        remove $
    """
    if '$' in str:
        return str.replace('$', '')
    else:
        return str

def clean_str_lst(str_lst, operations):
    """
        clean string list
    """
    result = []
    for item in str_lst:
        for op in operations:
            item = op(item)
        result.append(item)
    return result

clean_operations = [remove_space, remove_dollar]
result = clean_str_lst(str_lst, clean_operations)
print result
    
```

    ['1.123', '1123.454', '899.12312']
    

# 匿名函数 lambda


```python
f = lambda x:x**2
f(2)
```




    4




```python
str_lst = ['Welcome', 'to', 'Python', 'Data', 'Analysis', 'Course']
str_lst.sort(key=lambda x:len(x)) # sort by length
print str_lst

str_lst.sort(key=lambda x:x[-1]) # sort by the last letter
print str_lst
```

    ['to', 'Data', 'Python', 'Course', 'Welcome', 'Analysis']
    ['Data', 'Course', 'Welcome', 'Python', 'to', 'Analysis']
    

# 生成器 generator


```python
def gen_test():
    for i in range(3):
        yield i
        
gen = gen_test() #此时不执行生成器
type(gen)
```




    generator




```python
for i in gen: # 直到迭代时才执行
    print i
```

    0
    1
    2
    


```python

```
