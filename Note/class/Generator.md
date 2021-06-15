# 生成器

## 定义
生成器是一个用于创建迭代器的工具，本质上仍然是迭代器，python 自动让生成器实现了迭代器协议  
生成器的写法类似于函数，当要返回数据时使用**yield**语句

## yiled 原理
`yield`能够**临时挂起**当前函数，记住上下文，将控制权返回给函数调用者  
在调用生成器运行时，每次遇到`yield`时函数会暂时保存当前所有的运行信息，返回`yield`的值，并在下一次执行`next()`方法时从当前位置继续执行  

  #### yield 和 return 的区别
  - 函数遇到`return`就结束了，销毁上下文；`yield`可以保存函数的运行状态，挂起函数，用来返回多次值  
  - `return`执行流程控制的函数为普通函数；`yield`执行流程控制的函数为生成器函数  

## 实例
```
# 输入
def gensquares(N):
    for i in range(N):
        print('当前的元素为：', i)
        yield i**2


squares = gensquares(5)   # 得到一个生成器对象 squares
print(type(squares))   # 判断 squares 的类型
print(dir(squares))   # 返回 squares 的属性、方法列表

print(next(squares))   # 输出 squares 的元素
print(squares.__next__())   # 输出 squares 的下一个元素
print('--------------------------')   # 和下面的 for 循环输出区分开

for item in squares:   # 遍历 squares 中的元素
    print(item)

print(next(squares))   # 继续输出 squares 的下一个元素
    
# 输出
<class 'generator'>
['__class__', '__del__', '__delattr__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__iter__', '__le__', '__lt__', '__name__', '__ne__', '__new__', '__next__', '__qualname__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', 'close', 'gi_code', 'gi_frame', 'gi_running', 'gi_yieldfrom', 'send', 'throw']
当前的元素为： 0
0
当前的元素为： 1
1
--------------------------
当前的元素为： 2
4
当前的元素为： 3
9
当前的元素为： 4
16
Traceback (most recent call last):
  File "xxx.py", line xxx, in <module>
    print(next(squares))   # 继续输出 squares 的下一个元素
StopIteration
```
综上，  
- squares 是一个生成器对象  
- squares 内部实现了`__iter__()`和`__next__()`方法，本质上 squares 是一个迭代器对象  
- 由于生成器对象本质上是一个迭代器对象，因此可以通过`next()`、`__next__()`、`for`循环输出或遍历生成器中的元素  
- 生成器和迭代器一样，每次输出后将会保存上一次输出的状态，下一次将会从当前位置继续执行；并且在遍历完成后，输出状态没有了，继续输出将会报错  

## 生成器表达式
类似于列表、字典、集合的推导式  

- 定义  
  ```
  generator = (expr for val in collection if condition)
  ```
 
- 实例
  ```
  # 输入
  squares = (x ** 2 for x in range(5))
  print(next(squares))
  print(next(squares))
  for x in squares:
      print(x, end=" ")
      
  # 输出
  0
  1
  4 9 16
  ```

- 生成器表达式也可以作为函数参数  
  ```
  # 输入
  print(sum(x ** 2 for x in range(5)))
  print(dict((x, x ** 2) for x in range(5)))
  
  # 输出
  30
  {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
  ```
