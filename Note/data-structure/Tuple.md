# 元组
Introduction and syntax of Tuple  

## 写在前面  
以下代码均是在 jupyter-notebook 的环境下运行的，因此可以直接输出变量；而在 pytcharm 的环境下运行，必须用 print 函数进行输出

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
  `tup = ()`  

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
- 切片的方式截取元组中的元素 \[start : end : step]  
  - 其中：start、end、step 可以省略。start、end 省略表示截取从第一个元素至最后一个元素，step 省略表示步长默认为 1  
    ```
    In [1]: tup = (1, 2, 3, 4, 5)
    In [2]: print('tup[1:4]: ', tup[1:4])
    In [3]: print('tup[1:]: ', tup[1:])
    In [4]: print('tup[::2]: ', tup[::2])

    Out [2]: tup[1:4]: (2, 3, 4)
    Out [3]: tup[1:]: (2, 3, 4, 5)
    Out [4]: tup[::2]: (1, 3, 5)
    ```