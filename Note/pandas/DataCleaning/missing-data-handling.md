# 缺失数据处理

## 1. fillna()
- 描述  
使用指定的方法填充 Na/NaN 值

- 语法  
`DataFrame.fillna(value=None, method=None, axis=None, inplace=False, limit=None, downcast=None)`

|常用参数|说明|
|-----|-----|
|value|标量、字典、Series、DataFrame 类型；用于填充缺失值<br>或者指定为每个 index（对于 Series）或 columns（对于 DataFrame）使用字典/Series/DataFrame的值|
|method|{'backfill'/'bfill', 'pad'/'ffill', None（**默认**）}；<br>'backfill'/'bfill' -- 向后填充，使用下一个有效值来填充空白<br>'pad'/'ffill' -- 向前填充，使用最后一个有效值填充空白|
|axis|{0/‘index’, 1/‘columns’}；沿着指定轴向填充缺失值|
|limit|整型（**默认** None）；表示填充的最大数量|
|inplace|布尔类型（**默认** False）；当为 True 时，表示上述修改在原地进行，相应的视图也会进行修改|

返回值：  
返回 DataFrame 的对象，并不是原地进行修改  

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

## 2. replace()
- 描述  
替换 DataFrame 中指定的值  
该方法动态地为 DataFrame 替换值，与`.loc`和`.iloc`的更新方式不同，该方法不需要指定要更新值的位置  

- 语法  
`DataFrame.replace(to_replace=None, value=None, inplace=False, limit=None, regex=False, method='pad')`

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