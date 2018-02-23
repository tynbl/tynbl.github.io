
# Python高阶函数

* 函数式编程

函数本身也可赋值给变量


```python
import math
math.sqrt(25)
```




    5.0




```python
math.sqrt
```




    <function math.sqrt>




```python
fun = math.sqrt
fun
```




    <function math.sqrt>




```python
fun(10)
```




    3.1622776601683795



将函数作为参数


```python
def func_add(x, y, f):
    """
        functional addition
    """
    return f(x) + f(y)

print func_add(4, 25, math.sqrt)
print func_add(-4, 25, abs)
```

    7.0
    29
    

# map/reduce

* map


```python
x_2 = [x**2 for x in range(10)]
print x_2

x_sqrt_lst = map(math.sqrt, x_2)
print x_sqrt_lst

x_2_float_lst = map(float, x_2)
print x_2_float_lst

x_2_str_lst = map(str, x_2)
print x_2_str_lst
```

    [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
    [0.0, 1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0]
    [0.0, 1.0, 4.0, 9.0, 16.0, 25.0, 36.0, 49.0, 64.0, 81.0]
    ['0', '1', '4', '9', '16', '25', '36', '49', '64', '81']
    

* reduce


```python
str_lst = map(str, range(5)) # ['0', '1', ...]
print str_lst

def make_num(str1, str2):
    return int(str1) * 10 + int(str2)

result = reduce(make_num, str_lst)
print result
```

    ['0', '1', '2', '3', '4']
    1234
    

规范字符串


```python
name_lst = ['poNNY MA', 'rObIN li', 'steve JOBS', 'bILL gates']
standard_name_lst = map(str.title, name_lst)
print standard_name_lst
```

    ['Ponny Ma', 'Robin Li', 'Steve Jobs', 'Bill Gates']
    

# filter


```python
number_lst = range(-10, 10)

def is_negative(x):
    return x < 0

filtered_lst = filter(is_negative, number_lst)
print number_lst
print filtered_lst
```

    [-10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [-10, -9, -8, -7, -6, -5, -4, -3, -2, -1]
    

# map reduce filter 与匿名函数

* map与匿名函数


```python
x_lst = range(10)
result_lst = map(lambda item : item**2 +item**3, x_lst)
print x_lst
print result_lst
```

    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [0, 2, 12, 36, 80, 150, 252, 392, 576, 810]
    

* reduce与匿名函数


```python
x_lst = range(1, 5)
product = reduce(lambda x, y : x*y, x_lst)
print x_lst
print product
```

    [1, 2, 3, 4]
    24
    

* filter与匿名函数


```python
number_lst = range(-10, 10)
filtered_lst = filter(lambda x : x<0, number_lst)
print number_lst
print filtered_lst
```

    [-10, -9, -8, -7, -6, -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
    [-10, -9, -8, -7, -6, -5, -4, -3, -2, -1]
    


```python

```
