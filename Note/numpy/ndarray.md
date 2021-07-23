# ndarray

[官方文档](https://numpy.org/doc/stable/)

约定导入`NumPy`的语法：  
```py
import numpy as np
```

## 1、定义

ndarray 是 NumPy 的一种多维数组对象  

数组和列表的区别：  
- 数组是一个同构多维容器，即所有的元素必须是相同类型的  
- 数组支持广播计算的特性，列表不支持广播计算  

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
`arange()`与`range()`方法是一致的  
1. `arange(n)`表示 [0, n) 左闭右开的区间  
2. `arange(n, m)`表示 [n, m) 左闭右开的区间  
3. `arange(n, m, s)`表示 [n, m) 左闭右开的区间按步长 s 进行取值  

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
常用的数据类型有：int, str, float 等  

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

`np.genfromtxt(路径)`方法可以从 txt 文件中读取数组  
常用参数： 
- 路径：windows 系统上的路径需要用 r 进行转义  
- delimiter：分隔符  
- dtype：数据类型  

```py
# 输入
import numpy as np

arr1 = np.genfromtxt('/media/ubuntu/64ee45db-468c-4e40-ae91-1d1a54a51213/ubuntu/PycharmProjects/test1/pydata-book-2nd-edition/data_example.txt', delimiter=',', dtype=int)
print(arr1)

# 输出
[[  1   2   3]
 [ 10  20  30]
 [100 200 300]]
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

## 4、索引和切片
数组的索引和切片与列表的索引和切片是类似的  

```py
# 输入
import numpy as np

arr2 = np.array([[1, 2, 3, 4, 5],
                 [6, 7, 8, 9, 10],
                 [11, 12, 13, 14, 15]])
print(arr2)
print('--------------------')

print(arr2[1])
print('--------------------')
print(arr2[0: 2])
print('--------------------')
print(arr2[1][0])
print('--------------------')
print(arr2[0:2, 1:3])
print('--------------------')
print(arr2[0:2][1:3])

# 输出
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]
 [11 12 13 14 15]]
--------------------
[ 6  7  8  9 10]
--------------------
[[ 1  2  3  4  5]
 [ 6  7  8  9 10]]
--------------------
6
--------------------
[[2 3]
 [7 8]]
--------------------
[[ 6  7  8  9 10]]
```

## 5、ndarray 常用方法

### 5.1 reshape()
`reshape()`方法返回在原数组的基础上更改后的**新数组**  

- 返回的是更改形状后的新数组  
- 新数组的元素个数必须和原数组保持一致  
- 更改为一维数组可表示为`reshape(-1)`（建议）或`reshape(n)`（n 为数组元素个数，较大时不友好） 

```py
# 输入
import numpy as np

one_arr = np.arange(24)
two_arr1 = one_arr.reshape(3, 8)
print(two_arr1)
two_arr2 = one_arr.reshape(4, 6)
print(two_arr2)

# 输出
[[ 0  1  2  3  4  5  6  7]
 [ 8  9 10 11 12 13 14 15]
 [16 17 18 19 20 21 22 23]]
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]]
```

### 5.2 resize()
`resize()`方法在**原数组**的基础上直接更改形状，无返回值

- 直接在原数组上进行修改，无返回值  
- 新数组的元素个数不需要和原数组保持一致：少了截取，多了用 0 补全  
- 更改为一维数组只能表示为`resize(n)`（n 为数组元素个数） 

```py
# 输入
import numpy as np

one_arr = np.arange(24)
one_arr.resize(3, 8)
print(one_arr)
one_arr.resize(5, 6)
print(one_arr)

# 输出
[[ 0  1  2  3  4  5  6  7]
 [ 8  9 10 11 12 13 14 15]
 [16 17 18 19 20 21 22 23]]
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]
 [ 0  0  0  0  0  0]]
```

### 5.3 flatten()
将多维数组降为一维数组  
**注意**：返回的是数组的拷贝（copy），对拷贝所做的修改不会影响原来的数组  

```py
# 输入
import numpy as np

arr2 = np.arange(24).reshape(4, 6)
print(arr2)

arr1 = arr2.flatten()
print(arr1)
arr1[23] = 0
print('修改后的 arr1:\n{}'.format(arr1))
print('修改后的 arr2:\n{}'.format(arr2))

