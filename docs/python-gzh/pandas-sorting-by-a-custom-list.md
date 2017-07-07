
 
#  [Pandas的DataFrame如何按指定list排序](http://mp.weixin.qq.com/s/rueYdM0SdcLc9aw39EpqBA) #

* 引入pandas库


```python
import pandas as pd
```

* 构造Series数据


```python
s = pd.Series({'a':1,'b':2,'c':3})
s
```




    a    1
    b    2
    c    3
    dtype: int64




```python
s.index
```




    Index(['a', 'b', 'c'], dtype='object')



* 指定的list，后续按指定list的元素顺序进行排序


```python
list_custom = ['b', 'a', 'c']
list_custom
```




    ['b', 'a', 'c']




```python
df = pd.DataFrame(s)
df = df.reset_index()
df.columns = ['words', 'number']
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>words</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



**设置成“category”数据类型**


```python
# 设置成“category”数据类型
df['words'] = df['words'].astype('category')
```


```python
# inplace = True，使 recorder_categories生效
df['words'].cat.reorder_categories(list_custom, inplace=True)

# inplace = True，使 df生效
df.sort_values('words', inplace=True)
df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>words</th>
      <th>number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>0</th>
      <td>a</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>



**指定list元素多的情况：**

若指定的list所包含元素比Dataframe中需要排序的列的元素**多**，怎么办？

* reorder_catgories（）方法不能继续使用，因为该方法使用时要求新的categories和dataframe中的categories的元素个数和内容必须一致，只是顺序不同。
* 这种情况下，可以使用 set_categories()方法来实现。新的list可以比dataframe中元素多。


```python
list_custom_new = ['d', 'c', 'b','a','e']
dict_new = {'e':1, 'b':2, 'c':3}
df_new = pd.DataFrame(list(dict_new.items()), columns=['words', 'value'])
print(list_custom_new)
df_new.sort_values('words', inplace=True)
df_new
```

    ['d', 'c', 'b', 'a', 'e']
    




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>words</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>3</td>
    </tr>
    <tr>
      <th>0</th>
      <td>e</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_new['words'] = df_new['words'].astype('category')

# inplace = True，使 set_categories生效
df_new['words'].cat.set_categories(list_custom_new, inplace=True)

df_new.sort_values('words', ascending=True)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>words</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>0</th>
      <td>e</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>



**指定list元素少的情况：**

若指定的list所包含元素比Dataframe中需要排序的列的元素**少**，怎么办？
* 这种情况下，set_categories()方法还是可以使用的，只是没有的元素会议NaN表示

注意下面的list中没有元素“b”


```python
list_custom_new = ['d', 'c','a','e']
dict_new = {'e':1, 'b':2, 'c':3}
df_new = pd.DataFrame(list(dict_new.items()), columns=['words', 'value'])
print(list_custom_new)
df_new.sort_values('words', inplace=True)
df_new
```

    ['d', 'c', 'a', 'e']
    




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>words</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>b</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>3</td>
    </tr>
    <tr>
      <th>0</th>
      <td>e</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_new['words'] = df_new['words'].astype('category')

# inplace = True，使 set_categories生效
df_new['words'].cat.set_categories(list_custom_new, inplace=True)

df_new.sort_values('words', ascending=True)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>words</th>
      <th>value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>c</td>
      <td>3</td>
    </tr>
    <tr>
      <th>0</th>
      <td>e</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
