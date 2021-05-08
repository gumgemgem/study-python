# Lambda 表达式

- 描述
  可以创建匿名函数  
  - Lambda 只是一个表达式，只能在其中封装有限的逻辑进去
  - Lambda 表达式可以引用包含作用域中的变量
  - Lambda 表达式本质上和普通定义的函数类似，同样都是需要传递参数且具有返回值；调用方式也类似，更加方便地调用时可以给其取一个别名

- 语法
  ```
  lambda [arg1 [,arg2,.....argn]]: expression
  ```

- 实例
  ```
  In[1]: def make_incrementor(n):
             return lambda x: x + n

         f = make_incrementor(42)
         print(f(0), f(1))
         
  Out[1]: 42
          43
          
  In[2]: pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]
         new_pairs = sorted(pairs, key=lambda pair: pair[1])
         print(new_pairs)
         
  Out[2]: [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
  
  In[3]: sum = lambda arg1, arg2: arg1 + arg2   # 给 Lambda 表达式取了一个别名 sum
         print(sum(10, 20))
  
  Out[3]: 30
  ```
