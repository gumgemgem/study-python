# 元组
Introduction and syntax of Tuple  

## 写在前面  
以下以`In []`和`Out []`开始的代码均是在 jupyter-notebook(即ipython) 的环境下运行的，因此可以直接输出变量  
其他格式的代码是在 pycharm(非ipython) 的环境下运行的，必须用 print 函数进行输出

## 定义  
固定长度，不可改变的 python 序列对象  

## 初始化  
- 用逗号分隔  
  ```
  In [1]: tup = 4，5，6
  In [2]: tup

  Out [2]: (4, 5, 6)
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

## 索引、截取  
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
    
## 删除元组  
  元组中的元素不可以删除，但是整个元组可以用 `del` 进行删除  
  ```
  tup = (4, 5, 6)
  del tup
  ```
  
## 元组运算符  
  - `+` 加号运算符将元组串联起来  
  - `*` 乘号运算符将元组复制串联起来  
    ```
    In[1]: tup = (1, 2)
           tup * 2
          
    Out[1]: (1, 2, 1, 2)
    ```
  - `in/not in` 判断元素是否存在  
  - `for` 循环进行迭代  

## 元组的内置函数  
  [`len()、max()、min()、tuple()`](https://github.com/gumgemgem/study-python/blob/main/Note/function/build-in_function.md)  
  
## 元组的拆分  
