# DataFrame

约定导入`Pandas`和`Series、DataFrame`的写法：  
```py
import pandas as pd
```
调用：`pd.DataFrame()`  
```py
import pandas
from pandas import Series, DataFrame
```
调用：`DataFrame()`  

## 1、定义
DataFrame 是一个表格型的数据结构，它含有一组有序的列，每列可以是不同的值类型（数值、字符串、布尔型等）  
DataFrame 既有行索引也有列索引，它可以被看作由 Series 组成的字典（共用同一个行索引）  

```py
pandas.DataFrame(data, index, columns, dtype, copy)
```

参数说明：  
- data -- 一组数据（ndarray, Series, map, lists, dict等类型）
- index -- 行索引/行标签/轴标签  
- columns -- 列索引/列标签。默认为 RangeIndex(0, 1, 2, ..., n)
- dtype -- 数据类型  
- copy -- 拷贝数据，默认为 False  

关于列序列：  
创建 DataFrame 时如果指定了列序列，DataFrame 的列就会按照指定的顺序进行排序  
```py
# 输入
import pandas as pd

data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state', 'pop'])
print(df)

# 输出
   year   state  pop
0  2000    Ohio  1.5
1  2001    Ohio  1.7
2  2002    Ohio  3.6
3  2001  Nevada  2.4
4  2002  Nevada  2.9
5  2003  Nevada  3.2
```

## 2、DataFrame 支持多种输入数据

### 2.1 用二维 ndarray 数组生成 DataFrame
- 二维数组的一行代表 DataFrame 中的一条记录  
- 如果没有指定索引和列，将会自动生成索引序列和列序列  
```py
# 输入
import pandas as pd
import numpy as np

two_array = np.array([[1., 2., 3., 4.],
                      [4., 3., 2., 1.]])

df1 = pd.DataFrame(two_array)
print(df1)
print('----------------------------')
df2 = pd.DataFrame(two_array, index=['one', 'two'], columns=['a', 'b', 'c', 'd'])
print(df2)

# 输出
     0    1    2    3
0  1.0  2.0  3.0  4.0
1  4.0  3.0  2.0  1.0
----------------------------
       a    b    c    d
one  1.0  2.0  3.0  4.0
two  4.0  3.0  2.0  1.0
```

### 2.2 Series、字典、列表、元组组成的列表生成 DataFrame
- 和二维数组生成 DataFrame 类似，列表的各项是 DataFrame 中的一行。其中字典和 Series 索引的并集将会成为 DataFrame 的列  
- 如果是由 Series 组成的列表或字典组成的列表生成的 DataFrame  
  由于 Series 会生成行索引，创建 DataFrame 时会将行索引转化为列，因此 DataFrame 指定的列最好和 Series 的索引（未指定时默认 0 开始的自然数序列）存在交集，否则将会没有数值；但 DataFrame 的行索引可以随意进行指定  
  字典组成的列表类似，DataFrame 指定的列最好和字典的建序列存在交集，否则将会没有数值；但 DataFrame 的行索引可以随意进行指定  
```py
# 输入
import pandas as pd

df1 = pd.DataFrame([pd.Series([1, 2, 3, 4]), pd.Series([2, 3, 4, 5])])
print(df1)
print('----------------------------')
# 行索引可以进行任意指定
df2 = pd.DataFrame([pd.Series([1, 2, 3, 4]), pd.Series([2, 3, 4, 5])], index=['one', 'two'])
print(df2)
print('----------------------------')
# Series 本身的行索引[0, 1, 2, 3]和指定的列['a', 'b', 'c', 'd']无交集，DataFrame 无数值
df3 = pd.DataFrame([pd.Series([1, 2, 3, 4]), pd.Series([2, 3, 4, 5])], columns=['a', 'b', 'c', 'd'])
print(df3)
print('----------------------------')
# 元组组成的列表本身没有行索引和列，因此随意指定行索引和列
df4 = pd.DataFrame([(1, 2, 3, 4), (2, 3, 4, 5)], columns=['a', 'b', 'c', 'd'])
print(df4)
print('----------------------------')
# 字典组成的列表的键序列最好和制定的列存在交集
df5 = pd.DataFrame([{'a': 1, 'b': 2}, {'a': 10, 'b': 20, 'c': 30}], columns=['b', 'c'])
print(df5)

# 输出
   0  1  2  3
0  1  2  3  4
1  2  3  4  5
----------------------------
     0  1  2  3
one  1  2  3  4
two  2  3  4  5
----------------------------
    a   b   c   d
0 NaN NaN NaN NaN
1 NaN NaN NaN NaN
----------------------------
   a  b  c  d
0  1  2  3  4
1  2  3  4  5
----------------------------
    b     c
0   2   NaN
1  20  30.0
```

