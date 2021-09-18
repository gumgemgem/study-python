# Group by: split-apply-combine

- **Spliting** the data into groups based on some criteria  
- **Applying** a function to each group independently  
- **Combining** the results into a data stucture  

## 1. 分组键类型

1. 列表或数组，其元素个数与待分组的轴数目必须一样  
2. 表示 DataFrame 某个列名或索引名  
`df.groupby('A')` 是 `df.groupby(df['A'])`的 **语法糖**（Syntactic sugar）：简化表达方式  
**注意**：如果前面不是 df，而是 df 的某一部分且不包含列 'A'，则不可以使用语法糖的方式  
**例如**：`df['B', 'C'].groupby(df['A'])`
3. 字典或 Series，给出待分组轴上的值与分组名之间的对应关系  
4. 函数，用于处理轴索引的各个标签  
5. 上述类别任意组合的列表  

