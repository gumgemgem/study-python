# 迭代器

## 定义
- 用来迭代取值的工具，是一个可以记住遍历的位置的对象  
- 迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束
- 迭代器**只能前进不能后退**  

## 可迭代对象与迭代器对象
- 可迭代对象（Iterable）  
  - 可迭代对象通过索引的方式进行迭代取值，但只适用于序列类型：字符串、列表、元组  
  - 没对于没有索引的字典、集合等非序列类型，只能通过迭代器的方式进行迭代取值  
  - 字符串、列表、元组、字典、集合、打开的文件都是可迭代对象  
  
- 迭代器对象（Iterator）  
  - 迭代器对象内置有`iter()`和`next()`方法  
  - 执行迭代器对象`iter()`或迭代器`.__iter__()`方法得到的依然是迭代器本身  
  - 执行迭代器对象`next()`或迭代器`.__next__()`方法计算出迭代器中的下一个值  
  - 迭代器对象可以使用`for`语句进行遍历，也可以使用`next()`函数进行遍历，也可以用迭代器`.__next__()`进行遍历  
  
- 区别与联系  
  迭代器对象一定是可迭代对象，但可迭代对象不一定是迭代器对象  

- 实例  
  ```
  # 输入
  l = [1, 2, 3, 4]
  it = iter(l)   # 创建迭代器对象
  print(next(it)) # 用 next() 输出迭代器的下一个元素
  print(next(it))
  
  # 输出
  1
  2
  ```
  ```
  # 输入
  l = [1, 2, 3, 4]
  it = iter(l)   # 创建迭代器对象

  for x in it:   # 用 for循环进行遍历
      print(x, end=" ")
      
  # 输出
  1 2 3 4
  ```
  
## 创建迭代器
把对象/类创建为迭代器，必须实现`__iter__()`和`__next__()`方法  
- `__iter__()`：返回迭代器对象本身  
- `__next__()`：返回序列中的下一个项目  
```
# 输入
from collections import Iterator

class MyNumbers:
    def __iter__(self):
        self.a = 1
        return self   # 返回迭代器对象本身

    def __next__(self):
        x = self.a
        self.a += 1
        return x


myclass = MyNumbers()
myiter = iter(myclass)   # iter() 方法返回的是迭代器本身

print(isinstance(myclass, Iterator))   # 判断 myclass 是否为一个迭代器对象 
print(myclass == myiter)   # 判断 myclass 是否和 myiter 一样
print(next(myclass))   # 等价于 print(next(myiter)) 
print(next(myclass))   # 等价于 print(next(myiter))
print(myclass.__next__())   # 迭代器输出元素可以用

# 输出
True
True
1
2
3
```