### 2.3 用 Series 字典生成 DataFrame
- 如果没有指定索引序列，那么索引是每个 Series 索引的**并集**；如果指定了索引序列，则指定索引序列将作为索引  
- 如果没有指定列，那么列是字典键的有序列表；如果指定列，则指定列将作为列，而不是指定列和字典键的并集  
- DataFrame 指定的行索引最好和 Series 的索引（未指定时默认 0 开始的自然数序列）存在交集，否则将会没有数值  
```py
# 输入
import pandas as pd

d = {'one': pd.Series([1., 2., 3.], index=['a', 'b', 'c']),
     'two': pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}

df1 = pd.DataFrame(d)
df2 = pd.DataFrame(d, index=['d', 'b', 'a'])
df3 = pd.DataFrame(d, index=['d', 'b', 'a'], columns=['two', 'three'])
print(df1)
print('-------------------')
print(df2)
print('-------------------')
print(df3)

# 输出
   one  two
a  1.0  1.0
b  2.0  2.0
c  3.0  3.0
d  NaN  4.0
-------------------
   one  two
d  NaN  4.0
b  2.0  2.0
a  1.0  1.0
-------------------
   two three
d  4.0   NaN
b  2.0   NaN
a  1.0   NaN
```
```py
# 输入
d = {'one': pd.Series([1., 2., 3.]),
     'two': pd.Series([1., 2., 3., 4.])}

# 字典 d 生成后默认的行索引序列是[0, 1, 2, 3],如果指定的行索引序列与其无关将无数值
df1 = pd.DataFrame(d, index=[2, 3, 4, 5])
print(df1)
print('----------------------------')
df2 = pd.DataFrame(d, index=['a', 'b', 'c', 'd'])
print(df2)

# 输出
   one  two
2  3.0  3.0
3  NaN  4.0
4  NaN  NaN
5  NaN  NaN
----------------------------
   one  two
a  NaN  NaN
b  NaN  NaN
c  NaN  NaN
d  NaN  NaN
```

### 2.4 用数组、列表、元组组成的字典生成 DataFrame
- 数组、列表、元组序列的长度必须相同  
- 如果没有传递索引参数，会自动生成与序列长度相同的索引序列；如果传递了索引参数，传入的索引参数的长度必须和序列长度一致  
- 如果没有指定列，那么列是字典键的有序列表；如果指定列，则指定列将作为列，而不是指定列和字典键的并集  
```py
# 输入
import pandas as pd

d = {'one': [1., 2., 3., 4.],
     'two': [4., 3., 2., 1.]}

df1 = pd.DataFrame(d)
df2 = pd.DataFrame(d, index=['a', 'b', 'c', 'd'])
df3 = pd.DataFrame(d, index=['a', 'b', 'c', 'd'], columns=['two', 'three'])
print(df1)
print('-------------------')
print(df2)
print('-------------------')
print(df3)

# 输出
   one  two
0  1.0  4.0
1  2.0  3.0
2  3.0  2.0
3  4.0  1.0
-------------------
   one  two
a  1.0  4.0
b d = {'one': pd.Series([1., 2., 3.]),
     'two': pd.Series([1., 2., 3., 4.])}

df = pd.DataFrame(d, index=[1, 2, 3, 4])
print(df)    0  1  2  3
0  1  2  3  4
1  2  3  4  5
--------------------
   1  2  3
0  2  3  4
1  3  4  52.0  3.0
c  3.0  2.0
d  4.0  1.0
-------------------
   two three
a  4.0   NaN
b  3.0   NaN
c  2.0   NaN
d  1.0   NaN
```
```py
# 输入
import pandas as pd
import numpy as np

array1 = np.array([1., 2., 3., 4.])
array2 = np.array([4., 3., 2., 1.])
d = {'one': array1, 'two': array2}

df1 = pd.DataFrame(d)
print(df1)
print('----------------------------')
df2 = pd.DataFrame(d, index=['a', 'b', 'c', 'd'])
print(df2)

# 输出
   one  two
0  1.0  4.0
1  2.0  3.0
2  3.0  2.0
3  4.0  1.0
----------------------------
   one  two
a  1.0  4.0
b  2.0  3.0
c  3.0  2.0
d  4.0  1.0
```

