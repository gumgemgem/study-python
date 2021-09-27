# 面向对象编程  

## 1. 基本定义

- **类** ：  
描述具有相同属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例  
- **方法** ：  
类中定义的函数  
- **实例化** ：  
创建一个类的实例，类的具体对象  
- **对象** ：  
同上，类的实例化。对象包括两个数据成员（类变量和实例变量）和方法  
- **类变量** ：  
类变量定义在类中且在函数体外。类变量在整个实例化的对象中是公用的。  
类变量通常不作为实例变量进行使用  
- **实例变量** ：  
在类中且函数体内，属性是用变量来表示的，这种变量就称为实例变量，即 `self.变量名` 形式的变量  
- **局部变量** ：  
在类中且函数体内，只用作当前实例的类，这种变量就称为局部变量，即 `变量名 = 变量值` 形式的变量  

## 2. 类对象

类对象的操作：**实例化** 和 **属性引用**  
实例化 -- 将类实例化为对象：`obj = Classname()`  
属性引用 -- 访问类的属性和方法：`obj.name`  

```py
# 输入
class MyClass:
    """A simple example class"""
    i = 12345

    def f(self):
        return 'hello world'


if __name__ == '__main__':
    x = MyClass()   # 类的实例化
    print('MyClass 类的属性 i 为：', x.i)   # 访问类的属性
    print('MyClass 类的方法 f 的输出为：', x.f())   # 访问类的方法

# 输出
MyClass 类的属性 i 为： 12345
MyClass 类的方法 f 的输出为： hello world
```

## 3. 类的方法

同样使用 `def` 关键字定义方法，但是类的方法必须包含参数 `self`，并且位于第一个参数  

### 3.1 关于 `self`

- 参数 `self` 代表的是 **类的实例**，而不是类，用于访问属于该类的变量  

```py
# 输入
class Test:
    def __init__(self):
        self.a = 6

    def prt(self):
        print(self)
        print(self.__class__)
        print(self.a)


if __name__ == '__main__':
    t = Test()
    t.prt()
    t.prt()

# 输出
<__main__.Test object at 0x0000018FFBE43E50>
<class '__main__.Test'>
6
6
```

说明：  
1. 从上述执行结果可以看出，`self` 代表的是类的实例，代表当前对象的地址；  
2. `self.__class__` 指向类；  
3. `self.属性/方法` 和 `对象.属性/方法` 作用相同； 

- `self` 不是 Python 的关键字，换成其它单词也可以，但必须位于类方法的首位  

```py
# 输入
class Person:
    def __init__(abc, name, age):
        abc.name = name
        abc.age = age

    def myf(xyz):
        print('Hello my name is', xyz.name)


if __name__ == '__main__':
    p = Person('Bill', 63)
    p.myf()

# 输出
Hello my name is Bill
```

### 3.2 `__init__()` 方法

该方法会在类实例化时自动调用，可以将值赋给对象属性

```py
# 输入
class f:
    def __init__(self, a, b):
        self.m = a
        self.n = b

    def sum(self):
        return self.m + self.n


if __name__ == '__main__':
    p = f(3, 5)
    res = p.sum()
    print(res)

# 输出
8
```

## 4. 动态增加属性和方法

当对象或类的属性在需要增加，且不方便修改源码的时候，可以动态增加对象或类的属性和方法  

### 4.1 动态给对象增加属性和方法

动态给对象增加属性和方法时，只对当前对象生效，其他对象是不会受到影响的  

- 增加属性  

语法：`obj.新属性名 = 新属性名的初始值`  

```py
# 输入
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


if __name__ == '__main__':
    s1 = Student('Bill', 22)
    s2 = Student('Mary', 24)
    s1.score = 96
    print(s1.score)
    print(s2.score)

# 输出
    print(s2.score)
AttributeError: 'Student' object has no attribute 'score'
96
```

- 增加方法  

1. 给对象增加方法不可以像增加属性一样直接定义并初始化，要通过 `types.MethodType` 方法给对象绑定新方法  
2. 添加的方法在函数定义时必须要传入 `self` 参数

```py
import types

[定义函数]

obj.新方法名 = types.MethodType(函数名，obj)
```

```py
# 输入
import types

class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


def func(self, gain):
    self.score = gain
    print('成绩为：', self.score)


if __name__ == '__main__':
    s1 = Student('Bill', 22)
    s2 = Student('Mary', 24)
    s1.func = types.MethodType(func, s1)
    s1.func(96)

# 输出
成绩为： 96
```

### 4.2 动态给类增加属性和方法

给类增加的属性和方法将会影响该类实例化的所有对象  

- 增加属性  

语法：`类名.新属性名 = 新属性名的初始值`  

```py
# 输入
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age


if __name__ == '__main__':
    s1 = Student('Bill', 22)
    s2 = Student('Mary', 24)
    Student.score = 96
    print('{}的成绩为：{}'.format(s1.name, s1.score))
    print('{}的成绩为：{}'.format(s2.name, s2.score))

# 输出
Bill的成绩为：96
Mary的成绩为：96
```

- 增加方法  

ToDo：  
1. 增加方法：静态方法和类方法  
2. 实例方法、静态方法、类方法的区别和使用场景，[详情参考](https://www.cnblogs.com/mrwuzs/p/10899498.html)  