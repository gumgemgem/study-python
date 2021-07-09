# Series 和 DataFrame 的基本操作

## 索引

### 索引对象

pandas 的索引对象可以管理轴标签和其它元数据（比如轴标签等）  
语法：  
```py
obj.index
```

- 索引对象可以进行切片  
  索引对象只有整数切片的方式，且是左开右闭的区间；不能进行标签切片  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  index = df.index
  print(index)
  print(index[1:4])

  # 输出
  Index(['one', 'two', 'three', 'four', 'five', 'six'], dtype='object')
  Index(['two', 'three', 'four'], dtype='object')
  ```

- 索引对象不可变  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  index = df.index
  index[0] = 'first'

  # 输出
  TypeError: Index does not support mutable operations
  ```

- 类似于一个固定大小的集合  
  集合的大部分属性和方法同样适用于索引对象  
  
  |方法|说明|
  |:-----|:----|
  |append|连接另一个 Index 对象，产生一个新的 Index|
  |difference|计算差集，并得到一个 Index|
  |intersection|计算交集|
  |union|计算并集|
  |delete|删除索引 i 处的元素，并得到新的 Index|
  |drop|删除传入的值，并得到新的 Index|
  |insert|将元素插入到索引 i 处，并得到新的 Index|
  |is_unique|当 Index 没有重复值时，返回True|
  
  ```py
  # 输入
  import pandas as pd

  data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
          'year': [2000, 2001, 2002, 2001, 2002, 2003],
          'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}

  df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
                    index=['one', 'two', 'three', 'four', 'five', 'six'])

  index = df.index
  columns = df.columns
  print('one' in index)
  print('2003' in columns)
  
  # 输出
  True
  False
  ```
  
- 与集合最大的不同在于，索引对象可以包含重复的标签  
  选择重复的标签，会显示该标签的所有结果  
  ```py
  # 输入
  import pandas as pd

  # data = {'state sta': ['Ohio', 'Ohio', 'Ohio', 'Nevada', 'Nevada', 'Nevada'],
  #         'year': [2000, 2001, 2002, 2001, 2002, 2003],
  #         'pop': [1.5, 1.7, 3.6, 2.4, 2.9, 3.2]}
  #
  # df = pd.DataFrame(data, columns=['year', 'state sta', 'pop'],
  #                   index=['one', 'two', 'three', 'four', 'five', 'six'])

  dup_index = pd.Index(['one', 'one', 'three', 'four', 'five', 'six'])
  print(dup_index)
  
  # 输出
  Index(['one', 'one', 'three', 'four', 'five', 'six'], dtype='object')
  ```
  
### 重新索引
`reindex()`方法可以创建一个新的对象，它的数据符合新的索引，即根据新索引进行重排  

- Series 对象
  - `reindex()`会根据新索引重排。当某个索引值不存在时，引入缺失值  
    ```py
    # 输入
    import pandas as pd

    obj1 = pd.Series([4.5, 7.2, -5.3, 3.6], index=['a', 'b', 'c', 'd'])
    print(obj1)
    print('--------------------')
    obj2 = obj1.reindex(['a', 'b', 'c', 'd', 'e'])
    print(obj2)
    
    # 输出
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    dtype: float64
    --------------------
    a    4.5
    b    7.2
    c   -5.3
    d    3.6
    e    NaN
    dtype: float64
    ```
  
