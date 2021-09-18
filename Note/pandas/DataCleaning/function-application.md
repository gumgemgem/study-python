# 函数应用

### 1. apply()
- 描述  
沿着 DataFrame 的某一轴向应用函数  

  - 传递给该函数的对象是 Series 对象，对象的索引是 DataFrame 索引（当 axis=0）或DataFrame 的列（当 axis=1） 

  - 返回类型：当 result_type=None，最终的返回类型根据提供的函数方法的返回类型来推断的；否则，取决于 result_type 的参数  

- 语法  
`DataFrame.apply(func, axis=0, raw=False, result_type=None, args=(), **kwargs)`  

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