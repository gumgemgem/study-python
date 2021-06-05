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
 
## 嵌套的列表推导式
- 语法  
  ```
  list_comp = [expr for val1 in collection1 for val2 in colletion2 if condition]
  ```
  其中，过滤条件可以省略  
  以上推导式等价于  
  ```
  lsit_comp = []
  for val1 in collection1:
      for val2 in collection2:
          if condition:
              list_comp.append(val2)
  print(list_comp)
  ```
  注意：  
      - 推导式中 for 循环的顺序与嵌套 for 循环的顺序是一样的  
      - 考虑到代码的可读性，两三个以上的嵌套不建议使用推导式  
  
- 实例  
  ```
  # 输入
  # 找出 all_data 中至少有2个 e 的所有名字
  name_of_interest = [name for names in all_data for name in names if name.count('e') >= 2]
  print(name_of_interest)
  # 等价于
  result = []
  for names in all_data:
      for name in names:
          if name.count('e') >= 2:
              result.append(name)
  print(result)
  
  # 输出
  ['Steven']
  ['Steven']
  ```
  ```
  # 输入
  # 将元组的列表扁平化为一个列表
  some_tuples = [(1, 2, 3), (4, 5, 6), (7, 8, 9)]
  l = [x for tup in some_tuples for x in tup]
  print(l)
  
  # 输出
  [1, 2, 3, 4, 5, 6, 7, 8, 9]
  ```
