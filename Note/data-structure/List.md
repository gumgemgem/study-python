# 列表
Introduction and syntax of List

## 1、定义
长度可变，内容可改变的 python 序列对象  

## 2、初始化
- 用`[]`定义
  ```
  l = [1, 2, 3]
  ```
  
- 用`list()`函数
  ```
  tup = ('a', 'b', 'c')
  l = list(tup)
  ```
- 空列表
  ```
  l1 = []  # 或
  l2 = list()
  ```

## 3、索引和切片
[见「元组的索引和截取」](https://github.com/gumgemgem/study-python/blob/main/Note/data-structure/Tuple.md)

## 4、修改、添加和删除
- 修改  
  需要修改列表中的指定元素，直接对该处的元素进行重新赋值
  
- 添加
  - 在列表末尾添加元素：`append()`方法
    ```
    In[1]: list1 = ['a', 'b', 'c']
           list1.append('d')
           list1
    Out[1]: ['a', 'b', 'c', 'd']
    ```
  
  - 在特定位置插入元素：`insert()`方法
    ```
    In[1]: list2 = ['a', 'b', 'd']
           list2.insert(2, 'c')
           list2
    Out[1]: ['a', 'b', 'c', 'd']
    ```
  
  - 追加多个元素：`extend()`方法
    ```
    In[1]: list3 = ['a', 'b', 'c']
           list3.extend(['d', (1, 2)])
           list3
    Out[1]: ['a', 'b', 'c', 'd', (1, 2)]
    ```

- 删除
  - 移除并**返回**指定位置的元素：`pop()`方法  
    ```
    l = ['a', 'b', 'c', 'd']
    l.pop(2)
    print(l)
    
    # 输出：
    ’c‘
    ['a', 'b', 'd']
    ```
  
  - 删除某个确定的值，会先寻找**第一个值**并删除：`remove()`方法  
    ```
    l = ['a', 'b', 'c', 'd', 'b']
    l.remove(’b‘)
    print(l)
    
    # 输出：
    ['a', 'c', 'd', 'b']
    ```
  
  - 删除指定位置的元素或者切片或者删除整个列表：`del`语句  
    ```
    l = ['a', 'b', 'c', 'd', 'b']
    del l[1]  # 删除列表中的第二个元素
    print(l)
    del l[1:3]  # 删除切片
    print(l)
    del l    # 删除整个列表
    print(l)
    
    # 输出：
    ['a', 'c', 'd', 'b']
    ['a', b']
    NameError: name 'l' is not defined
    ```

## 5、列表的方法
- `sort()`方法  
  - 说明    
    是列表独有的排序方法，它将列表原地排序，但不创建新的对象  

  - 语法
    ```
    list.sort(key=None, reverse=False)
    ```
    `key`：主要是用来进行比较的元素  
    `reverse`：排序规则，`reverse = True`为降序，`reverse = False`为升序（**默认**）  

  - 实例
    ```
    a = [7, 2, 5, 1, 3]
    a.sort()
    print(a)

    b = ['Google', 'Runoob', 'Taobao', 'Facebook']  # 默认按照第一个字符进行排序
    b.sort()
    print(b)

    # 输出：
    [1, 2, 3, 5, 7]
    ['Facebook', 'Google', 'Runoob', 'Taobao']
    ```
    ```
    # sort() 可以指定 key 进行排序
    c = ['saw', 'small', 'He', 'foxes', 'six']
    c.sort(key=len)
    print(c)

    def takeSecond(elem):  # 获取列表的第二个元素
        return elem[1]

    d = [(2, 2), (3, 4), (4, 1), (1, 3)]
    d.sort(key=takeSecond)
    print(d)

    # 输出;
    ['He', 'saw', 'six', 'small', 'foxes']
    [(4, 1), (2, 2), (1, 3), (3, 4)]
    ```

    
- `count()`方法  
  `count()`可以统计某个值在序列（元组和列表）中出现的频率  
  ```
  l = [1, 1, 1, 2]
  l.count(1)

  # 输出：
  3
  ``` 

## 6、列表的运算符
[见「元组的运算符」](https://github.com/gumgemgem/study-python/blob/main/Note/data-structure/Tuple.md)  
  
## 7、列表的内置函数
[`len()、max()、min()、list()、enumerate()、sorted()、zip()、reversed()`](https://github.com/gumgemgem/study-python/blob/main/Note/function/build-in_function.md)

## 8、列表的拆包与打包
[见「序列的拆包和打包」](https://github.com/gumgemgem/study-python/blob/main/Note/data-structure/Tuple.md)
