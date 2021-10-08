# string 类型操作

## 1. Series.str.lower()
## 2. Series.str.upper()
## 3. index.str.lower() / columns.str.lower()
## 4. index.str.upper() / columns.str.upper()

- 描述  
`Series.str.lower()` 将 Series 中的 string 类型转换为小写  
**注意**:  
有返回值，不是在原地进行大小写转换

- 语法  
`Series.str.lower()`  

返回值：  
返回大小写转换后的 Series 或 index，不是在原地修改

- 实例  
```py
# 输入
import pandas as pd
import numpy as np

df = pd.DataFrame({'Key1': ['a', 'c', 'b', 'b', 'a'],
                   'Key2': ['one', 'two', 'one', 'two', 'one'],
                   'Key3': ['A', np.nan, 'B', 'A', np.nan]})
print(df)
print('*************************************')
print(df.Key3.str.lower())
print('*************************************')
print(df.columns.str.lower())
print('*************************************')
print(df)
print('*************************************')
df.columns = df.columns.str.lower()
print(df)

# 输出
  Key1 Key2 Key3
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
Name: Key3, dtype: object
*************************************
Index(['key1', 'key2', 'key3'], dtype='object')
*************************************
  Key1 Key2 Key3
0    a  one    A
1    c  two  NaN
2    b  one    B
3    b  two    A
4    a  one  NaN
*************************************
  key1 key2 key3
0    a  one    A
1    c  two  NaN
2    b  one    B
3    b  two    A
4    a  one  NaN
```