# 输出
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]]
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23]
修改后的 arr1:
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22  0]
修改后的 arr2:
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]]
```

### 5.4 ravel()
将多维数组降为一维数组  
**注意**：返回的是数组的视图（view），对视图所做的修改会影响原来的数组  

```py
# 输入
import numpy as np

arr2 = np.arange(24).reshape(4, 6)
print(arr2)

arr1 = arr2.ravel()
print(arr1)
arr1[23] = 0
print('修改后的 arr1:\n{}'.format(arr1))
print('修改后的 arr2:\n{}'.format(arr2))

# 输出
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22 23]]
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22 23]
修改后的 arr1:
[ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16 17 18 19 20 21 22  0]
修改后的 arr2:
[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]
 [18 19 20 21 22  0]]
```

## 6、ndarray 常用统计函数
通过数组上的一组数学函数对整个数组或某个轴向的数据进行统计计算  
常用的统计函数形式：`np.func(ndarray)`或`ndarray.func()`

|方法|说明|
|:----|:----|
|arr.sum() 或 np.sum(arr)|对数组中全部或某轴向的元素求和。零长度的数组求和为 0|
|arr.mean() 或 np.mean(arr)|求算数平均数。零长度的数组算数平均数为 NaN|
|arr.std() 或 np.std(arr)|标准差。自由度可调，默认为 n|
|arr.var() 或 np.var(arr)|方差。自由度可调，默认为 n|
|arr.min() 或 np.min(arr)|最小值|
|arr.max() 或 np.max(arr)|最大值|
|arr.argmin() 或 np.argmin(arr)|最小元素的索引|
|arr.argmax() 或 np.argmax(arr)|最大元素的索引|
|arr.cumsum() 或 np.cumsum(arr)|对数组中全部或某轴向所有元素的累计和|
|arr.cumprod() 或 np.cumprod(arr)|对数组中全部或某轴向所有元素的累计积|

`axis=i`参数可以沿某一轴向进行计算：  
参数 i 表示函数沿着第 i 个下标变化的方式进行计算，[详见](https://zhuanlan.zhihu.com/p/31275071)  

```py
# 输入
import numpy as np
arr2 = np.array([[1, 2, 3, 4, 5],
                 [6, 12, 8, 14, 10],
                 [11, 7, 13, 9, 15]])
print(arr2)
print('--------------------')

print(arr2.max(axis=0))
print(arr2.max(axis=1))

# 输出
[[ 1  2  3  4  5]
 [ 6 12  8 14 10]
 [11  7 13  9 15]]
--------------------
[11 12 13 14 15]
[ 5 14 15]
```

```py
# 输入
import numpy as np

three_array = np.array([[[1, 2, 3],
                         [10, 20, 30]],
                        [[4, 5, 6],
                         [40, 50, 60]]])
print(three_array)
print('---------------------')

print(np.sum(three_array, axis=0))
print('---------------------')
print(np.sum(three_array, axis=1))
print('---------------------')
print(np.sum(three_array, axis=2))

# 输出
[[[ 1  2  3]
  [10 20 30]]

 [[ 4  5  6]
  [40 50 60]]]
---------------------
[[ 5  7  9]
 [50 70 90]]
---------------------
[[11 22 33]
 [44 55 66]]
---------------------
[[  6  60]
 [ 15 150]]
```

## 7、数组的广播计算
广播计算：大小相同的数组之间的任何算术运算都会将运算应用到元素级  

- 数组之间的运算必须是在大小相同的数组之间进行，否则会报错  
- 数组之间的乘法是数组之间的元素对应相乘，与矩阵的乘法不同  

```py
# 输入
import numpy as np

arr1 = np.array([[1, 2, 3, 4, 5],
                 [6, 12, 8, 14, 10],
                 [11, 7, 13, 9, 15]])
arr2 = np.array([np.arange(1, 6), np.arange(6, 11), np.arange(11, 16)])

print(arr1 * 2)
print('-------------------------')
print(arr1 + arr2)
print('-------------------------')
print(arr1 + 5)
print('-------------------------')
print(arr1 * arr2)

# 输出
[[ 2  4  6  8 10]
 [12 24 16 28 20]
 [22 14 26 18 30]]
-------------------------
[[ 2  4  6  8 10]
 [12 19 16 23 20]
 [22 19 26 23 30]]
-------------------------
[[ 6  7  8  9 10]
 [11 17 13 19 15]
 [16 12 18 14 20]]
-------------------------
[[  1   4   9  16  25]
 [ 36  84  64 126 100]
 [121  84 169 126 225]]
```