# Series 和 DataFrame 的基本操作

## 索引

### 索引对象

pandas 的索引对象可以管理轴标签和其它元数据（比如轴标签等）  
语法：  
```py
obj.index
```

- 索引对象可以进行切片  
  索引对象只有整数切片的方式，且是左开右闭的区间；不能进行标签切片  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  index = df.index
  print(index)
  print(index[1:4])

  # 输出
  Index(['one', 'two', 'three', 'four', 'five', 'six'], dtype='object')
  Index(['two', 'three', 'four'], dtype='object')
  ```

- 索引对象不可变  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  index = df.index
  index[0] = 'first'

  # 输出
  TypeError: Index does not support mutable operations
  ```

- 类似于一个固定大小的集合  
  集合的大部分属性和方法同样适用于索引对象  
  
  |方法|说明|
  |:-----|:----|
  |append|连接另一个 Index 对象，产生一个新的 Index|
  |difference|计算差集，并得到一个 Index|
  |intersection|计算交集|
  |union|计算并集|
  |delete|删除索引 i 处的元素，并得到新的 Index|
  |drop|删除传入的值，并得到新的 Index|
  |insert|将元素插入到索引 i 处，并得到新的 Index|
  |is_unique|当 Index 没有重复值时，返回True|
  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  index = df.index
  columns = df.columns
  print('one' in index)
  print('2003' in columns)
  
  # 输出
  True
  False
  ```
  
- 与集合最大的不同在于，索引对象可以包含重复的标签  
  选择重复的标签，会显示该标签的所有结果  
  ```py
  # 输入
  import pandas as pd

  dup_index = pd.Index(['one', 'one', 'three', 'four', 'five', 'six'])
  print(dup_index)
  
  # 输出
  Index(['one', 'one', 'three', 'four', 'five', 'six'], dtype='object')
  ```
  
### 重新索引
`reindex()`方法可以创建一个新的对象，它的数据符合新的索引，即根据新索引进行重排  

reindex 函数参数说明：  
|参数|说明|
|:----|:----|
|index|用作索引的新序列。既可以是 index 实例，也可以其他序列类型的 python 数据结构|
|method|插值填充方式|
|fill_value|在重新索引的过程中，需要引入缺失值时使用的替代值|
|limit|前向或后向填充时的最大填充量|
|tolerance|向前或向后填充时，填充不准确匹配项的最大间距（绝对值距离）|
|level|在 MultiIndex 的指定级别上匹配简单索引，否则选取其子集|
|copy|默认为 True，无论如何都复制；如果为 False，则新旧相等就不复制|

- Series 对象
  - `reindex()`会根据新索引重排。当某个索引值不存在时，引入缺失值  
    ```py
    # 输入
    import pandas as pd

    obj1 = pd.Series([4.5, 7.2, -5.3, 3.6], index=['a', 'b', 'c', 'd'])
    print(obj1)
    print('--------------------')
    obj2 = obj1.reindex(['a', 'b', 'c', 'd', 'e'])
    print(obj2)
    
    # 输出
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    dtype: float64
    --------------------
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    e    NaN
    dtype: float64
    ```
  
  - 重新索引的数据填充：如时间序列的有序数据（method 参数）及缺失值填充（fill_value 参数）  
    ```py
    # 输入
    import pandas as pd

    obj1 = pd.Series([4.5, 7.2, -5.3, 3.6], index=['a', 'b', 'c', 'd'])
    print(obj1)
    print('--------------------')
    # 缺失值填充
    obj2 = obj1.reindex(['a', 'b', 'c', 'd', 'e', 'f'], fill_value=6.6)
    print(obj2)
    print('--------------------')
    # 前向插值
    obj3 = obj1.reindex(['a', 'b', 'c', 'd', 'e', 'f'], method='ffill')
    print(obj3)

    # 输出
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    dtype: float64
    --------------------
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    e    6.6
    f    6.6
    dtype: float64
    --------------------
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    e    3.6
    f    3.6
    dtype: float64
    ```

- DataFrame 对象  
  - `reindex`重排索引和列：传递不带关键字的序列可以重排索引；传递带关键字`columns`的序列重排列  
    ```py
    # 输入
    import pandas as pd

    data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
            'year': [2000, 2001, 2003, 2004, 2005, 2006],
            'pop': [1.5, 1.7, 2.0, 2.4, 2.9, 3.2]}

    df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                      index=['one', 'two', 'three', 'four', 'five', 'six'])

    print('---------------重排索引--------------------')
    df1 = df.reindex(['one', 'two', 'three', 'five', 'six', 'seven'])
    print(df1)
    print('---------------重排列--------------------')
    df2 = df.reindex(columns=['year', 'pop', 'debt'])
    print(df2)
    print('-------------重排索引和列--------------------')
    df3 = df.reindex(['one', 'two', 'three', 'four', 'five', 'six', 'seven'],
                     columns=['year', 'state sta', 'pop', 'debt'])
    print(df3)

    # 输出
    ---------------重排索引--------------------
            year state sta  pop
    one    2000.0      Ohio  1.5
    two    2001.0      Ohio  1.7
    three  2003.0      Ohio  2.0
    five   2005.0    Nevada  2.9
    six    2006.0    Nevada  3.2
    seven     NaN       NaN  NaN
    ---------------重排列--------------------
          year  pop  debt
    one    2000  1.5   NaN
    two    2001  1.7   NaN
    three  2003  2.0   NaN
    four   2004  2.4   NaN
    five   2005  2.9   NaN
    six    2006  3.2   NaN
    -------------重排索引和列--------------------
            year state sta  pop  debt
    one    2000.0      Ohio  1.5   NaN
    two    2001.0      Ohio  1.7   NaN
    three  2003.0      Ohio  2.0   NaN
    four   2004.0    Nevada  2.4   NaN
    five   2005.0    Nevada  2.9   NaN
    six    2006.0    Nevada  3.2   NaN
    seven     NaN       NaN  NaN   NaN
    ```

  - 重新索引的数据填充：  

    缺失值填充: 使用`fill_value`参数  
    ```py
    # 输入
    import pandas as pd

    data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
            'year': [2000, 2001, 2003, 2004, 2005, 2006],
            'pop': [1.5, 1.7, 2.0, 2.4, 2.9, 3.2]}

    df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                      index=['one', 'two', 'three', 'four', 'five', 'six'])

    df = df.reindex(['one', 'two', 'three', 'four', 'five', 'six', 'seven'],
                    columns=['year', 'state sta', 'pop', 'debt'], fill_value=6)
    print(df)

    # 输出
           year state sta  pop  debt
    one    2000      Ohio  1.5     6
    two    2001      Ohio  1.7     6
    three  2003      Ohio  2.0     6
    four   2004    Nevada  2.4     6
    five   2005    Nevada  2.9     6
    six    2006    Nevada  3.2     6
    seven     6         6  6.0     6
    ```

    插值填充：插值填充不可以使用`method`参数，而应使用`ffill()`方法  
    **注意**：如果继续使用`method='ffill'`的方式，会报错：  
    ```py
    ValueError: index must be monotonic increasing or decreasing
    ```
    ```py
    # 输入
    import pandas as pd

    data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
            'year': [2000, 2001, 2003, 2004, 2005, 2006],
            'pop': [1.5, 1.7, 2.0, 2.4, 2.9, 3.2]}

    df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                      index=['one', 'two', 'three', 'four', 'five', 'six'])    
    
    df = df.reindex(['one', 'two', 'three', 'four', 'five', 'six', 'seven'],
                    columns=['year', 'state sta', 'pop', 'debt']).ffill()
    print(df)

    # 输出
             year state sta  pop  debt
    one    2000.0      Ohio  1.5   NaN
    two    2001.0      Ohio  1.7   NaN
    three  2003.0      Ohio  2.0   NaN
    four   2004.0    Nevada  2.4   NaN
    five   2005.0    Nevada  2.9   NaN
    six    2006.0    Nevada  3.2   NaN
    seven  2006.0    Nevada  3.2   NaN
    ```

### 丢弃指定轴上的项

`drop`方法可以删除指定轴上的项，返回一个在指定轴上删除了指定值的**新对象**
- 删除指定行/多行：`drop(index)` / `drop([index1, index2, ...])`  
- 删除指定列/多列：`drop(column, axis=1)`或`drop(column, axis='columns')` /  
  `drop([column1, column2, ...], axis=1)`或`drop([column1, column2, ...], axis='columns')`  
- `inplace=True`参数可以原地修改对象，不会返回新的对象，如：`obj.drop(index, inplace=True)`  

```py
# 输入
import pandas as pd

