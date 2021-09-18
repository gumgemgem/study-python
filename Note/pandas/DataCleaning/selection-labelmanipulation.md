# 数据选择、标签操作

# 1. duplicated()

- 描述  
判断数据中是否有重复的行数据；可以选择指定的列序列进行判断  
**作用** ：可以查看重复项数据

- 语法  
`DataFrame.duplicated(subset=None, keep='first')`

|参数|说明|
|---|---|
|subset|是否需要选取列的子集（**默认** 所有列）；column label or sequence of labels, optional|
|keep|如果存在重复行，重复行的标记方式（**默认** 'first'）；{'first', 'last', False}<br>**注意** ：所有非重复项都标为 False<br>'first' -- 重复项中第一次出现的行标为 False，其余重复项都是 True<br>'last' -- 重复项中最后一次出现的行标为 False，其余重复项都是 True<br>False -- 将所有重复项标为 True|

返回值：布尔值的 Series

- 实例  
```py
# 输入
import pandas as pd

df = pd.DataFrame({'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
                   'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
                   'rating': [4, 4, 3.5, 15, 5]})

print(df)
print('*********************************')
print(df.duplicated())
print('*********************************')
print(df.duplicated(keep='last'))
print('*********************************')
print(df.duplicated(keep=False))
print('*********************************')
print(df.duplicated(subset='brand'))

# 输出
     brand style  rating
0  Yum Yum   cup     4.0
1  Yum Yum   cup     4.0
2  Indomie   cup     3.5
3  Indomie  pack    15.0
4  Indomie  pack     5.0
*********************************
0    False
1     True
2    False
3    False
4    False
dtype: bool
*********************************
0     True
1    False
2    False
3    False
4    False
dtype: bool
*********************************
0     True
1     True
2    False
3    False
4    False
dtype: bool
*********************************
0    False
1     True
2    False
3     True
4     True
dtype: bool
```

## 2. drop_diplicates()

- 描述  
删除数据中重复的行数据；可以选择指定的列序列进行操作  
**作用** ：可以删除重复项数据

- 语法  
`DataFrame.drop_duplicates(subset=None, keep='first', inplace=False, ignore_index=False)`

|参数|说明|
|---|---|
|subset|是否需要选取列的子集（**默认** 所有列）；column label or sequence of labels, optional|
|keep|如果存在重复行，重复行的标记方式（**默认** 'first'）；{'first', 'last', False}<br>'first' -- 保留重复项中第一次出现的数据，其余重复项都删除<br>'last' --  保留重复项中最后一次出现的数据，其余重复项都删除<br>False -- 将所有重复项都删除|
|inplace|是否原地修改数据，否则返回一个副本（**默认** False）；bool|
|ignore_index|是否重新排列返回的结果索引（**默认** False）；bool|

返回值：布尔类型的 DataFrame（inplace=False）或 None（inplace=True）  

- 实例  
```py
# 输入
import pandas as pd

df = pd.DataFrame({'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
                   'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
                   'rating': [4, 4, 3.5, 15, 5]})

print(df)
print('*********************************')
print(df.drop_duplicates())
print('*********************************')
print(df.drop_duplicates(subset='brand', keep='last'))
print('*********************************')
print(df.drop_duplicates(ignore_index=True))
print('*********************************')
print(df.drop_duplicates(inplace=True))
print(df)

# 输出
     brand style  rating
0  Yum Yum   cup     4.0
1  Yum Yum   cup     4.0
2  Indomie   cup     3.5
3  Indomie  pack    15.0
4  Indomie  pack     5.0
*********************************
     brand style  rating
0  Yum Yum   cup     4.0
2  Indomie   cup     3.5
3  Indomie  pack    15.0
4  Indomie  pack     5.0
*********************************
     brand style  rating
1  Yum Yum   cup     4.0
4  Indomie  pack     5.0
*********************************
     brand style  rating
0  Yum Yum   cup     4.0
1  Indomie   cup     3.5
2  Indomie  pack    15.0
3  Indomie  pack     5.0
*********************************
None
     brand style  rating
0  Yum Yum   cup     4.0
2  Indomie   cup     3.5
3  Indomie  pack    15.0
4  Indomie  pack     5.0
```