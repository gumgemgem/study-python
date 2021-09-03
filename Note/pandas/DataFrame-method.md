# DataFrame 常用方法

## 缺失数据处理

### 1、fillna()
- 描述  
使用指定的方法填充 Na/NaN 值

- 语法  
```py
DataFrame.fillna(value=None, method=None, axis=None, inplace=False, limit=None, downcast=None)
```

|常用参数|说明|
|-----|-----|
|value|标量、字典、Series、DataFrame 类型；用于填充缺失值<br>或者指定为每个 index（对于 Series）或 columns（对于 DataFrame）使用字典/Series/DataFrame的值|
|method|{'backfill'/'bfill', 'pad'/'ffill', None（**默认**）}；<br>'backfill'/'bfill' -- 向后填充，使用下一个有效值来填充空白<br>'pad'/'ffill' -- 向前填充，使用最后一个有效值填充空白|
|axis|{0/‘index’, 1/‘columns’}；沿着指定轴向填充缺失值|
|limit|整型（**默认** None）；表示填充的最大数量|
|inplace|布尔类型（**默认** False）；当为 True 时，表示上述修改在原地进行，相应的视图也会进行修改|

返回值：  
返回 DataFrame 的对象，并不一定是原地进行修改  

- 实例  
```py
# 输入
import pandas as pd
import numpy as np


def func(df):
    print(df)
    # 用 0 填充
    print(df.fillna(0))
    # 前向填充
    print(df.fillna(method='ffill'))
    # 用字典进行填充，并限制填充数目
    dict1 = {'A': 1, 'B': 2, 'C': 3, 'D': 4}
    print(df.fillna(value=dict1, limit=1))
    # 用 DataFrame 进行填充
    df2 = pd.DataFrame(np.zeros((4, 4)), columns=list('ABCE'))
    print(df.fillna(df2))


df1 = pd.DataFrame([[np.nan, 2, np.nan, 0],
                   [3, 4, np.nan, 1],
                   [np.nan, np.nan, np.nan, 5],
                   [np.nan, 3, np.nan, 4]],
                  columns=list("ABCD"))
func(df1)

# 输出
     A    B   C  D
0  NaN  2.0 NaN  0
1  3.0  4.0 NaN  1
2  NaN  NaN NaN  5
3  NaN  3.0 NaN  4
     A    B    C  D
0  0.0  2.0  0.0  0
1  3.0  4.0  0.0  1
2  0.0  0.0  0.0  5
3  0.0  3.0  0.0  4
     A    B   C  D
0  NaN  2.0 NaN  0
1  3.0  4.0 NaN  1
2  3.0  4.0 NaN  5
3  3.0  3.0 NaN  4
     A    B    C  D
0  1.0  2.0  3.0  0
1  3.0  4.0  NaN  1
2  NaN  2.0  NaN  5
3  NaN  3.0  NaN  4
     A    B    C  D
0  0.0  2.0  0.0  0
1  3.0  4.0  0.0  1
2  0.0  0.0  0.0  5
3  0.0  3.0  0.0  4
```

### 2、replace()
- 描述  
替换 DataFrame 中指定的值  
该方法动态地为 DataFrame 替换值，与`.loc`和`.iloc`的更新方式不同，该方法不需要指定要更新值的位置  

- 语法  
```py
DataFrame.replace(to_replace=None, value=None, inplace=False, limit=None, regex=False, method='pad')
```

|常用参数|说明|
|---|---|
|to_replace|str, regex, list, dict, Series, int, float, or None<br>-- numeric/str/regex/list：满足条件的值被替换为 value<br>-- dict:<br>1、字典可以指定不同的替换值：value 必须为 None<br>2、用 value 替换字典中指定 DataFrame 中指定列的指定值：value 不能为 None<br>3、嵌套字典`{'col': {'val1': 'val2'}}`替换表示列 col 的值 val1 被替换成值 val2：value 必须为 None|
|value|str, regex, list, dict, scalar, None（**默认**）；替换任何匹配 to_replace 的值|
|limit|前向或后向填充的最大数目|
|inplace|布尔类型（**默认** False）；当为 True 时，表示上述修改在原地进行，相应的视图也会进行修改|