obj = pd.Series([4.5, 7.2, -5.3, 3.6, 6.6], index=['a', 'b', 'c', 'd', 'e'])
obj1 = obj.drop('e')
print(obj1)

data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2003, 2004, 2005, 2006],
        'pop': [1.5, 1.7, 2.0, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                  index=['one', 'two', 'three', 'four', 'five', 'six'])
print('------------------------------')
print(df)
print('------------------------------')
df1 = df.drop('six')
print(df1)
print('------------------------------')
df2 = df.drop('pop', axis=1)
print(df2)

# 输出
a    4.5
b    7.2
c   -5.3
d    3.6
dtype: float64
------------------------------
       year state sta  pop
one    2000      Ohio  1.5
two    2001      Ohio  1.7
three  2003      Ohio  2.0
four   2004    Nevada  2.4
five   2005    Nevada  2.9
six    2006    Nevada  3.2
------------------------------
       year state sta  pop
one    2000      Ohio  1.5
two    2001      Ohio  1.7
three  2003      Ohio  2.0
four   2004    Nevada  2.4
five   2005    Nevada  2.9
------------------------------
       year state sta
one    2000      Ohio
two    2001      Ohio
three  2003      Ohio
four   2004    Nevada
five   2005    Nevada
six    2006    Nevada
```