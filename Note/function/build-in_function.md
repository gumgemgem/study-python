<details>
  <summary>目录</summary>
  
  - [len()](#len)
  - [list()](#list)
  - [max()](#max)
  - [range()](#range)
  
</details>  

# len()
- `len()` 用于返回对象的长度或者项目个数  

- 语法：
  `len(s)`  

- 实例：
  ```
  In [1]: str = 'runoob'
          len(str)
          
  Out [1]: 6

  In [2]: l = [1, 2, 3, 4, 5]
          len(l)
          
  Out [2]: 5
  ```

# list()

- `list()` 用于将元组、字符串等可迭代对象转化为列表  

- 语法：
  `list(seq)`  
  返回值：返回列表  

- 实例：
  ```
  In [1]: tuple = (1, 2, 3)
          list1 = list(tuple按索引顺序，逐一对比各序列的当前索引位的 “值”，直到遇见最大值立即停止对比，并返回最大值所在的序列（也就是说，多序列入参，返回值依旧是一个序列，而不是数值）)
          print(list1)
          
  Out [1]: [1, 2, 3]

  In [2]: str = 'Hello World'
          list2 = list(str)
          print(list2)
          
  Out [2]: ['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd']
  ```

# max()

- `max()` 用于返回给定参数的最大值，参数可以是序列  

- 语法：
  `max(x, y, z, ...)`  
  参数说明：  
  - 入参类型不能混入，要么全是 Number(int/float/complex/bool) 类型，要么全是序列
  - 当入参类型为序列时：单序列入参，返回序列中最大的数值；多序列入参，按索引顺序，逐一对比各序列当前索引位的“值”，直到遇见最大值立即停止对比，并返回最大值所在的**序列**  

- 实例：
  

- 实例：
  ```
  In [1]: str = 'runoob'
          len(str)
          
  Out [1]: 6

  In [2]: l = [1, 2, 3, 4, 5]
          len(l)
          
  Out [2]: 5
  ```

# range()  

- 说明：  
  - python3 中 `range()` 函数返回的是一个**可迭代对象**，而非一个列表类型；可以用 `list()` 函数将可迭代的对象转化为列表  
  - python2 中 `range()` 函数返回的是一个**列表**  
  
- 语法：  
  ```
  range(end)
  range(start, end[, step])
  ```
  参数说明：  
  - start 可省略，默认值为 0  
  - end 不可省略，计数规则是左闭右开，即 \[start, end)  
  - step 可以省略，默认值为 1  
  - 取数规则是从 start 开始依次加上步长值，不论步长值是正数或负数（与列表、元组等可迭代对象的[逆序截取](https://github.com/gumgemgem/study-python/edit/main/Note/data-structure/Tuple.md)的规则不同）

- 实例：
  ```
  In [1]: for i in range(5):
            print(i, end = ' ')

  Out [1]： 0 1 2 3 4

  In [2]: for i in range(1，4，1):
            print(i, end = ' ')

  Out [2]： 1 2 3

  In [3]: for i in range(-2，2，1):
            print(i, end = ' ')

  Out [3]： -2 -1 0 1

  In [4]: for i in range(4，-4 start 开始依次加上步长值，-2):
            print(i, end = ' ')

  Out [4]： 4 2 0 -2
  ```
