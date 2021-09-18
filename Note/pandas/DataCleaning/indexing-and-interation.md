# 索引和迭代数据

## 1. loc()
## 2. iloc()
## 3. head()
## 4. tail()

## 5. isin()

- 描述  
判断 DataFrame 中的每个元素是否包含在给定的 values 值中

- 语法  
`DataFrame.isin(values)`

|参数|说明|
|---|---|
|values|iterable, Series, DataFrame or dict<br>iterable -- 判断元素是否包含在可迭代对象中<br>Series -- 索引相同的位置元素是否相同<br>dict -- 键和列相同的位置元素是否相同<br>DataFrame -- 索引和列都相同的位置元素是否相同|

返回值：布尔值的 DataFrame


- 实例  
```py
# 输入
import pandas as pd

df = pd.DataFrame({'num_legs': [2, 4], 'num_wings': [2, 0]},
                  index=['falcon', 'dog'])
s = pd.Series([2, 0], index=['dog', 'cat'])
other = pd.DataFrame({'num_legs': [8, 2], 'num_wings': [0, 2]},
                     index=['spider', 'falcon'])

print(df)
print('*******************************')
print(df.isin([0, 2]))
print('*******************************')
print(df.isin(s))
print('*******************************')
print(df.isin({'num_wings': [0, 3]}))
print('*******************************')
print(df.isin(other))
print('*******************************')
print(df.num_legs.isin([2, 5]))

# 输出
        num_legs  num_wings
falcon         2          2
dog            4          0
*******************************
        num_legs  num_wings
falcon      True       True
dog        False       True
*******************************
        num_legs  num_wings
falcon     False      False
dog        False      False
*******************************
        num_legs  num_wings
falcon     False      False
dog        False       True
*******************************
        num_legs  num_wings
falcon      True       True
dog        False      False
*******************************
falcon     True
dog       False
Name: num_legs, dtype: bool
```