- 实例  
```py
# 输入
import pandas as pd


def func(df):
    print(df)
    # 标量替换
    print(df.replace(0, 5))
    # 列表替换
    print(df.replace([0, 1, 2, 3], 4))
    print(df.replace([0, 1, 2, 3], [3, 2, 1, 0]))
    # 字典替换
    print(df.replace({0: 10, 1: 100}))
    print(df.replace({'A': 0, 'B': 5}, 100))
    print(df.replace({'A': {0: 100, 4: 400}}))


df1 = pd.DataFrame({'A': [0, 1, 2, 3, 4],
                    'B': [5, 6, 7, 8, 9],
                    'C': ['a', 'b', 'c', 'd', 'e']})
func(df1)

# 输出
   A  B  C
0  0  5  a
1  1  6  b
2  2  7  c
3  3  8  d
4  4  9  e
   A  B  C
0  5  5  a
1  1  6  b
2  2  7  c
3  3  8  d
4  4  9  e
   A  B  C
0  4  5  a
1  4  6  b
2  4  7  c
3  4  8  d
4  4  9  e
   A  B  C
0  3  5  a
1  2  6  b
2  1  7  c
3  0  8  d
4  4  9  e
     A  B  C
0   10  5  a
1  100  6  b
2    2  7  c
3    3  8  d
4    4  9  e
     A    B  C
0  100  100  a
1    1    6  b
2    2    7  c
3    3    8  d
4    4    9  e
     A  B  C
0  100  5  a
1    1  6  b
2    2  7  c
3    3  8  d
4  400  9  e
```


## 转换

### 1、copy()
- 描述  
复制 DataFrame 对象

- 语法  
```py
DataFrame.copy(deep=True)
```

参数说明：  
deep -- 布尔类型（**默认** True）  

当 deep=True 时，将使用调用对象的副本创建新对象，对副本的修改不会反映在原始数据中（深拷贝）；  
当 deep=False 时，仅复制对对象的引用，对原始数据的修改都会反映在浅拷贝中（浅拷贝）；  
**注意**：当对象中嵌套包含 Python 对象时，深拷贝将会复制数据，但是不会递归复制 Python 对象，只能引用该 Python 对象，因此更新嵌套数据对象将会反映在深拷贝中  

返回值：  
返回 DataFrame 的深拷贝或是浅拷贝  

- 实例  
```py
# 输入
import pandas as pd


# 当对象中不包含 Python 对象时
print('--- 当对象中不包含 Python 对象时 ---')
df = pd.DataFrame({'A': [0, 1, 2, 3, 4],
                   'B': [5, 6, 7, 8, 9],
                   'C': ['a', 'b', 'c', 'd', 'e']})
df1 = df.copy()              # 深拷贝
df2 = df.copy(deep=False)    # 浅拷贝
df.loc[0, 'C'] = 'A'
print(df1)
print('-------------------------------')
print(df2)

# 输出
--- 当对象中不包含 Python 对象时 ---
   A  B  C
0  0  5  a
1  1  6  b
2  2  7  c
3  3  8  d
4  4  9  e
-------------------------------
   A  B  C
0  0  5  A
1  1  6  b
2  2  7  c
3  3  8  d
4  4  9  e
```
```py
# 输入
import pandas as pd


# 当对象中包含 Python 对象时
print('--- 当对象中包含 Python 对象时 ---')
s = pd.Series([[1, 2], [3, 4]])
s1 = s.copy()
# 深拷贝对 Python 对象是引用，不进行递归复制，因此地址相同
print(id(s[0]), id(s1[0]))

s[0][0] = 100
print('-------------------------------')
# 更改 Python 对象后，s[0] 的地址不变但数据发生改变，深拷贝的地址不变但数据改变
print(id(s[0]), id(s1[0]))
print(s)
print(s1)

s[0] = [5, 6]
print('-------------------------------')
# 更改 Series 数据后，s[0] 的地址和数据均发生改变，深拷贝的地址和数据均不变
print(id(s[0]), id(s1[0]))
print(s)
print(s1)

s[0][0] = 1000
print('-------------------------------')
# 更改 Python 对象后，s[0] 的地址不变但数据发生改变，深拷贝的地址和数据均不变
print(id(s[0]), id(s1[0]))
print(s)
print(s1)

# 输出
--- 当对象中包含 Python 对象时 ---
139870373212744 139870373212744
-------------------------------
139870373212744 139870373212744
0    [100, 2]
1      [3, 4]
dtype: object
0    [100, 2]
1      [3, 4]
dtype: object
-------------------------------
139870525625992 139870373212744
0    [5, 6]
1    [3, 4]
dtype: object
0    [100, 2]
1      [3, 4]
dtype: object
-------------------------------
139870525625992 139870373212744
0    [1000, 6]
1       [3, 4]
dtype: object
0    [100, 2]
1      [3, 4]
dtype: object
```


