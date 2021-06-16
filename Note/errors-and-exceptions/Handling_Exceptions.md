# 错误和异常处理

## 错误和异常
- 句法错误（或解析错误）  
  句子的语法有错误称为**句法错误**  
  ```
  # 输入
  while True
      print('Hello World!')
  
  # 输出
  File "xxx.py", line xxx
      while True
               ^
  SyntaxError: invalid syntax
  ```

- 异常  
  即使句子的语法是正确的，在运行时也可能发生错误，运行期间检测到的错误被称为**异常**  
  ```
  # 输入
  10 * (1/0)
  
  # 输出
  Traceback (most recent call last):
    File "xxx.py", line xxx
      10 * (1/0)
  ZeroDivisionError: division by zero
  ```
  
## 异常处理
#### try...except...  
```
try:
    执行代码
except：
    发生异常时执行的代码
```
```
# 输入
def attempt_float(x):
    try:
        return float(x)
    except:
        return x


a = attempt_float('123')
b = attempt_float('something')
print(a)
print(b)

# 输出
123.0
something
```
- 可以指定某种异常出现时执行特定语句  
  ```
  # 输入
  def attempt_float(x):
      try:
          return float(x)
      except ValueError:
          return x


  a = attempt_float('123')
  b = attempt_float('something')
  c = attempt_float((1, 2))
  print(a)
  print(b)
  print(c)

  # 输出
  Traceback (most recent call last):
    File "xxx.py", line xxx, in <module>
      c = attempt_float((1, 2))
    File "xxx.py", line xxx, in attempt_float
      return float(x)
  TypeError: float() argument must be a string or a number, not 'tuple'
  ```

- 当不止一种异常时  
  - 可以使用多个`except`语句  
    ```
    # 输入
    def attempt_float(x):
        try:
            return float(x)
        except ValueError:
            return x
        except TypeError:
            print('TypeError：float() argument must be a string or a number!')
            return 0


    a = attempt_float('123')
    b = attempt_float('something')
    c = attempt_float((1, 2))
    print(a)
    print(b)
    print(c)
    
    # 输出
    TypeError：float() argument must be a string or a number!
    123.0
    something
    0
    ```
    
  - 可以用元组包含多个异常  
    ```
    # 输入
    def attempt_float(x):
        try:
            return float(x)
        except (ValueError, TypeError):
            return x


    a = attempt_float('123')
    b = attempt_float('something')
    c = attempt_float((1, 2))
    print(a)
    print(b)
    print(c)
    
    # 输出
    123.0
    something
    (1, 2)
    ```
    
#### try...except...else...
```
try:
    执行代码
except：
    发生异常时执行的代码
else:
    没有异常时执行的代码
```
```
# 输入
def attempt_float(x):
    try:
        float(x)
    except (ValueError, TypeError):
        return x
    else:
        print('Successful conversion!')
        return float(x)


a = attempt_float('123')
print(a)

# 输出
Successful conversion!
123.0
```
**注意**：  
- 使用`else`子句比把所有的语句都放在`try`子句中要好，可以避免`except`中无法捕获的异常  
- 使用`else`子句时，如果`try`子句中需要返回值，那么返回语句需写在`else`语句中，因为函数在执行`return`语句后就默认结束了，后面的`else`语句将不会执行  

#### try-finally
```
try:
    执行代码
except：
    发生异常时执行的代码
else:
    没有异常时执行的代码
finally:
    不论是否有异常都会执行的代码
```
```
# 输入
def attempt_float(x):
    try:
        float(x)
    except (ValueError, TypeError):
        return x
    else:
        print('Successful conversion!')
        return float(x)
    finally:
        print('这句话，无论是否有异常都会执行！')


a = attempt_float('123')
print(a)

# 输出
Successful conversion!
这句话，无论是否有异常都会执行！
123.0
```
**注意**：  
`finally`子句前不是必须有`except`和`else`子句  
