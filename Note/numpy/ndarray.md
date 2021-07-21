# ndarray

约定导入`NumPy`的语法：  
```py
import numpy as np
```

## 1、定义
ndarray 是 NumPy 的一种多维数组对象，是一个同构数组多维容器，即所有的元素必须是相同类型的  

## 2、创建 ndarray

### 2.1 array() 方法创建一维数组
- 基于列表  
```py
one_array = np.array(无嵌套列表)
```

- 基于元组  
```py
one_array = np.array(无嵌套元组)
```

- 实例  
```py
# 输入
import numpy as np

one_array1 = np.array([1, 2, 3, 4, 5])
print(type(one_array1))
print(one_array1)
print('------------------------------')

one_array2 = np.array((6, 7, 8, 9, 10))
print(type(one_array2))
print(one_array2)

# 输出
<class 'numpy.ndarray'>
[1 2 3 4 5]
------------------------------
<class 'numpy.ndarray'>
[ 6  7  8  9 10]
```

### 2.2 array() 方法创建二维数组
- 基于列表  
```py
two_array = np.array(嵌套二层列表)
```
其中：嵌套的数据必须是同类型等长的一组数据，如列表、元组  

- 基于元组  
```py
two_array = np.array(嵌套二层元组)
```
其中：嵌套的数据必须是同类型等长的一组数据，如列表、元组  

- 实例  
```py
# 输入
import numpy as np

two_array1 = np.array([[1, 2, 3, 4, 5],
                      [6, 7, 8, 9, 10],
                      [11, 12, 13, 14, 15]])
print(two_array1)
print('------------------------------')

two_array2 = np.array(((1, 2, 3, 4, 5),
                       (6, 7, 8, 9, 10),
                       (11, 12, 13, 14, 15)))
print(two_array2)

# 输出
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]]
------------------------------
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]]
```

### 2.3 array() 方法创建三维数组
- 基于列表  
```py
two_array = np.array(嵌套三层列表)
```
其中：嵌套的数据必须是同类型等长的一组数据，如嵌套二层列表、嵌套二层元组  

- 基于元组  
```py
two_array = np.array(嵌套三层元组)
```
其中：嵌套的数据必须是同类型等长的一组数据，如嵌套二层列表、嵌套二层元组  

- 实例  
```py
# 输入
import numpy as np

three_array1 = np.array([[[1, 2, 3],
                         [10, 20, 30]],
                        [[4, 5, 6],
                         [40, 50, 60]]])
print(three_array1)
print('------------------------------')

three_array2 = np.array((((1, 2, 3),
                          (10, 20, 30)),
                        ((4, 5, 6),
                         (40, 50, 60))))
print(three_array2)

# 输出
[[[ 1  2  3]
  [10 20 30]]

 [[ 4  5  6]
  [40 50 60]]]
------------------------------
[[[ 1  2  3]
  [10 20 30]]

 [[ 4  5  6]
  [40 50 60]]]
```

### 2.4 arange() 方法
`arange(n[, m])`表示 [0, n) 或 [n, m) 左闭右开的区间
- 一维数组  
`np.arange(n)`可以创建 [0, n-1] 的一维数组  
```py
# 输入
import numpy as np

arr1 = np.arange(5)
print(arr1)

# 输出
[0 1 2 3 4]
```

- 二维数组  
`np.array([np.arange(n), np.arange(n), ...])`可以创建二维数组  
```py
# 输入
import numpy as np

arr2 = np.array([np.arange(1, 5), np.arange(1, 5)])
print(arr2)

# 输出
[[1 2 3 4]
 [1 2 3 4]]
```

- 三维数组  
```py
np.array([[np.arange(n), np.arange(n), ...], 
          [np.arange(n), np.arange(n), ...], 
          ...])
```
可以创建二维数组  

```py
# 输入
import numpy as np

arr3 = np.array([[np.arange(1, 5), np.arange(1, 5)],
                 [np.arange(2, 6), np.arange(2, 6)],
                 [np.arange(3, 7), np.arange(3, 7)]])
print(arr3)

# 输出
[[[1 2 3 4]
  [1 2 3 4]]

 [[2 3 4 5]
  [2 3 4 5]]

 [[3 4 5 6]
  [3 4 5 6]]]
```

- dtype 参数  
arange() 方法默认的数据类型是整型，需要更改数据类型，可以使用`dtype`参数  
常用的数据类型有：str, float 等  
```py
# 输入
import numpy as np

arr3 = np.array([[np.arange(1, 5), np.arange(1, 5)],
                 [np.arange(2, 6), np.arange(2, 6)],
                 [np.arange(3, 7), np.arange(3, 7)]], dtype='float')
print(arr3)

# 输出
[[[1. 2. 3. 4.]
  [1. 2. 3. 4.]]

 [[2. 3. 4. 5.]
  [2. 3. 4. 5.]]

 [[3. 4. 5. 6.]
  [3. 4. 5. 6.]]]
```

### 2.5 从文件中获得
`np.genfromtxt()`方法可以从 txt 文件中读取数组  
常用参数：  
- delimiter：分隔符  
- dtype：数据类型
```py
# 输入


# 输出

```

### 2.6 总结
对于任意一个 n 维数组，它的内层都是一个 n-1 维的数组，依次类推

## 3、ndarray 的属性
- ndim  
数组的维度：`array.ndim`  

- shape  
数组的尺度大小：`array.shape`  
注意：输出的尺度大小从左至右依次表示高维数组的尺度大小  
例如：(s, n, m)  
s -- 二维数组有 s 个； n -- 一维数组有 n 个； m -- 一维数组的大小是 m
    
- size  
数组元素的数量：`array.size`  

- 实例  
```py
# 输入
import numpy as np

three_array = np.array([[[1, 2, 3],
                         [10, 20, 30]],
                        [[4, 5, 6],
                         [40, 50, 60]]])
print(three_array)
print('数组维数：', three_array.ndim)
print('数组尺度：', three_array.shape)
print('数组元素的数量：', three_array.size)

# 输出
[[[ 1  2  3]
  [10 20 30]]

 [[ 4  5  6]
  [40 50 60]]]
数组维数： 3
数组尺度： (2, 2, 3)
数组元素的数量： 12
```

## 