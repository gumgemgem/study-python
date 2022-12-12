# 合并数据

## 1. merge() 

- 描述

`merge()`主要是通过数据库样式的连接合并**两个** DataFrame 或者已命名的 Series  

  1. 类似于数据库的 Join 操作
  2. 只能用于**两张**表**横向**上的合并
  3. pandas 中主要存在两种形式：`pandas.merge()` 和 `pandas.DataFrame.merge()`；两种形式其实是一样的，此处只介绍第一种  

- 语法

```
pandas.merge(left, right, how='inner', on=None, left_on=None, right_on=None, left_index=False, right_index=False,  
             sort=False, suffixes=('_x', '_y'), copy=True, indicator=False, validate=None)
```

|常用参数|说明|
|:---|:---|
|left|DataFrame<br>连接的主表|
|right|DataFrame or named Series<br>被连接的表（DataFrame or 已命名的 Series）|
|how|{'left', 'right', 'outer', 'inner', 'cross'}, default 'inner'<br>'left' -- 类似于 SQL left outer join<br>'right' -- 类似于 SQL right outer join<br>'outer' -- 类似于 SQL full outer join<br>'inner' -- 类似于 SQL inner join<br>'cross' -- 创建笛卡尔积，并且保留左键的顺序；因为是笛卡尔积，所以不需要指定列或索引进行连接|
|on|label or list<br>连接两表的列名或索引级别名称，必须同时出现在两张表中；<br>如果 on=None 且 right_index=False, left_index=False，则两张表列的交集作为连接键|
|left_on|label or list, or array-like<br>左侧 DataFrame 中的列名或索引级别作用键|
|right_on|label or list, or array-like<br>右侧 DataFrame 中的列名或索引级别作用键|
|left_index|bool, default False<br>如果为 True，则使用左侧 DataFrame 中的索引（行标签）作为其连接键；<br>对于多层索引的左侧 DataFrame，索引级别数必须与右侧 DataFrame 中的连接键数（多层索引 or 多列）相匹配|
|right_index|bool, default False<br>如果为 True，则使用右侧 DataFrame 中的索引（行标签）作为其连接键；<br>对于多层索引的右侧 DataFrame，索引级别数必须与左侧 DataFrame 中的连接键数（多层索引 or 多列）相匹配|
|sort|bool, default False<br>按照字典顺序通过连接键对结果 DataFrame 进行排序；默认 False 会提高性能|
|suffixes|list-like, default is ('\_x', '\_y')<br>用于区分非连接键的重叠列名，为重叠列名添加字符串后缀以区分|

- 实例

[1. 参考官网示例](https://pandas.pydata.org/docs/reference/api/pandas.merge.html?highlight=pandas%20merge#pandas.merge)  
[2. 参考其它示例](https://blog.csdn.net/brucewong0516/article/details/82707492)

## 2. join()

- 描述  

`join()`

- 语法  


- 实例  
