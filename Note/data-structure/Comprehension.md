# 推导式

## 列表推导式
- 语法  
  ```
  list_comp = [expr for val in collection if condition]
  ```
  其中，过滤条件可以省略
  等价于下面的 for 循环：  
  ```
  result = []
  for val in collection:
      if condition:
          result.append(expr)
  ```

- 实例  
  ```
  # 输入
  strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
  print([x.upper() for x in strings if len(x) > 2])
  
  # 输出
  ['BAT', 'CAR', 'DOVE', 'PYTHON']
  ```
  
## 集合推导式
- 语法  
  ```
  set_comp = {expr for value in collection if condition}
  ```
  其中，过滤条件可以省略  

- 实例  
  ```
  # 输入
  strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
  print({len(x) for x in strings})
  
  # 输出
  {1, 2, 3, 4, 6}
  ```
  
## 字典推导式
- 语法  
  ```
  dict_comp = {key_expr : value_expr for value in collection if condition}
  ```
  其中，过滤条件可以省略  

- 实例  
  ```
  # 输入
  # 创建 strings 列表中字符串的位置及字符串的字典
  strings = ['a', 'as', 'bat', 'car', 'dove', 'python']
  dict = {key : value for (key, value) in enumerate(strings, 1)}
  print(dict)
  
  # 输出
  {1: 'a', 2: 'as', 3: 'bat', 4: 'car', 5: 'dove', 6: 'python'}
  ```
 
