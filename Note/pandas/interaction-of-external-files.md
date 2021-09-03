# pandas 与外部文件之间的交互作用

## 1、从外部文件中读取数据

### 1.1 从 CSV 文件中读取数据至 DataFrame
- 语法  
```py
pd.read_csv([参数列表])
```

|常用参数|说明|
|---|----|
|filepath_or_buffer|读取文件的路径或 URL（必须带主机）或可以实现 read 方法的任意对象|
|sep|分隔符（**默认**为 ','）|
|header|指定表头所在的行（**默认**为 infer）；整数或整数列表（从 0 开始）|
|names|设置导入数据的列名称（**默认**为 None）；类数组类型|
|index_col|指定某列或多列为索引，（**默认**为 None）；整数、字符串、整数或字符串的序列、False<br>PS：整数指的是列所在的整数索引|
|usecols|指定读取特定列；整数、字符串的列表类型|
|dtype|指定列的数据类型；e.g. `dtype={'col1':str}`|

**header 和 names 用法说明**：  

1. csv 文件中有表头并且是第一行；header 和 names 均不用指定  
2. csv 文件中有表头但不是第一行；可以通过 header 参数进行表头指定  
3. csv 文件中是纯数据，无表头；可以通过 names 参数设置表头名称  
4. csv 文件中存在表头，但希望更改表头的名字；可以通过 header 参数选出参数所在行，再通过 names 参数指定新的表头，此时新的表头将会替代原本的表头，等价与将表头 rename  

- 实例  
```py
# 输入

import pandas as pd 

df1 = pd.read_csv('../study_file/student.csv')
df2 = pd.read_csv('../study_file/student.csv', dtype={'id': str})
df3 = pd.read_csv('../study_file/student.csv', dtype={'id': str},
                  names=['编号', '名字', '性别', '数学', '语文', '英语'])
df4 = pd.read_csv('../study_file/student.csv', dtype={'id': str}, header=0,
                  names=['编号', '名字', '性别', '数学', '语文', '英语'])
df5 = pd.read_csv('../study_file/student.csv', dtype={'id': str},
                  usecols=[0, 1, 3])

print(df1)
print('------------------------------------')
print(df2)
print('------------------------------------')
print(df3)
print('------------------------------------')
print(df4)
print('------------------------------------')
print(df5)

# 输出
   id name gender  math  Chinese  English
0   1   张三      男    60       89       97
1   2   王红      女    69       87       76
2   3   李四      男    78       90       95
3   4   赵云      男    90       98       97
4   5   李丽      女    98      100       87
------------------------------------
    id name gender  math  Chinese  English
0  001   张三      男    60       89       97
1  002   王红      女    69       87       76
2  003   李四      男    78       90       95
3  004   赵云      男    90       98       97
4  005   李丽      女    98      100       87
------------------------------------
    编号    名字      性别    数学       语文       英语
0   id  name  gender  math  Chinese  English
1  001    张三       男    60       89       97
2  002    王红       女    69       87       76
3  003    李四       男    78       90       95
4  004    赵云       男    90       98       97
5  005    李丽       女    98      100       87
------------------------------------
   编号  名字 性别  数学   语文  英语
0   1  张三  男  60   89  97
1   2  王红  女  69   87  76
2   3  李四  男  78   90  95
3   4  赵云  男  90   98  97
4   5  李丽  女  98  100  87
------------------------------------
    id name  math
0  001   张三    60
1  002   王红    69
2  003   李四    78
3  004   赵云    90
4  005   李丽    98
```

### 1.2 从 Excel 文件中读取数据至 DataFrame
- 语法  
```py
pd.read_excel([参数列表])
```

|常用参数|说明|
|---|---|
|io|读取文件的路径或 URL（必须带主机）或可以实现 read 方法的任意对象|
|sheet_name|读取 Excel 中的指定表单（**默认**为 0）； 字符、整型、列表或None<br>字符：'Sheet1' -- 取 Sheet1 的数据<br>整型：n -- 取第 n + 1 张表单的数据<br>列表：取几张表单的数据生成一个 DataFrame<br>None：Excel 中的所有表单|
|header|指定表头行号（**默认**为 0）；整型或整型列表，没有表头请使用 None|
|names|设置导入数据的列名（**默认**为 None）；类数组类型|
|index_col|指定索引列号（**默认**为 None）；整型或者整型列表，没有列索引请使用 None<br>**注意**：如果使用了 usecols 作为子集，那么 index_col 基于该子集|
|usecols|有选择地读取某些列（**默认**为 None）；整型、字符、列表、None<br>None：读取所有列<br>整型：从 0 开始的指定列<br>字符：根据指定列读取列 e.g. 'A:E' 或 'A, C, E :G' 或 'id'<br>字符或整型的列表：指定读取多个列|
|dtype|指定待读取数据的类型（**默认**为 None）；字典、None，e.g. {'a': str}<br>**注意**：如果指定了 converters 参数，则 dtype 参数将无效|

