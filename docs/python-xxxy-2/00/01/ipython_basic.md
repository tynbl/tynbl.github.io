
# ? 和 ??

* 变量+(?) 和 变量+(??)


```python
x = 5
```


```python
x?
```


```python
x??
```

* 函数+(?) 函数+(??)


```python
def print_info():
    """
        show information
    """
    print 'Hello ChinaHadoop'
```


```python
print_info?
```


```python
print_info??
```

# 魔术命令

* %timeit 和 %time，%%timeit，%%time用于多条语句


```python
%timeit [x for x in range(10)]
```

    1000000 loops, best of 3: 888 ns per loop
    


```python
%%time
l = []
for x in range(100000):
    l.append(x)
```

    Wall time: 33 ms
    


```python

```
