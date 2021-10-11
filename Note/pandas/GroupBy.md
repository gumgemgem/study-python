# Group by: split-apply-combine

- **Spliting** the data into groups based on some criteria  
- **Applying** a function to each group independently  
- **Combining** the results into a data stucture  

语法：  
`DataFrame/Series.groupby(by=None, axis=0, level=None, as_index=True, sort=True, group_keys=True, squeeze=NoDefault.no_default, observed=False, dropna=True)`

|常用参数|说明|
|:---|:---|
|by|mapping, function, label, or list of labels<br>用于确定分组键|
|axis|0 or 'index', 1 or 'columns', default 0<br>沿何轴向进行分组|
|level|int, level name, or sequence of such, default None<br>如果是组合索引（分层索引），可以按照指定 level 进行分组|
|dropna|bool, default True<br>如果为真，且分组键中存在 NA 值，NA 值和该值所在的行/列都将被舍弃；否则保留|

## 1. 分组键类型

1. 列表或数组，其元素个数与待分组的索引轴数目必须一样  
2. 表示 DataFrame 某个列名或索引名  
3. 字典或 Series，给出待分组轴上的名字与分组名之间的对应关系 [【详情见第 5 点】](#5-分组键是字典或-Series)  
4. 函数，在索引或列标签上进行调用 [【详情见第 6 点】](#6-分组键是函数)    
5. 上述类别任意组合的列表  

说明：  
`df.groupby('A')` 是 `df.groupby(df['A'])`的 **语法糖**（Syntactic sugar）：简化表达方式  

- 如果前面不是 df，而是 df 的某一部分且不包含列 'A'，则不可以使用语法糖的方式  
`df[['B', 'C']].groupby(df['A'])`
- 如果前面是 df 的某一列，不论是否包含列 'A'，都不可以使用语法糖的方式  
`df['A'].groupby(df['A'])`  

实例：  
```py
import numpy as np
import pandas as pd

df = pd.DataFrame({'key1': ['a', 'a', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': [1, 2, 3, 4, 5],
                   'data2': [10, 20, 30, 40, 50]})
grouped1 = df.groupby([1, 1, 2, 2, 2])             # 分组键是列表
grouped2 = df.groupby(np.array([1, 1, 2, 2, 2]))   # 分组键是数组
grouped3 = df.groupby('key1')                      # 分组键是列名
grouped4 = df.groupby(df['key1'])                  # 分组键是 Series
grouped5 = df.groupby({'key1': 1, 'key2': 2, 'data1': 1, 'data2': 2}, axis=1)   # 分组键是字典
```

## 2. 对分组结果进行迭代
1. 分组得到的是 GroupBy 对象，该对象支持迭代，迭代产生一组二元数组（分别是分组键和数据块） 

- 分组键是唯一的，二元数组的第一个元素是分组键名  
`for name, group in df.groupby('key1')`
- 分组键是多重的，二元数组的第一个元素是分组键值组成的元组  
`for name, group in df.groupby(['key1', 'key2'])` -- name 是分组键组成的元组  
`for (k1, k2), group in df.groupby(['key1', 'key2'])` -- (k1, k2) 是分组键组成的元组  

实例：  
```py
# 输入
import pandas as pd

df = pd.DataFrame({'key1': ['a', 'a', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': [1, 2, 3, 4, 5],
                   'data2': [1, 20, 30, 40, 50]})
for name, group in df.groupby('key1'):
    print(name)
    print(group)

print('*************************')
for (k1, k2), group in df.groupby(['key1', 'key2']):
    print((k1, k2))
    print(group)
    
print('*************************')
for key, group in df.groupby(['key1', 'key2']):
    print(key)
    print(group)

# 输出
a
  key1 key2  data1  data2
0    a  one      1      1
1    a  two      2     20
4    a  one      5     50
b
  key1 key2  data1  data2
2    b  one      3     30
3    b  two      4     40
*************************
('a', 'one')
  key1 key2  data1  data2
0    a  one      1      1
4    a  one      5     50
('a', 'two')
  key1 key2  data1  data2
1    a  two      2     20
('b', 'one')
  key1 key2  data1  data2
2    b  one      3     30
('b', 'two')
  key1 key2  data1  data2
3    b  two      4     40
*************************
('a', 'one')
  key1 key2  data1  data2
0    a  one      1      1
4    a  one      5     50
('a', 'two')
  key1 key2  data1  data2
1    a  two      2     20
('b', 'one')
  key1 key2  data1  data2
2    b  one      3     30
('b', 'two')
  key1 key2  data1  data2
3    b  two      4     40
```

2. 可以将分组后的对象打包成字典（`{分组键: 数据块}`）或二元数组组成的列表（`[(分组键, 数据块)]`）  

实例：  
```py
# 输入
import pandas as pd

df = pd.DataFrame({'key1': ['a', 'a', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': [1, 2, 3, 4, 5],
                   'data2': [1, 20, 30, 40, 50]})
l = list(df.groupby('key1'))
d = dict(list(df.groupby('key1')))
print(l)
print('*********************************')
print(d)

# 输出
[('a',   key1 key2  data1  data2
0    a  one      1      1
1    a  two      2     20
4    a  one      5     50), ('b',   key1 key2  data1  data2
2    b  one      3     30
3    b  two      4     40)]
*********************************
{'a':   key1 key2  data1  data2
0    a  one      1      1
1    a  two      2     20
4    a  one      5     50, 'b':   key1 key2  data1  data2
2    b  one      3     30
3    b  two      4     40}
```

## 3. 不同维度的分组
默认情况下，groupby 是按照行变化的方向（axis=0）进行分组的，同样也可以按照列（axis=1）进行分组  

实例：
```py
# 输入
import pandas as pd

df = pd.DataFrame({'key1': ['a', 'a', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': [1, 2, 3, 4, 5],
                   'data2': [1, 20, 30, 40, 50]})
print(df.dtypes)
print('************************')
for dtype, group in df.groupby(df.dtypes, axis=1):
    print(dtype)
    print(group)

# 输出
key1     object
key2     object
data1     int64
data2     int64
dtype: object
************************
int64
   data1  data2
0      1      1
1      2     20
2      3     30
3      4     40
4      5     50
object
  key1 key2
0    a  one
1    a  two
2    b  one
3    b  two
4    a  one
```

## 4. 选取一列或列的子集
**先分组再取列或列的子集** 实际上是 **先取列或列的子集再进行分组** 的语法糖  
`df.groupby('key1')['data1']`、`df.groupby('key1')[['data1']]` 实际上是  
`df['data1'].groupby('key1')`、`df[['data1']].groupby('key1')[['data1']]`的语法糖

实例：  
```py
# 输入
import pandas as pd

df = pd.DataFrame({'key1': ['a', 'a', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': [1, 2, 3, 4, 5],
                   'data2': [1, 20, 30, 40, 50]})
print(df.groupby('key1')['data1'].mean())   # 返回的是 Series 类型
print('**************************')
print(df.groupby('key1')[['data1']].mean())   # 返回的是 DataFrame 类型

# 输出
key1
a    2.666667
b    3.500000
Name: data1, dtype: float64
**************************
         data1
key1          
a     2.666667
b     3.500000
```

## 5. 分组键是字典或 Series
当字典或 Series 中存在 DataFrame 中没有的元素（未分组键）时也是可以的

实例：  
```py
# 输入
import numpy as np
import pandas as pd 

mapping = {'a': 'red', 'b': 'red', 'c': 'blue', 'd': 'blue', 'e': 'red', 'f': 'other'}   # f 是未分组键
map_series = pd.Series(mapping)
df = pd.DataFrame(np.random.randn(5, 5),
                  columns=['a', 'b', 'c', 'd', 'e'],
                  index=['Joe', 'Steve', 'Wes', 'Jim', 'Travis'])
df.iloc[2:3, [1, 2]] = np.nan
print(df)
print('***************************************')
print(df.groupby(mapping, axis=1).count())   # 字典作为分组键
print(df.groupby(map_series, axis=1).count())   # Series 作为分组键

# 输出
               a         b         c         d         e
Joe    -1.223154 -0.594024 -0.002612  0.706028 -0.207485
Steve   1.661293 -0.938452 -0.728948 -1.714422 -1.384233
Wes     0.647308       NaN       NaN  0.694095  1.578946
Jim    -0.766099  0.070814  0.693425  0.838504 -0.499822
Travis -0.522405 -0.963755 -1.437092  1.386050 -0.271177
***************************************
        blue  red
Joe        2    3
Steve      2    3
Wes        1    2
Jim        2    3
Travis     2    3
        blue  red
Joe        2    3
Steve      2    3
Wes        1    2
Jim        2    3
Travis     2    3
```

## 6. 分组键是函数
函数会作用在指定的轴向（索引或列）上，作用后函数的返回值就是分组的名称  

实例：  
```py
# 输入
import numpy as np
import pandas as pd 

df = pd.DataFrame(np.random.randn(5, 5),
                  columns=['a', 'b', 'c', 'd', 'e'],
                  index=['Joe', 'Steve', 'Wes', 'Jim', 'Travis'])
df.iloc[2:3, [1, 2]] = np.nan
print(df)
print('***************************************')
print(df.groupby(len).count())   # len() 函数作用在索引轴向上计算人名的字符长度，返回的长度进行分组

# 输出
               a         b         c         d         e
Joe     0.145989 -1.585637 -0.210805  0.485398  1.254857
Steve   0.679129 -0.247332  0.855666  0.766833  1.153250
Wes     1.643675       NaN       NaN  0.096284 -0.984045
Jim    -0.464697 -0.084404 -0.116382  1.753380  1.501150
Travis -0.072660 -0.862315 -0.595634  0.842520  0.500667
***************************************
   a  b  c  d  e
3  3  2  2  3  3
5  1  1  1  1  1
6  1  1  1  1  1
```

## 7. 组合索引按级别分组
ToDo:  
1. 组合索引的定义  
2. 组合索引按级别分组可以传递序号或是索引名  
3. 组合索引也可以按照多重级别进行分组 【见官网示例，Group By】