# 函数

## 定义
函数使用`def`进行声明；用`return`返回值，可以同时拥有多条`return`语句，也可以没有返回语句，此时默认返回 None  
```
def 函数名(参数列表):
    函数主体
    [return语句]
```

## 参数
函数定义时的参数为**形式参数**，函数调用时的参数为**实际参数**

- 默认值参数  
  函数在**定义**参数列表时如果指定了默认值参数，函数调用时如果省略该参数，则该参数取默认值；如果调用时指定了值，则取指定值  
  **注意**：
  - 默认值参数是针对形参而言的，只有在函数定义时才会有默认参数  
  - 函数定义时，默认参数必须在位置参数的后面  
  ```
  # 输入
  def f(arg=6):
    print(arg)


  f()
  f(5)
  
  # 输出
  6
  5
  ```
  **注意**：默认值只计算一次，因此当默认值为列表、字典会类实例等可变对象时，会累积后续调用时传递的参数  
  ```
  # 输入
  def f1(a, l=[]):
    l.append(a)
    return l


  print(f1(1))
  print(f1(2))
  print(f1(3))
  
  # 输出
  [1]
  [1, 2]
  [1, 2, 3]
  ```
  
- 关键字参数  
  `kwarg=value`形式的关键字参数可以用于调用函数，使用关键字参数允许函数调用时参数的顺序与声明时的顺序不一致  
  ```
  # 输入
  def f(a, x=1, y=2, z=3):
    print("a是：{}，x是：{}，y是：{}，z是：{}".format(a, x, y, z))


  f(6)   # a是位置参数
  f(a=6)   # a是关键字参数
  f(a=6, y=4)   # a、y都是关键字参数
  f(y=6, a=4)   # a、y都是关键字参数
  f(4, 5, 6)   # a、x、y都是位置参数
  f(4, x=5)   # a是位置参数，x是关键字参数
  
  # 输出
  a是：6，x是：1，y是：2，z是：3
  a是：6，x是：1，y是：2，z是：3
  a是：6，x是：1，y是：4，z是：3
  a是：4，x是：1，y是：6，z是：3
  a是：4，x是：5，y是：6，z是：3
  a是：4，x是：5，y是：2，z是：3
  ```
  **注意**:
  - 关键字参数是针对实参而言的，只有在函数调用时才会有关键字参数  
  - 在函数调用时，关键字参数必须在位置参数的后面；但是关键字参数的顺序并不重要  

- 位置参数  
  函数调用时根据函数定义时的参数位置来传递参数  
  - 在函数定义时，按照从左至右的顺序一次定义形参，即位置形参  
  - 在函数调用时，按照从左至右的顺序一次定义实参，即位置实参  
  **注意**：位置实参必须和位置形参一一对应，且一个参数都不可以少  
  
## 命名空间、作用域、和变量  
- 命名空间（namespace）：描述变量作用域的名称  
- 变量：
  - 全局变量（global variable）：全局命名空间的变量，可以在整个程序范围内访问  
  - 局部变量（local variable）：局部命名空间的变量，只能在其被声明的函数内部访问  
  - 任何函数中赋值的变量默认都是分配到局部命名空间中的，一般情况下，在函数执行完毕后，局部命名空间就会被销毁  
  ```
  # 输入
  total = 0   # 全局变量


  def sum(arg1, arg2):
      total = arg1 + arg2   # 局部变量，不建议和全局变量同名
      print('函数内的 total：', total)
      return total


  sum(10, 20)
  print('函数外的 total：', total)

  # 输出
  函数内的 total： 30
  函数外的 total： 0
  ```
- `global`和`nonlocal`关键字  
  在函数中修改全局变量的值，必须使用`global`关键字声明成全局变量（不建议频繁使用，可以考虑类）  
  ```
  # 输入
  total = 0   # 全局变量


  def sum(arg1, arg2):
      global total
      total = arg1 + arg2
      print('函数内的 total：', total)
      return total


  sum(10, 20)
  print('函数外的 total：', total)
  
  # 输出
  函数内的 total： 30
  函数外的 total： 30
  ```
  
## 返回多个值
```
# 输入
def f():
    a = 5
    b = 6
    c = 7
    return a, b, c   # 函数其实返回的是一个元组，最后该元组会被拆包到各个结果变量中


x, y, z = f()
print(x, y, z)
result = f()
print(result, type(result))

# 输出
5 6 7
(5, 6, 7) <class 'tuple'>
```
```
def f():
    a = 5
    b = 6
    c = 7
    return {'a' : a, 'b' : b, 'c' : c}   # 返回的是字典类型


result = f()
print(result, type(result))

# 输出
{'b': 6, 'a': 5, 'c': 7} <class 'dict'>   # 字典中每个键值对的顺序是随机的
```

## 函数也是对象
```
# 输入
# 对数据进行清洗工作
import re


def clean_strings(strings):
    result = []
    for value in strings:
        value = value.strip()   # 清洗空白符
        value = re.sub('[!#?]', '', value)   #清洗指定标点符号
        value = value.title()   # 将首字母大写
        result.append(value)
    return result


states = ['   Alabama  ', 'Georgial!', ' china', ' Jap##en']
cleaned_states = clean_strings(states)
print(cleaned_states)

# 输出
['Alabama', 'Georgial', 'China', 'Japen']
```
其实，还可以将给定字符串上的操作做成一个列表，可以使一系列清洗操作更具可复用性：  
```
import re


# 定义清洗指定标点符号的函数
def remove_punctuation(value):
    return re.sub('[!#?]', '', value)


def clean_strings(strings, ops):
    result = []
    for value in strings:
        for function in ops:
            value = function(value)
        result.append(value)
    return result


# 定义清洗操作的函数列表
clean_ops = [str.strip, remove_punctuation, str.title]
states = ['   Alabama  ', 'Georgial!', ' china', ' Jap##en']
cleaned_states = clean_strings(states, clean_ops)
print(cleaned_states)
```
