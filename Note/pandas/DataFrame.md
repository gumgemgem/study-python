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

## 2、创建 DataFrame

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
  由于 Series 会生成行索引，创建 DataFrame 时会将行索引转化为列，因此 DataFrame 指定的列最好和 Series 的索引（未指定时默认 0 开始的自然数序列）存在交集，否则将会没有数值；但 Daimport numpy as npaFrame 的行索引可以随意进行指定  
  字import matplotlib.pyplot as plt典组成的列表类似，DataFrame 指定的列最好和字典的建序列存在交集，否则将会没有数值；但 DataFrame 的行索引可以随意进行指定  
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
b  2.0  3.0
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

### 2.7 从外部文件数据创建 DataFrame
[详情见 interaction-of-external-files.md](interaction-of-external-files.md)

## 3、列操作

### 3.1 提取列
- 通过类似字典标记的方式`DataFrame[column]`或属性的方式`DataFrame.column`，可以提取 DataFrame 的某一列为一个 Series  
- `DataFrame[column]`适用于任何列名，`DataFrame.column`只适用于列名是一个合理的 Python 变量名时  
- 通过`DataFrame[[column1, column2, ...]]`的方式可以得到一组列  
- 此方法不可以进行切片操作，即不存在`DataFrame[column1: column2]`的语法  

```py
# 输入
import pandas as pd

data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'])
print(df['year'])
print('------------------------')
print(df.year)
print('------------------------')
# 这里不可以使用 df.state sta
print(df['state sta'])
print('------------------------')
print(df[['year', 'pop']])

# 输出
0    2000
1    2001
2    2002
3    2001
4    2002
5    2003
Name: year, dtype: int64
------------------------
0    2000
1    2001
2    2002
3    2001
4    2002
5    2003
Name: year, dtype: int64
------------------------
0      Ohio
1      Ohio
2      Ohio
3    Nevada
4    Nevada
5    Nevada
Name: state sta, dtype: object
------------------------
       year  pop
one    2000  1.5
two    2001  1.7
three  2002  3.6
four   2001  2.4
five   2002  2.9
six    2003  3.2
```

### 3.2 修改列
- 列可以通过赋值的方式进行修改  
- `DataFrame.column`的方式不可以创建新的列，只能用`DataFrame[column]`的方式  
- 将列表或数组赋值给某个列时，其长度必须和 DataFrame 的长度相匹配  
- 将 Series 赋值给某个列时，会精确匹配 DataFrame 的行索引，所有空位都会被填上缺失值  
```py
import pandas as pd
import numpy as np

data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state sta', 'pop', 'debt'],
                  index=['one', 'two', 'three', 'four', 'five', 'six'])

df['debt'] = 16.5
print(df)
print('----------------------------------')
df['debt'] = np.arange(6)
print(df)
print('----------------------------------')
df['debt'] = pd.Series([-1.2, -1.5, -1.7], index=['two', 'four', 'five'])
print(df)

# 输出
       year state sta  pop  debt
one    2000      Ohio  1.5  16.5
two    2001      Ohio  1.7  16.5
three  2002      Ohio  3.6  16.5
four   2001    Nevada  2.4  16.5
five   2002    Nevada  2.9  16.5
six    2003    Nevada  3.2  16.5
----------------------------------
       year state sta  pop  debt
one    2000      Ohio  1.5     0
two    2001      Ohio  1.7     1
three  2002      Ohio  3.6     2
four   2001    Nevada  2.4     3
five   2002    Nevada  2.9     4
six    2003    Nevada  3.2     5
----------------------------------
       year state sta  pop  debt
one    2000      Ohio  1.5   NaN
two    2001      Ohio  1.7  -1.2
three  2002      Ohio  3.6   NaN
four   2001    Nevada  2.4  -1.5
five   2002    Nevada  2.9  -1.7
six    2003    Nevada  3.2   NaN
```

### 3.3 删除列
`del DataFrame[column]`或`del DataFrame.column`可以删除指定列  
```py
# 输入
import pandas as pd

data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                  index=['one', 'two', 'three', 'four', 'five', 'six'])

df['eastern'] = (df['state sta'] == 'Ohio')
print(df)
print('----------------------------------')
del df['eastern']
print(df)

# 输出
       year state sta  pop  eastern
one    2000      Ohio  1.5     True
two    2001      Ohio  1.7     True
three  2002      Ohio  3.6     True
four   2001    Nevada  2.4    False
five   2002    Nevada  2.9    False
six    2003    Nevada  3.2    False
----------------------------------
       year state sta  pop
one    2000      Ohio  1.5
two    2001      Ohio  1.7
three  2002      Ohio  3.6
four   2001    Nevada  2.4
five   2002    Nevada  2.9
six    2003    Nevada  3.2
```

## 4、用 loc 和 iloc 进行选取
轴标签`loc`和整数索引`iloc`，可以从 DataFrame 选择行或行和列的子集  

|类型|说明|
|:-----|:----|
|df[val]|从 DataFrame 选取单列或一组列|
|df.loc[val]|通过标签，选取 DataFrame 的单个行或一组行|
|df.loc[:, val]|通过标签，选取单个列或列子集|
|df.loc[val1, val2]|通过标签同时选取行和列|
|df.iloc[where]|通过整数位置，从 DataFrame 选取单个行或行子集|
|df.iloc[:, where]|通过整数位置，从 DataFrame 选取单个列或列子集|
|df.iloc[where_i, where_j]|通过整数位置，同时选取行和列|

注意：  
- 整数索引`iloc`是从 0 开始  
- 轴标签`loc`和整数索引`iloc`都可进行行列的切片。轴标签`loc`进行切片时是**左闭右闭**的区间；整数索引`iloc`进行切片时是**左闭右开**的区间  
- 当`df[val]`取多列时，多列必须存放在列表中；且取列无切片的方式  

