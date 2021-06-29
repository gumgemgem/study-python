# Series

约定导入`Pandas`和`Series、DataFrame`的写法：
```py
import pandas as pd
```
调用：`pd.Series()`
```py
import pandas
from pandas import Series, DataFrame
```
调用：`Series()`

## 1、定义
`Series`是一种类似于一维数组的对象，也类似于表格中的一个列  
它由一组数据（各种`NumPy`数据类型）以及与之相关的数据标签（即索引）组成  
```py
pandas.Series(data, index, dtype, name, copy)
```
参数说明：  
- data -- 一组数据（ndarray类型）  
- index -- 数据索引标签，默认从 0 开始  
- dtype -- 数据类型，默认会自己判断  
- name -- 设置名称  
- copy -- 拷贝数据，默认为 False  

实例：  
```py
# 输入
import pandas as pd

obj = pd.Series([4, 7, -5, 3])
print(obj)

# 输出
0    4
1    7
2   -5
3    3
dtype: int64
```

## 2、关于索引标签
- 当不采用默认的索引序列时，可以指定各个值的索引标签  
  ```py
  # 输入
  import pandas as pd

  obj = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj)

  # 输出
  d    4
  b    7
  a   -5
  c    3
  dtype: int64
  ```
  
- 索引标签可以通过[`index属性`](#index)赋值的方式直接进行修改：`Series对象.index = 新的索引标签列表`  
  ```py
  import pandas as pd

  d = {'a': 1., 'b': 2., 'c': 3., 'd': 4., 'e': 5.}
  obj = pd.Series(d)
  print(obj)
  print('-----------------')
  obj.index = ['A', 'B', 'C', 'D', 'E']
  print(obj)
  
  # 输出
  a    1.0
  b    2.0
  c    3.0
  d    4.0
  e    5.0
  dtype: float64
  -----------------
  A    1.0
  B    2.0
  C    3.0
  D    4.0
  E    5.0
  dtype: float64
  ```

## 3、data 的类别
关于`data`的主要类别，主要分为：多维数组、字典、标量值（如：5）  

- 多维数组  
  ```py
  # 输入
  import pandas as pd
  import numpy as np

  obj = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
  print(obj)
  
  # 输出
  a   -0.983872
  b   -0.460480
  c    0.258876
  d   -0.001938
  e    0.411950
  dtype: float64
  ```
  
- 字典  
  `Series`可以通过字典实例化得到  
  **注意**：  
  `data`为字典，且未设置`index`参数时，Python 版本 >= 3.6 且 Pandas 版本 >= 0.23，`Series`将按照字典的插入顺序排序索引  
  如果设置了`index`参数，则按照索引标签提取`data`中的值，**缺失数据**用`NaN`（Not a Number）表示  
  ```py
  # 输入
  import pandas as pd

  d = {'b': 1, 'a': 0, 'c': 2}
  obj = pd.Series(d)
  print(obj)
  
  # 输出
  b    1
  a    0
  c    2
  dtype: int64
  ```
  ```py
  # 输入
  import pandas as pd

  d = {'b': 1, 'a': 0, 'c': 2}
  obj = pd.Series(d, index=['b', 'c', 'd', 'a'])
  print(obj)
  
  # 输出
  b    1.0
  c    2.0
  d    NaN
  a    0.0
  dtype: float64
  ```
   
- 标量值  
  `data`是标量值时，必须提供索引。`Series`按照索引长度重复该标量值  
  ```py
  # 输入
  import pandas as pd

  obj = pd.Series(5., index=['a', 'b', 'c', 'd', 'e'])
  print(obj)
  
  # 输出
  a    5.0
  b    5.0
  c    5.0
  d    5.0
  e    5.0
  dtype: float64
  ```

## 3、检测缺失值

- Pandas中的`isnull()`和`notnull()`函数用于检测缺失数据：`isnull(Series对象)`/`notnull(Series对象)`  
  ```py
  # 输入
  import pandas as pd

  d = {'b': 1, 'a': 0, 'c': 2}
  obj = pd.Series(d, index=['b', 'c', 'd', 'a'])
  print(obj)
  print('---------------')
  print(pd.isnull(obj))
  print('---------------')
  print(pd.notnull(obj))
  
  # 输出
  b    1.0
  c    2.0
  d    NaN
  a    0.0
  dtype: float64
  ---------------
  b    False
  c    False
  d     True
  a    False
  dtype: bool
  ---------------
  b     True
  c     True
  d    False
  a     True
  dtype: bool
  ```
  
- `Series`中也存在`isnull()`和`notnull()`的方法：`Series对象.isnull()`/`Series对象.notnull()`  
  ```py
  # 输入
  import pandas as pd

  d = {'b': 1, 'a': 0, 'c': 2}
  obj = pd.Series(d, index=['b', 'c', 'd', 'a'])
  print(obj)
  print('---------------')
  print(obj.isnull())
  print('---------------')
  print(obj.notnull())
  
  # 输出
  b    1.0
  c    2.0
  d    NaN
  a    0.0
  dtype: float64
  ---------------
  b    False
  c    False
  d     True
  a    False
  dtype: bool
  ---------------
  b     True
  c     True
  d    False
  a     True
  dtype: bool
  ```

## 4、索引和切片

- 索引  
  可以通过索引的方式选取`Series`中的某个值：`Series对象[index]`  
  ```py
  # 输入
  import pandas as pd

  obj1 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj1['b'])

  obj2 = pd.Series([4, 7, -5, 3], index=[2, 3, 4, 5])
  print(obj2[4])
  
  # 输出
  7
  -5
  ```
  
- 切片  
  - 通过索引列表的方式进行切片：`Series对象[[索引列表]]`  
  ```py
  # 输入
  import pandas as pd

  obj1 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj1[['b', 'c']])

  obj2 = pd.Series([4, 7, -5, 3], index=[2, 3, 4, 5])
  print(obj2[[2, 5]])
  
  # 输出
  b    7
  c    3
  dtype: int64
  2    4
  5    3
  dtype: int64
  ```
  
  - 通过列表切片的方式进行切片：`Series对象[start: stop: step]`  
  **注意**：此时切片中的起始值和步长与列表中的定义一致，与`Series`中`data`是否是数值无关  
  ```py
  # 输入
  import pandas as pd

  obj1 = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj1[0: 4])

  obj2 = pd.Series([4, 7, -5, 3], index=[2, 3, 4, 5])
  print(obj2[1: 3])
  
  # 输出
  d    4
  b    7
  a   -5
  c    3
  dtype: int64
  3    7
  4   -5
  dtype: int64
  ```

## 5、矢量运算与对齐 Series 标签
- `Series`与`ndarray`一样，支持大多数 NumPy 函数和运算（根据布尔型数组进行过滤、四则运算、数学函数等），并且运算后都会保留索引值的链接  
  ```py
  # 输入
  import pandas as pd

  obj = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj > 0)   # 生成布尔型的数组
  print('---------------')
  print(obj[obj > 0])   # 根据布尔型的数组进行过滤，筛掉 False 的值

  # 输出
  d     True
  b     True
  a    False
  c     True
  dtype: bool
  ---------------
  d    4
  b    7
  c    3
  dtype: int64
  ```
  ```py
  # 输入
  import pandas as pd
  import numpy as np

  obj = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj * 2)   # 四则运算
  print('---------------')
  print(np.exp(obj))   # 数学函数

  # 输出
  d     8
  b    14
  a   -10
  c     6
  dtype: int64
  ---------------
  d      54.598150
  b    1096.633158
  a       0.006738
  c      20.085537
  dtype: float64
  ```
  
- Series 之间的操作会自动基于索引标签对齐数据，因此不用顾及执行计算操作的 Series 是否有相同的标签  
  **注意**： 其计算结果是所有涉及索引的并集，可以避免信息的丢失，类似于数据库中的`join`操作  
  ```py
  # 输入
  import pandas as pd

  d = {'a': 1., 'b': 2., 'c': 3., 'd': 4., 'e': 5.}
  obj1 = pd.Series(d, index=['a', 'b', 'c', 'd'])
  obj2 = pd.Series(d, index=['b', 'c', 'd', 'f'])
  print(obj1)
  print('--------------')
  print(obj2)
  print('--------------')
  print(obj1 + obj2)
  
  # 输出
  a    1.0
  b    2.0
  c    3.0
  d    4.0
  dtype: float64
  --------------
  b    2.0
  c    3.0
  d    4.0
  f    NaN
  dtype: float64
  --------------
  a    NaN
  b    4.0
  c    6.0
  d    8.0
  f    NaN
  dtype: float64
  ```
  ```py
  # 输入
  import pandas as pd

  d = {'a': 1., 'b': 2., 'c': 3., 'd': 4., 'e': 5.}
  obj = pd.Series(d)
  print(obj)
  print('--------------')
  print(obj[1:] + obj[:-1])
  
  # 输出
  a    1.0
  b    2.0
  c    3.0
  d    4.0
  e    5.0
  dtype: float64
  --------------
  a    NaN
  b    4.0
  c    6.0
  d    8.0
  e    NaN
  dtype: float64
  ```

## 6、Series 类似字典
- `Series`可以判断某个索引标签是否在`Series`中  
  ```py
  # 输入
  import pandas as pd

  obj = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print('b' in obj)

  # 输出
  True
  ```
 
- `Series`可以用索引标签更改值或增加值  
  ```py
  # 输入
  import pandas as pd

  obj = pd.Series([4, 7, -5, 3], index=['d', 'b', 'a', 'c'])
  print(obj)
  print('---------------')
  obj['a'] = 2   # 更改值
  print(obj)
  print('---------------')
  obj['e'] = 6   # 增加值
  print(obj)
  
  # 输出
  d    4
  b    7
  a   -5
  c    3
  dtype: int64
  ---------------
  d    4
  b    7
  a    2
  c    3
  dtype: int64
  ---------------
  d    4
  b    7
  a    2
  c    3
  e    6
  dtype: int64
  ```

## 7、Series 的属性

#### values
`values`作为 Pandas 和 NumPy 中间转换的桥梁，可以将 Pandas 中的数据格式转化为 NumPy 中的数组形式  
```py
# 输入
import pandas as pd

obj = pd.Series([4, 7, -5, 3])
print(obj.values)
print(type(obj.values))

# 输出
[ 4  7 -5  3]
<class 'numpy.ndarray'>
```

#### array
`array`可以将 Series 中的 data 数组提取出来  
```py
# 输入
import pandas as pd

d = {'a': 1., 'b': 2., 'c': 3., 'd': 4., 'e': 5.}
obj = pd.Series(d)
print(obj.array)

# 输出
<PandasArray>
[1.0, 2.0, 3.0, 4.0, 5.0]
Length: 5, dtype: float64
```

#### index
`index`可以获得 Series 对象的索引对象  
```py
# 输入
import pandas as pd

obj = pd.Series([4, 7, -5, 3])
print(obj.index)

# 输出
RangeIndex(start=0, stop=4, step=1)
```

#### name
`name`属性可以为 Series 对象的数据和索引标签命名  
```py
# 输入
import pandas as pd

d = {'a': 1., 'b': 2., 'c': 3., 'd': 4., 'e': 5.}
obj = pd.Series(d)
print(obj)
print('命名前 obj 数据和索引标签的名称： {} 和 {}'.format(obj.name, obj.index.name))
obj.name = 'number'
obj.index.name = 'letter'
print('命名后 obj 数据和索引标签的名称： {} 和 {}'.format(obj.name, obj.index.name))

# 输出
a    1.0
b    2.0
c    3.0
d    4.0
e    5.0
dtype: float64
命名前 obj 数据和索引标签的名称： None 和 None
命名后 obj 数据和索引标签的名称： number 和 letter
```

#### dtype
`dtype`可以获得 Series 对象的数据类型和索引标签的类型  
```py
# 输入
import pandas as pd

d = {'a': 1., 'b': 2., 'c': 3., 'd': 4., 'e': 5.}
obj = pd.Series(d)
print('obj 数据类型和索引标签的类型： {} 和 {}'.format(obj.dtype, obj.index.dtype))

# 输出
obj 数据类型和索引标签的类型： float64 和 object
```
