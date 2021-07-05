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

## 定义
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

## DataFrame 支持多种输入数据

### 用二维 ndarray 数组生成 DataFrame
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

### Series、字典、列表、元组组成的列表生成 DataFrame
- 和二维数组生成 DataFrame 类似，列表的各项是 DataFrame 中的一行。其中字典和 Series 索引的并集将会成为 DataFrame 的列  
- DataFrame 指定的行索引最好和 Series 的行索引（未指定时默认 0 开始的自然数序列）有关系，否则将会没有数值

### 用 Series 字典生成 DataFrame
- 如果没有指定索引序列，那么索引是每个 Series 索引的**并集**；如果指定了索引序列，则指定索引序列将作为索引  
- 如果没有指定列，那么列是字典键的有序列表；如果指定列，则指定列将作为列，而不是指定列和字典键的并集  
- DataFrame 指定的行索引最好和 Series 的行索引（未指定时默认 0 开始的自然数序列）有关系，否则将会没有数值  
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

### 用数组、列表、元组组成的字典生成 DataFrame
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
print(df) 2.0  3.0
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

### 用嵌套字典生成 DataFrame
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
e  NaN  NaN+
----------------------------
   two three
a    4   NaN
b    3   NaN
c    2   NaN
d    1   NaN
```

