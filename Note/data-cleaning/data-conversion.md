# 数据转换

主要涉及到数据的删除、转换等

## 目录
- [1. 删除重复数据](#1-删除重复数据)  
  - [1.1 duplicated()](#11-duplicated)  
  - [1.2 drop_duplictates()](#12-drop_duplictates)  
- [2. 删除指定行或列数据](#2-删除指定行或列数据)  
  - [2.1 drop()](#21-drop)

## 1. 删除重复数据

### 1.1 duplicated()

- 说明  

判断数据中是否有重复的**行数据**（可以选择**指定的列序列**进行判断）  

- 语法  

`DataFrame.duplicated(subset=None, keep='first')`  

|参数|说明|
|---|---|
|subset|column label or sequence of labels, optional<br>指定需要判断重复数据的字段或字段的序列，**可选参数**（默认**所有列**）|
|keep|{'fisrt', 'last', False}, default 'fisrt'<br>指定哪些重复行需要标记（已知非重复行默认标记为 False）<br>'fisrt' -- 重复项都标记为 True，除了第一次出现的行（**默认**）<br>'last' -- 重复项都标记为 True，除了最后一次出现的行<br>False -- 所有重复项都标记为 True|

返回值：带有重复行标记的布尔类型的 Series  

- 示例  

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

- 扩展  

  - 保留非重复的数据（作用同**drop_duplicates()**）
  - 与`any()`结合判断数据中是否存在重复数据  
  - 与`sum()`结合得到重复数据行数  
  
  ```py
  # 输入
  import pandas as pd

  df = pd.DataFrame({'brand': ['Yum Yum', 'Yum Yum', 'Indomie', 'Indomie', 'Indomie'],
                     'style': ['cup', 'cup', 'cup', 'pack', 'pack'],
                     'rating': [4, 4, 3.5, 15, 5]})

  print(df)
  print('*********************************')
  print(df[~df.duplicated(subset='brand')])
  print(df.duplicated(subset='brand').any())
  print(df.duplicated(subset='brand').sum())

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
  True
  3
  ```

### 1.2 drop_duplictates()

- 说明  

删除数据中重复的**行数据**（可以选择**指定的列序列**进行判断数据是否重复）  

- 语法  

`DataFrame.drop_duplicates(subset=None, keep='first', inplace=False, ignore_index=False)`

|参数|说明|
|---|---|
|subset|column label or sequence of labels, optional<br>指定需要判断重复数据的字段或字段的序列，**可选参数**（默认**所有列**）|
|keep|{'fisrt', 'last', False}, default 'fisrt'<br>指定哪些重复行需要标记（已知非重复行默认标记为 False）<br>'fisrt' -- 重复项都标记为 True，除了第一次出现的行（**默认**）<br>'last' -- 重复项都标记为 True，除了最后一次出现的行<br>False -- 所有重复项都标记为 True|
|inplace|bool, default False<br>是否原地修改数据，否则返回一个副本（默认**False**）|
|ignore_index|bool, default False<br>是否重新排列返回结果的索引（默认**False**）|

返回值：返回删除重复数据后的 DataFrame（inplace=False）或 None（inplace=True）  

- 示例  

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

## 2. 删除指定行或列数据

### 2.1 drop()

- 说明  

通过指定标签名称（labels）和相应的轴（axis），或直接指定索引（index）或列名称（columns）来删除行或列  
使用多索引时，可以通过指定级别(level)来删除不同级别上的标签

- 语法  

`DataFrame.drop(labels=None, axis=0, index=None, columns=None, level=None, inplace=False, errors='raise')`  

|参数|说明|
|---|---|
|labels|single label or list-like<br>指定要删除的单个标签或标签类似列表（元组会被认为是单个标签而非标签序列）；常与 axis 参数结合使用|
|axis|{0 or 'index', 1 or 'columns'}, default 0<br>是否从索引（或 0）或列（或 1）中删除标签，**默认 0**|
|index|single label or list-like<br>指定索引上删除标签；即（labels, axis=0）等价于（index=labels）|
|columns|single label or list-like<br>指定列上删除标签；即（labels, axis=1）等价于（columns=labels）|
|level|int or level name, optional<br>对于组合索引，指定要删除索引的级别，可选参数|
|inplace|bool, default False<br>是否原地修改数据，否则返回一个副本（默认**False**）|
|errors|{'ignore', 'raise'}, default 'raise'<br>如果 'ignore'，则不显示错误，仅删除现有标签；**默认 'raise'**|

返回值：返回删除指定行或列数据后的 DataFrame（inplace=False）或 None（inplace=True）  

- 示例  

参考[官网示例](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop.html)
