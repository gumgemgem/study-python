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
