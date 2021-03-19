# 元组
Introduction and syntax of Tuple  

## 1、写在前面  
以下以`In []`和`Out []`开始的代码均是在 jupyter-notebook（即 ipython） 的环境下运行的，因此可以直接输出变量  
其他格式的代码是在 pycharm（非 ipython） 的环境下运行的，必须用 print 函数进行输出

## 2、定义  
固定长度，不可改变的 python 序列对象  

## 3、初始化  
- 用逗号分隔（加不加括号都行，但建议是必须的）  
  ```
  In [1]: tup1 = 4，5，6
  In [2]: tup1
  In [3]: tup2 = (1，2，3)
  In [4]: tup2
  
  Out [2]: (4, 5, 6)
  Out [4]: (1, 2, 3)
  ```  
  
- 用 tuple() 可以将任意序列或迭代器转化为元组  
  ```
  In [1]: tuple([4, 5, 6])

  Out [1]: (4, 5, 6)
  ```
  ```
  In [1]: tuple('string')

  Out [1]: ('s', 't', 'r', 'i', 'n', 'g')
  ```  
  
- 创建空元组  
  ```
  tup = ()
  ```
  
- 只含有一个元素的元组
  通过在该元素的后面加上逗号来创建,不加逗号会被认为是整型  
  ```
  tup = ('hello',)
  ```

## 4、索引和截取  
- 用方括号 `[]` 访问元素，序列从 0 开始  

- 元组中存储的对象可以是可变的也可以是不可变的  
  一旦创建了元组，元组中的对象就不能修改了，但如果元组中某个对象是可变的，可以在原位进行修改  
  ```
  In [1]: tup = tuple(['foo', [1, 2], True])
  In [2]: tup[1].append(3)
  In [3]: tup

  Out [3]: ('foo', [1, 2, 3], True)
  ```  
  
- 切片的方式截取元组中的元素`[start : end : step]` 其中 start 和 end 为左闭右开即 `[start, end)`  
  - 步长 step 取正数，表示**正序截取**  
    默认值：start 默认值为 0，end 默认值为序列的长度，step 默认值为 1  
    规则：start 必须在 end 的左边，从左至右按步长进行截取
    ```
    In [1]: tup = (1, 2, 3, 4, 5)
    In [2]: print('tup[1:4]: ', tup[1:4])
    In [3]: print('tup[1:]: ', tup[1:])
    In [4]: print('tup[::2]: ', tup[::2])
    In [5]: print('tup[-4:3]: ', tup[-4:3])

    Out [2]: tup[1:4]: (2, 3, 4)
    Out [3]: tup[1:]: (2, 3, 4, 5)
    Out [4]: tup[::2]: (1, 3, 5)
    Out [5]: tup[-4:3]: (2, 3)
    ```  
  - 步长 step 取负数，表示**逆序截取**  
    默认值：start 默认值为 -1，end 默认值为 0 且**在 end 取默认值时包含 0**  
    规则：start 必须在 end 的右边，从右至左按步长进行截取，与[`range()`函数的规则](https://github.com/gumgemgem/study-python/blob/main/Note/function/build-in_function.md)不同
    ```
    In [1]: tup = (1, 2, 3, 4, 5)
    In [2]: print('tup[::-1]: ', tup[::-1])
    In [3]: print('tup[:1:-2]: ', tup[::-2])
    In [4]: print('tup[:0:-1]: ', tup[:0:-1])  # end 不取默认值时仍然是左闭右开区间

    Out [2]: tup[::-1]: (5, 4, 3, 2, 1)
    Out [3]: tup[::-2]: (5, 3)
    Out [4]: tup[:0:-1]: (5, 4, 3, 2)
    ```  
    
## 5、删除元组  
  元组中的元素不可以删除，但是整个元组可以用 `del` 进行删除  
  ```
  tup = (4, 5, 6)
  del tup
  ```
  
## 6、元组运算符  
  - `+` 加号运算符将元组串联起来  
  - `*` 乘号运算符将元组复制串联起来  
    ```
    In[1]: tup = (1, 2)
           tup * 2
          
    Out[1]: (1, 2, 1, 2)
    ```
  - `in/not in` 判断元素是否存在  
  - `for` 循环进行迭代  

## 7、元组的内置函数  
  [`len()、max()、min()、tuple()`](https://github.com/gumgemgem/study-python/blob/main/Note/function/build-in_function.md)  
  
## 8、序列的打包与拆包
- 序列的打包
  定义序列给序列赋值本质就是将各元素打包进序列，即序列打包  

- 序列的拆包
  - 将序列赋值给类似序列的变量，**序列拆包**要求等号左侧的变量数与右侧序列里的所含的元素数相同  
    ```
    In [1]: tup1 = (4, 5, 6)
            a, b, c = tup1
            b
    In [2]: tup2 = (4, 5, (6, 7))
            a, b, (c, d) = tup2
            d
    In [3]: m, n = (1, 2)  # 序列的拆包可以很容易实现替换变量的名字
            n, m = (m , n)
            n
    In [4]: p1, p2, *rest = tup1  # 序列中开头或结尾不需要的元素可以用 *rest 进行抓取
            rest                  # rest 的输出形式是列表
    In [5]: *_ , q = tup1         # rest 的名字不重要，作为惯用写法，许多 Python 程序员会将不需要的变量使用下划线 *_
            _

    Out [1]: 5
    Out [2]: 7
    Out [3]: 1
    Out [4]: [6]
    Out [5]: [4, 5]
  
  - 序列中有嵌套时，注意拆包方式
    ```
    seq = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
    x, y, z = seq  # 列表的拆包
    print(x, y, z)
    
    for a, b, c in seq:  # 相当与 a, b, c = seq[i]，属于元组的拆包
        print('a = {0}, b = {1}, c = {2}'.format(a, b, c))
        
    # 输出：
    (1, 2, 3), (4, 5, 6), (7, 8, 9)

    a = 1, b = 2, c = 3
    a = 4, b = 5, c = 6
    a = 7, b = 8, c = 9
    ```
  
## 9、count 方法
  `count()`可以统计某个值在序列（元组和列表）中出现的频率
  ```
  tup = (1, 1, 1, 2)
  tup.count(1)
  
  # 输出：
  3
  ```