实例：  
```py
# 输入
import pandas as pd

data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                  index=['one', 'two', 'three', 'four', 'five', 'six'])

print(df.loc['one'])
print('----------------------------------')
print(df.loc[['one', 'two']])
print('----------------------------------')
print(df.loc['one': 'three'])
print('----------------------------------')
print(df.loc[:, 'year'])
print('----------------------------------')
print(df.loc['one', 'year'])
print('----------------------------------')
print(df.loc['one': 'three', 'year': 'pop'])

# 输出
year         2000
state sta    Ohio
pop           1.5
Name: one, dtype: object
----------------------------------
     year state sta  pop
one  2000      Ohio  1.5
two  2001      Ohio  1.7
----------------------------------
       year state sta  pop
one    2000      Ohio  1.5
two    2001      Ohio  1.7
three  2002      Ohio  3.6
----------------------------------
one      2000
two      2001
three    2002
four     2001
five     2002
six      2003
Name: year, dtype: int64
----------------------------------
2000
----------------------------------
       year state sta  pop
one    2000      Ohio  1.5
two    2001      Ohio  1.7
three  2002      Ohio  3.6
```
```py
# 输入
import pandas as pd

data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
        'year': [2000, 2001, 2002, 2001, 2002, 2003],
        'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                  index=['one', 'two', 'three', 'four', 'five', 'six'])

print(df.iloc[0])
print('----------------------------------')
print(df.iloc[[0, 1]])
print('----------------------------------')
print(df.iloc[0: 2])
print('----------------------------------')
print(df.iloc[:, 0])
print('----------------------------------')
print(df.iloc[0, 0])
print('----------------------------------')
print(df.iloc[0: 2, 0: 1])

# 输出
year         2000
state sta    Ohio
pop           1.5
Name: one, dtype: object
----------------------------------
     year state sta  pop
one  2000      Ohio  1.5
two  2001      Ohio  1.7
----------------------------------
     year state sta  pop
one  2000      Ohio  1.5
two  2001      Ohio  1.7
----------------------------------
one      2000
two      2001
three    2002
four     2001
five     2002
six      2003
Name: year, dtype: int64
----------------------------------
2000
----------------------------------
     year
one  2000
two  2001
```

## 5、DataFrame 的常用属性

### 5.1 index
- 描述  
  `index`属性可以获取 DataFrame 的行索引序列  
  
- 语法  
  ```py
  DataFrame.index
  ```

- 实例  
  见`columns`实例  

### 5.2 columns
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
  
### 5.3 name
- 描述  
  - `name`属性可以给 DataFrame 的索引和列命名  
  - `df.index.name`给索引命名；`df.columns.name`给列命名  

- 实例  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  print(df)
  print('--------------------------------')
  df.columns.name = 'country'
  df.index.name = 'sequence'
  print(df)
  
  # 输出
  a    1.0
  b    2.0
  c    3.0
  d    4.0
  e    5.0
  dtype: float64
  命名前 obj 数据和索引标签的名称： None 和 None
  --------------------------------
  命名后 obj 数据和索引标签的名称： number 和 letter
  letter
  a    1.0
  b    2.0
  c    3.0
  d    4.0
  e    5.0
  Name: number, dtype: float64
  ```
  
### 5.4 values
- 描述  
  `values`属性可以以二维数组的形式返回 DataFrame 中的数据  
  
- 语法  
  ```py
  DataFrame.values
  ```

- 实例  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  print(df)
  print('---------------------------------------')
  print(df.values)
  
  # 输出
         year state sta  pop
  one    2000      Ohio  1.5
  two    2001      Ohio  1.7
  three  2002      Ohio  3.6
  four   2001    Nevada  2.4
  five   2002    Nevada  2.9
  six    2003    Nevada  3.2
  ---------------------------------------
  [[2000 'Ohio' 1.5]
   [2001 'Ohio' 1.7]
   [2002 'Ohio' 3.6]
   [2001 'Nevada' 2.4]
   [2002 'Nevada' 2.9]
   [2003 'Nevada' 3.2]]
  ```

### 5.5 T
- 描述  
  `T`属性可以对 DataFrame 进行转置  
  
- 语法  
  ```py
  DataFrame.T
  ```

- 实例  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])
  print('----------------------- 转置前 ----------------------')
  print(df)
  print('\n')
  print('----------------------- 转置后 ----------------------')
  print(df.T)
  
  # 输出
  ----------------------- 转置前 ----------------------
         year state sta  pop
  one    2000      Ohio  1.5
  two    2001      Ohio  1.7
  three  2002      Ohio  3.6
  four   2001    Nevada  2.4
  five   2002    Nevada  2.9
  six    2003    Nevada  3.2


  ----------------------- 转置后 ----------------------
              one   two three    four    five     six
  year       2000  2001  2002    2001    2002    2003
  state sta  Ohio  Ohio  Ohio  Nevada  Nevada  Nevada
  pop         1.5   1.7   3.6     2.4     2.9     3.2
  ```

## 6、DataFrame 的常用方法

### 6.1 head()
- 描述  
  `head(n)`方法可以选取前 n 行，对较大的 DataFrame 比较友好
  
- 语法  
  ```py
  DataFrame.head(n)
  ```

  参数说明：  
  n -- 整数（**默认**：5）  

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

### 6.2 tail()
- 描述  
  `tail(n)`方法可以选取最后 n 行，对较大的 DataFrame 比较友好
  
- 语法  
  ```py
  DataFrame.tail(n)
  ```

  参数说明：  
  n -- 整数（**默认**：5）  