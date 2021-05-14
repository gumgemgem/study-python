<details>
  <summary>目录</summary>
  
  - [enumerate()](#enumerate)
  - [len()](#len)
  - [list()](#list)
  - [max()](#max)
  - [min()](#min)
  - [range()](#range)
  - [sorted()](#sorted)
  
</details>  

# enumerate()
- 描述  
  将一个可遍历的数据对象（如列表、元组或字符串）组合为一个索引序列，同时列出数据和数据下标`(i, value)元组序列`，一般用在`for`循环当中  

- 语法  
  ```
  enumerate(sequence, [start=0])
  ```
  
  参数说明：  
  `sequence`：一个序列、迭代器或其他支持迭代的对象  
  `start`：返回时下标起始位置  
  
  返回值：  
  enumerate（枚举）**对象**  
  
- 实例
  - 不在`for`循环中使用
    ```
    seasons = ['Spring', 'Summer', 'Fall', 'Winter']
    print(list(enumerate(seasons)))
    print(list(enumerate(seasons, start=1)))

    # 输出：
    [(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
    [(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]
    ```  
  
  - 在`for`循环中使用  
    ```
    seq = ['one', 'two', 'three']
    for i, element in enumerate(seq, 1):
        print(i, element)
        
    # 输出：
    1 one
    2 two
    3 three
    ```

# len()
- 描述  
  用于返回对象的长度或者项目个数  

- 语法
  `len(s)`  

- 实例
  ```
  In [1]: str = 'runoob'
          len(str)
          
  Out [1]: 6

  In [2]: l = [1, 2, 3, 4, 5]
          len(l)
          
  Out [2]: 5
  ```

# list()

- 描述  
  用于将元组、字符串等可迭代对象转化为列表  

- 语法将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中
  `list(seq)`  
  
  返回值：返回列表  

- 实例
  ```
  In [1]: tuple = (1, 2, 3)
          list1 = list(tuple)
          print(list1)
          
  Out [1]: [1, 2, 3]

  In [2]: str = 'Hello World'
          list2 = list(str)
          print(list2)
          
  Out [2]: ['H', 'e', 'l', 'l', 'o', ' ', 'W', 'o', 'r', 'l', 'd']
  ```

# max()

- 描述  
  用于返回给定参数的最大值，参数可以是序列  

- 语法
  ```
  max(x, y, z, ...)
  ```
  
  参数说明：  
  - 入参类型不能混入，要么全是 Number(int/float/complex/bool) 类型，要么全是序列
  - 当入参类型为序列时：单序列入参，返回序列中最大的数值；多序列入参，按索引顺序，逐一对比各序列当前索引位的“值”，直到遇见最大值立即停止对比，并返回最大值所在的**序列**  

- 实例
  ```
  In [1]: max(-1, -0.5, 0)
          
  Out [1]: 0

  In [2]: max([2, 4], [1, 5], [3, 1], [2, 5], [0, 7])
          
  Out [2]: [3, 1]
  ```
  
# min()

- 描述  
  用于返回给定参数的最小值，参数可以是序列  

- 语法  
  ```
  min(x, y, z, ...)
  ```
  
  参数说明：  
  - 入参类型不能混入，要么全是 Number(int/float/complex/bool) 类型，要么全是序列
  - 当入参类型为序列时：单序列入参，返回序列中最小的数值；多序列入参，按索引顺序，逐一对比各序列当前索引位的“值”，直到遇见最小值立即停止对比，并返回最小值所在的**序列**
  
- 实例
  ```
  In [1]: min(-1, -0.5, 0)
          
  Out [1]: -1

  In [2]: min([2, 4], [1, 5], [3, 1], [2, 5], [0, 7])
          
  Out [2]: [0, 7]
  ```

# range()  

- 描述  
  - python3 中 `range()` 函数返回的是一个**可迭代对象**，而非一个列表类型；可以用 `list()` 函数将可迭代的对象转化为列表  
  - python2 中 `range()` 函数返回的是一个**列表**  
  
- 语法  
  ```
  range(end)
  range(start, end[, step])
  ```
  
  参数说明：  
  - start 可省略，默认值为 0  
  - end 不可省略，计数规则是左闭右开，即 \[start, end)  
  - step 可以省略，默认值为 1  
  - 取数规则是从 start 开始依次加上步长值，不论步长值是正数或负数（与列表、元组等可迭代对象的[逆序截取](https://github.com/gumgemgem/study-python/edit/main/Note/data-structure/Tuple.md)的规则不同）

- 实例
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

  In [4]: for i in range(4，-4，-2):
            print(i, end = ' ')

  Out [4]： 4 2 0 -2
  ```

# sorted()

- 描述  
  `sorted()函数`对所有可迭代的对象可以进行排序操作  
  与`sort()方法`的区别：  
  - `sort()`是只应用在`List`上的方法；`sorted()`是可以对所有可迭代的对象进行排序操作的函数
  - `sort()`返回的是对已经存在的列表进行操作；`sorted()`返回的是一个新的可迭代对象，而不是在原来序列的基础上进行的操作
  
- 语法  
  ```
  sorted(iterable, key=None, reverse=False)
  ```
  
  参数说明：  
  - `iterable`：可迭代的对象  
  - `key`：主要是用来进行比较的元素；只有一个参数，具体的函数的参数就是取自于可迭代对象中，指定可迭代对象中的一个元素来进行排序  
  - `reverse`：排序规则，`reverse = True`为降序，`reverse = False`为升序（**默认**）  
  
  返回值：  
  返回重新排序的可迭代对象
  
- 实例  
  ```
  In [1]: example_list = [5, 0, 6, 1, 2, 7, 3, 4]
          result_list = sorted(example_list, key=lambda x: x*-1)
          print(result_list)
          
  Out [1]: [7, 6, 5, 4, 3, 2, 1, 0]
  
  In [2]: # 先按照成绩进行降序排列，相同成绩的按照名字进行升序排序
          d1 = [{'name': 'alice', 'score': 38}, {'name': 'bob', 'score': 18}, {'name': 'darl', 'score': 28}, {'name': 'christ', 'score': 28}]
          l = sorted(d1, key=lambda x: (-x['score'], x['name']))
          print(l)
          
  Out [2]: [{'name': 'alice', 'score': 38}, {'name': 'christ', 'score': 28}, {'name': 'darl', 'score': 28}, {'name': 'bob', 'score': 18}]
  ```

# zip()

- 描述
  创建了一个来自每个可迭代对象中元素的迭代器，即将可迭代对象中的对应元素打包成一个个元组，返回的是一个元组的迭代器  

- 语法
  ```
  zip([iterable, ...])
  ```
  
  注意：  
  - 当所输入的可迭代对象中最短的一个被耗尽时，迭代其将停止迭代
  - `python2` 中 `zip()` 返回的是一个列表； `python3` 中 `zip()` 返回的是一个对象，可以通过函数转换来输出，其中输出对象中第 i 个元组包含来自每个参数序列或可迭代对象的第 i 个元素
  - `zip` 和 `*` 结合可以用来拆解一个列表

- 实例
  ```
  In[1]: a = [1, 2, 3]
         b = [4, 5, 6]
         c = [4, 5, 7, 8]
         zipped1 = zip(a, b)
         zipped2 = zip(a, c)
         print(zipped1)
         print(zipped2)
         a1, b1 = zip(*zip(a, b))
         print(a1 == a and b1 == b)
  ```
