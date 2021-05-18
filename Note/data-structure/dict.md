# 字典

Introduction and syntax of Directory  

## 1、定义

是一种可变容器模型，且可存储任意类型的对象  
字典是一系列**键值对**的集合（`key: value`），每个键值对之间用逗号进行分割，整个字典包括在`{}`中  
```
d = {key1: value1, key2: value2, key3: value3, ...}
```
说明：  
- 键必须是唯一的，如果一个键被重复赋值，对应的值会被覆盖；值可以不唯一
- 键必须是不可变的数据类型（如字符串、数字、未直接或未间接包括可变对象的元组等）；值可以取任何数据类型  

## 2、初始化

- 创建空字典
  ```
  d = {}
  ```
  或  
  ```
  d = ditc()
  ```

- `{}`创建非空字典
  ```
  d = {key1: value1[, key2: value2, key3: value3, ...]}
  ```
  
- `dict()`将键值对序列构造为字典
  ```
  d1 = dict(([1, 'one'], [2, 'two']))
  d2 = dict([(1, 'one'), (2, 'two')])
  d3 = dict([{1, 'one'}, {2, 'two'}])
  ```
  
## 3、访问

用`[key]`的方式来访问字典中的值  
```
d = {1: 'one', 2: 'two'}
print(d[2])
```

## 4、修改和添加

- 修改字典元素
  可对要修改的元素重新赋值  
  ```
  d = {1: 'one', 2: 'three'}
  d[2] = 'two'
  print(d)
  ```

- 添加字典元素
  在字典中加入新的键值对  
  ```
  d = {1: 'one', 2: 'two'}
  d[3] = 'three'
  print(d)
  ```
  
## 5、清空和删除

- 删除字典中的元素  
  - `del`关键字  
    `del dict[key]`：可以删除键`key`和对应的值`value`
    ```
    # 输入
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    del d[5]
    print(d)
    
    # 输出
    {1: 'one', 2: 'two', 3: 'three', 4: 'four'}
    ```
    
  - `pop`方法  
    `dict.pop(key)`：删除键的同时返回对应的值  
    ```
    # 输入
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    del_value =  d.pop(5)
    print(del_value)
    print(d)
    
    # 输出
    five
    {1: 'one', 2: 'two', 3: 'three', 4: 'four'}
    ```

- 清空字典  
  `clear()`方法可以清空字典中的元素  
  ```
  # 输入
  d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
  d.clear()
  print(d)
  
  # 输出
  {}
  ```
  
- 删除整个字典  
  `del`关键字可以删除整个字典  
  ```
  # 输入
  d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
  del d
  print(d)
  
  # 输出
  NameError: name 'd' is not defined
  ```

## 6、
