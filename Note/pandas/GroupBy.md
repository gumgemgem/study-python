# Group by: split-apply-combine

- **Spliting** the data into groups based on some criteria  
- **Applying** a function to each group independently  
- **Combining** the results into a data stucture  

## 1. 分组键类型

1. 列表或数组，其元素个数与待分组的索引轴数目必须一样  
2. 表示 DataFrame 某个列名或索引名  
3. 字典或 Series，给出待分组轴上的名字与分组名之间的对应关系  
4. 函数，在轴标签上进行调用  
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
grouped1 = df.groupby([1, 1, 2, 2, 2])   # 分组键是列表
grouped2 = df.groupby(np.array([1, 1, 2, 2, 2]))   # 分组键是数组
grouped3 = df.groupby('key1')   # 分组键是列名
grouped4 = df.groupby(df['key1'])   # 分组键是 Series
```

## 2. 对分组结果进行迭代
分组得到的是 GroupBy 对象，该对象支持迭代，迭代产生一组二元数组（分别是分组名和数据块） 

- 分组键是唯一的，二元数组的第一个元素是分组键名  
`for name, group in df.groupby`
- 分组键是多重的，二元数组的第一个元素是分组键值组成的元组  