- 实例  
```py
# 输入

import pandas as pd

df1 = pd.read_excel('../study_file/student.xlsx')
df2 = pd.read_excel('../study_file/student.xlsx', sheet_name='Sheet2')
df3 = pd.read_excel('../study_file/student.xlsx', header=0)
df4 = pd.read_excel('../study_file/student.xlsx', header=None)
df5 = pd.read_excel('../study_file/student.xlsx',
                    names=['编号', '名字', '性别', '数学', '语文', '英语'])
df6 = pd.read_excel('../study_file/student.xlsx', header=0,
                    names=['编号', '名字', '性别', '数学', '语文', '英语'])
df7 = pd.read_excel('../study_file/student.xlsx', index_col=0)
df8 = pd.read_excel('../study_file/student.xlsx', index_col=0,
                    usecols=['name', 'gender', 'math'])
df9 = pd.read_excel('../study_file/student.xlsx', index_col=[0, 1])

print(df1)
print('------------------------------------')
print(df2)
print('------------------------------------')
print(df3)
print('------------------------------------')
print(df4)
print('------------------------------------')
print(df5)
print('------------------------------------')
print(df6)
print('------------------------------------')
print(df7)
print('------------------------------------')
print(df8)
print('------------------------------------')
print(df9)

# 输出
   id name gender  math  Chinese  English
0   1   张三      男   NaN     89.0       97
1   2   王红      女  69.0     87.0       76
2   3   李四      男  78.0     90.0       95
3   4   赵云      男  90.0      NaN       97
4   5   李丽      女  98.0    100.0       87
------------------------------------
Empty DataFrame
Columns: []
Index: []
------------------------------------
   id name gender  math  Chinese  English
0   1   张三      男   NaN     89.0       97
1   2   王红      女  69.0     87.0       76
2   3   李四      男  78.0     90.0       95
3   4   赵云      男  90.0      NaN       97
4   5   李丽      女  98.0    100.0       87
------------------------------------
    0     1       2     3        4        5
0  id  name  gender  math  Chinese  English
1   1    张三       男   NaN       89       97
2   2    王红       女    69       87       76
3   3    李四       男    78       90       95
4   4    赵云       男    90      NaN       97
5   5    李丽       女    98      100       87
------------------------------------
   编号  名字 性别    数学     语文  英语
0   1  张三  男   NaN   89.0  97
1   2  王红  女  69.0   87.0  76
2   3  李四  男  78.0   90.0  95
3   4  赵云  男  90.0    NaN  97
4   5  李丽  女  98.0  100.0  87
------------------------------------
   编号  名字 性别    数学     语文  英语
0   1  张三  男   NaN   89.0  97
1   2  王红  女  69.0   87.0  76
2   3  李四  男  78.0   90.0  95
3   4  赵云  男  90.0    NaN  97
4   5  李丽  女  98.0  100.0  87
------------------------------------
   name gender  math  Chinese  English
id                                    
1    张三      男   NaN     89.0       97
2    王红      女  69.0     87.0       76
3    李四      男  78.0     90.0       95
4    赵云      男  90.0      NaN       97
5    李丽      女  98.0    100.0       87
------------------------------------
     gender  math
name             
张三        男   NaN
王红        女  69.0
李四        男  78.0
赵云        男  90.0
李丽        女  98.0
------------------------------------
        gender  math  Chinese  English
id name                               
1  张三        男   NaN     89.0       97
2  王红        女  69.0     87.0       76
3  李四        男  78.0     90.0       95
4  赵云        男  90.0      NaN       97
5  李丽        女  98.0    100.0       87
```

## 2、将数据写至文件中

### 2.1 数据写至 CSV 文件
- 语法  
```py
DataFrame.to_csv([参数列表])
```

|常用参数|说明|
|---|---|
|path_or_buf|文件路径或写文件对象（**默认**为 None，则返回字符串）|
|sep|输出文件的分隔符（**默认**为 ','）|
|na_rep|缺失数据填充（**默认**为 ''）|
|columns|指定写入文件的列字段序列|
|header|写入文件的列名（**默认**为 True）；布尔、字符类型的列表<br>**注意**：如果给定了字符串列表，则假定它是字符串的别名|
|index|写入文件时是否将行索引写至文件中（**默认**为 True）；布尔类型|

- 实例  
```py
# 输入

import pandas as pd

df = pd.read_csv('../study_file/student.csv')
df.to_csv('../study_file/1.csv', sep=' ')
df.to_csv('../study_file/2.csv', na_rep=60)
df.to_csv('../study_file/3.csv', columns=['id', 'name', 'math'])
df.to_csv('../study_file/4.csv', header=False)
df.to_csv('../study_file/5.csv',
          header=['编号', '名字', '性别', '数学', '语文', '英语'])
df.to_csv('../study_file/6.csv', index=False)
```

### 2.2 数据写至 Excel 文件
- 语法
```py
DataFrame.to_excel([参数列表])
```

|常用参数|说明|
|---|---|
|excel_writer|Excel 文件路径或可写的 Excel 文件对象|
|sheet_name|指定文件写入 Excel 文件的哪个表单（**默认**为 'Sheet1'）；字符类型|
|na_rep|缺失数据填充（**默认**为 ''）|
|float_format|浮点数的保留位数；e.g. `float_format='%.2f'`表示保留小数点后两位|
|columns|指定写入文件的列；序列、列表、字符类型|
|header|写入文件的列名（**默认**为 True）；布尔、字符类型的列表<br>**注意**：如果给定了字符串列表，则假定它是字符串的别名|
|index|写入文件时是否将行索引写进文件中（**默认**为 True）；布尔类型|

- 实例
```py
# 输入

import pandas as pd

df = pd.read_excel('../study_file/student.xlsx')
df.to_excel('../study_file/1.xlsx', sheet_name='Sheet2')
df.to_excel('../study_file/2.xlsx', na_rep=60)
df.to_excel('../study_file/3.xlsx', columns=['id', 'name', 'math'])
df.to_excel('../study_file/4.xlsx', header=False)
df.to_excel('../study_file/5.xlsx',
            header=['编号', '名字', '性别', '数学', '语文', '英语'])
df.to_excel('../study_file/6.xlsx', index=True)
df.to_excel('../study_file/7.xlsx', float_format='%.2f')
```