### 2.5 用嵌套字典生成 DataFrame
- 外层字典的键作为列；内层字典的键作为行索引  
- 可以指定列和索引行  
```py
# 输入
import pandas as pd

d = {'one': {'a': 1, 'b': 2, 'c': 3}, 'two': {'a': 4, 'b': 3, 'c': 2, 'd': 1}}

df1 = pd.DataFrame(d)
print(df1)
print('----------------------------')
df2 = pd.DataFrame(d, index=['a', 'b', 'c', 'e'])
print(df2)
print('----------------------------')
df3 = pd.DataFrame(d, columns=['two', 'three'])
print(df3)

# 输出
   one  two
a  1.0    4
b  2.0    3
c  3.0    2
d  NaN    1
----------------------------
   one  two
a  1.0  4.0
b  2.0  3.0
c  3.0  2.0
e  NaN  NaN
----------------------------
   two three
a    4   NaN
b    3   NaN
c    2   NaN
d    1   NaN
```

### 2.6 通过另一个 DataFrame 生成 DataFrame
- 该 DataFrame 的索引将会被沿用，除非显示指定其他索引  
- 指定的索引最好和该 DataFrame 的索引存在交集  
```py
# 输入
import pandas as pd
import numpy as np

df1 = pd.DataFrame(np.array([[1, 2, 3, 4],
                             [2, 3, 4, 5]]))
print(df1)
print('--------------------')
df2 = pd.DataFrame(df1, columns=[1, 2, 3])
print(df2)

# 输出
   0  1  2  3
0  1  2  3  4
1  2  3  4  5
--------------------
   1  2  3
0  2  3  4
1  3  4  5
```

## 行列索引


## DataFrame 的常用属性

### index
- 描述  
  `index`属性可以获取 DataFrame 的行索引序列  
  
- 语法  
  ```py
  DataFrame.index
  ```

- 实例  
  见`columns`实例  

### columns
- 描述  
  `columns`属性可以获取 DataFrame 的列序列  
  
- 语法  
  ```py
  DataFrame.columns
  ```

- 实例  
  ```py
  # 输入
  import pandas as pd

  data = {'state': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data)
  print(df.index)
  print(df.columns)
  
  # 输出
  RangeIndex(start=0, stop=6, step=1)
  Index(['state', 'year', 'pop'], dtype='object')
  ```

## DataFrame 的常用方法

### head()
- 描述  
  `head()`方法可以选取前五行，对较大的 DataFrame 比较友好
  
- 语法  
  ```py
  DataFrame.head()
  ```

- 实例  
  ```py
  # 输入
  import pandas as pd
  import numpy as np

  df1 = pd.DataFrame(np.array([[1, 2, 3, 4],
                               [2, 3, 4, 5],
                               [3, 4, 5, 6],
                               [4, 5, 6, 7],
                               [5, 6, 7, 8],
                               [6, 7, 8, 9],
                               [7, 8, 9, 10]]))
  print(df1)
  print('--------------------')
  df2 = pd.DataFrame(df1)
  print(df2.head())
  
  # 输出
     0  1  2   3
  0  1  2  3   4
  1  2  3  4   5
  2  3  4  5   6
  3  4  5  6   7
  4  5  6  7   8
  5  6  7  8   9
  6  7  8  9  10
  --------------------
     0  1  2  3
  0  1  2  3  4
  1  2  3  4  5
  2  3  4  5  6
  3  4  5  6  7
  4  5  6  7  8
  ```
