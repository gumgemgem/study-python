# 改变形状、排序、转置

## 1. stack()

- 描述  
堆叠，将列旋转到索引

- 语法  
`DataFrame.stack(level=-1, dropna=True)`

|参数|说明|
|---|---|
|level|从列堆叠到索引轴上的标签（**默认** 为 -1）；整形、字符型、列表<br>-1：将最内层的列堆叠至索引轴<br>n：从 0 开始由外至内递增的顺序，将列 n 进行堆叠|
|dropna|是否删除全是缺失值的结果行（**默认** 为 True）；bool|

**注意** ：当列是单层时，进行 stack() 操作，会将单层列堆叠至索引上并返回一个 Series  

返回值：Series 或 DataFrame  

- 实例  
```py
# 输入
import pandas as pd

multicol = pd.MultiIndex.from_tuples([('weight', 'kg'),
                                      ('height', 'm')],
                                     name=['property', 'unit'])
df = pd.DataFrame([[None, 2], [3, 4]],
                  index=pd.Index(['cat', 'dog'], name='animal'),
                  columns=multicol)
print(df)
print('********************************')
print(df.stack())
print('********************************')
print(df.stack(1))
print('********************************')
print(df.stack(['property']))
print('********************************')
print(df.stack([0, 1]))
print('********************************')
df1 = df.stack()
print(df1.stack())

# 输出
property weight height
unit         kg      m
animal                
cat         NaN      2
dog         3.0      4
********************************
property     height  weight
animal unit                
cat    m        2.0     NaN
dog    kg       NaN     3.0
       m        4.0     NaN
********************************
property     height  weight
animal unit                
cat    m        2.0     NaN
dog    kg       NaN     3.0
       m        4.0     NaN
********************************
unit              kg    m
animal property          
cat    height    NaN  2.0
dog    height    NaN  4.0
       weight    3.0  NaN
********************************
animal  property  unit
cat     height    m       2.0
dog     height    m       4.0
        weight    kg      3.0
dtype: float64
********************************
animal  unit  property
cat     m     height      2.0
dog     kg    weight      3.0
        m     height      4.0
dtype: float64
```

## 2. unstack()

- 描述  
stack() 的反操作，将索引旋转到列

- 语法  
`DataFrame.unstack(level=-1, fill_value=None)`

|参数|说明|
|---|---|
|level|从索引堆叠到列上的标签（**默认** 为 -1）；整形、字符型、列表<br>-1：将最内层的索引堆叠至列<br>n：从 0 开始由外至内递增的顺序，将列 n 进行堆叠|
|fill_value|填补缺失值（**默认** 为 None）；int、str、dict|

**注意** ：当索引只有单层时，进行 unstack() 操作，并返回的是将堆叠后的列转化为索引的 Series  

返回值：Series 或 DataFrame  

- 实例
```py
# 输入
import pandas as pd
import numpy as np

index = pd.MultiIndex.from_tuples([('one', 'first', 'a'), ('one', 'first', 'b'),
                                   ('two', 'second', 'a'), ('two', 'second', 'b')])
s = pd.Series(np.arange(1.0, 5.0), index=index)

print(s)
print('*******************************')
print(s.unstack())
print('*******************************')
print(s.unstack(0))
print('*******************************')
df = s.unstack(0)
print(df.unstack())
print('*******************************')
print((df.unstack()).unstack())

# 输出
one  first   a    1.0
             b    2.0
two  second  a    3.0
             b    4.0
dtype: float64
*******************************
              a    b
one first   1.0  2.0
two second  3.0  4.0
*******************************
          one  two
first  a  1.0  NaN
       b  2.0  NaN
second a  NaN  3.0
       b  NaN  4.0
*******************************
        one       two     
          a    b    a    b
first   1.0  2.0  NaN  NaN
second  NaN  NaN  3.0  4.0
*******************************
one  a  first     1.0
        second    NaN
     b  first     2.0
        second    NaN
two  a  first     NaN
        second    3.0
     b  first     NaN
        second    4.0
dtype: float64
```