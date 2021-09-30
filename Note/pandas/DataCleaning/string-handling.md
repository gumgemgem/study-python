# string 类型操作

## 1. Series.str.lower()

- 描述  
将 Series 中的 string 类型转换为小写  

- 语法  
`Series.str.lower()`

- 实例  
```py
# 输入
import pandas as pd
import numpy as np

df = pd.DataFrame({'key1': ['a', 'c', 'b', 'b', 'a'],
                   'key2': ['one', 'two', 'one', 'two', 'one'],
                   'key3': ['A', np.nan, 'B', 'A', np.nan]})
print(df)
print('*************************************')
print(df.key3.str.lower())

# 输出
  key1 key2 key3
0    a  one    A
1    c  two  NaN
2    b  one    B
3    b  two    A
4    a  one  NaN
*************************************
0      a
1    NaN
2      b
3      a
4    NaN
```

## 2. Series.str.upper()
## 3. index.str.lower()
## 4. index



.str.upper()