## 函数应用、GroupBY & window

### 1、apply()
- 描述  
沿着 DataFrame 的某一轴向应用函数  

  - 传递给该函数的对象是 Series 对象，对象的索引是 DataFrame 索引（当 axis=0）或DataFrame 的列（当 axis=1） 

  - 返回类型：当 result_type=None，最终的返回类型根据提供的函数方法的返回类型来推断的；否则，取决于 result_type 的参数  

- 语法  
```py
DataFrame.apply(func, axis=0, raw=False, result_type=None, args=(), **kwargs)
```  

|常用参数|说明|
|---|---|
|func|应用于指定轴向的方法|
|axis|0（**默认**）/'index' 或 1/'columns'；方法应用的轴向|
|raw|布尔类型（**默认** False）；<br>False -- 将每个轴向作为一个 Series 传递给函数<br>True -- 传递的函数将接收一个 ndarray 对象|
|result_type|返回值的类型（**默认** None）<br>None -- 取决于调用方法的返回值<br>'expand' -- 类似于列表的结果就会被转换成 columns<br>'reduce' -- 如果可能的话，返回一个 Series，而不是扩展成类似列表的结果；与 'expand'相反<br>'broadcast' -- 结果将会被广播到原始形状的 DataFrame 中，原始的行列会被保留|
|arg|元组类型；需要传递给 func 的除 array/Series 之外的其他参数|


- 实例  
```py
# 输入
import pandas as pd
import numpy as np

# [[4, 9]] 表示嵌套列表，不是二维数组，因此不具备广播的特性
df = pd.DataFrame([[4, 9]] * 3, columns=['A', 'B'])
print(df)

print('---------------------')
print(df.apply(np.sqrt))
print('---------------------')
print(df.apply(np.sum, axis=0))
print('---------------------')
print(df.apply(np.sum, axis=1))

# 输出
   A  B
0  4  9
1  4  9
2  4  9
---------------------
     A    B
0  2.0  3.0
1  2.0  3.0
2  2.0  3.0
---------------------
A    12
B    27
dtype: int64
---------------------
0    13
1    13
2    13
dtype: int64
```
```py
# 输入
import pandas as pd

# [[4, 9]] 表示嵌套列表，不是二维数组，因此不具备广播的特性
df = pd.DataFrame([[4, 9]] * 3, columns=['A', 'B'])
print(df)

print('---------------------')
print(df.apply(lambda x: [1, 2], axis=1))
print('---------------------')
print(df.apply(lambda x: [1, 2], axis=1, result_type='expand'))
print('---------------------')
print(df.apply(lambda x: [1, 2], axis=1, result_type='reduce'))
print('---------------------')
print(df.apply(lambda x: pd.Series([1, 2], index=['foo', 'bar']), axis=1))
print('---------------------')
print(df.apply(lambda x: [1, 2], axis=1, result_type='broadcast'))

# 输出
   A  B
0  4  9
1  4  9
2  4  9
---------------------
0    [1, 2]
1    [1, 2]
2    [1, 2]
dtype: object
---------------------
   0  1
0  1  2
1  1  2
2  1  2
---------------------
0    [1, 2]
1    [1, 2]
2    [1, 2]
dtype: object
---------------------
   foo  bar
0    1    2
1    1    2
2    1    2
---------------------
   A  B
0  1  2
1  1  2
2  1  2
```