# 计算和描述性统计

## 1. Series.unique()

- 描述  
返回 Series 对象去重后的值  

- 语法  
`Series.unique()`  

返回值：返回一个 numpy 数组；去重后的数据将按照原始数据中的出现顺序排列  

- 实例  
```py
# 输入
import pandas as pd
import numpy as np

df = pd.DataFrame({'key1': ['a', 'c', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'data1': np.random.randn(5),
                   'data2': np.random.randn(5)})
print(df)
print(df.key1.unique())

# 输出
  key1 key2     data1     data2
0    a  one  0.419446  0.005400
1    c  two -0.291850  0.162656
2    b  one  0.438302  0.255220
3    b  two  1.240610  0.767071
4    a  one -1.503448 -1.420450
['a' 'c' 'b']
```

## 2. nunique()

- 描述  
返回指定轴上不同的元素数目  

- 语法  
`DataFrame.nunique(axis=0, dropna=True)`

|参数|说明|
|---|---|  
|axis|指定轴向，**默认** 为 0<br>0 / 'index'表示逐行<br>1 / 'columns'表示逐列|
|dropna|数目中是否忽略空值，**默认** 为 True|

返回值：返回 Series  

- 实例  
```py
# 输入
import pandas as pd
import numpy as np

df = pd.DataFrame({'key1': ['a', 'c', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'key3': ['A', np.nan, 'B', 'A', np.nan],
                   'data1': np.random.randn(5),
                   'data2': np.random.randn(5)})
print(df)
print('*************************************')
print(df.nunique())
print('*************************************')
print(df.nunique(axis=1))
print('*************************************')
print(df.nunique(dropna=False))

# 输出
  key1 key2 key3     data1     data2
0    a  one    A  0.343360 -0.525946
1    c  two  NaN -0.235533  1.257297
2    b  one    B -0.214568  0.783661
3    b  two    A -0.999865 -0.107285
4    a  one  NaN -1.150474  0.796357
*************************************
key1     3
key2     2
key3     2
data1    5
data2    5
dtype: int64
*************************************
0    5
1    4
2    5
3    5
4    4
dtype: int64
*************************************
key1     3
key2     2
key3     3
data1    5
data2    5
dtype: int64
```

