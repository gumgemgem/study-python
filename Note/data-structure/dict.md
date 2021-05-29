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
- 键必须是不可变的数据类型即**可哈希性**（如字符串、数字、元素不可变的元组等）；值可以取任何数据类型（可用`hash(object)`检测一个对象是否是可哈希的）

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

## 6、字典的内置函数
[len()、str()、type()](https://github.com/gumgemgem/study-python/blob/main/Note/function/build-in_function.md)

## 7、字典的内置方法
- keys()  
  - 描述  
    按照相同的顺序返回键组合的对象  
    
  - 语法  
    ```
    dict.keys()
    ```
    
  - 实例  
    ```
    # 输入
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    print(d.keys())
    print(list(d.keys()))
    
    # 输出
    dict_keys([1, 2, 3, 4, 5])
    [1, 2, 3, 4, 5]
    ```
    
- values()  
  - 描述  
    按照相同的顺序返回值组合的对象  
    
  - 语法  
    ```
    dict.values()
    ```
    
  - 实例  
    ```
    # 输入
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    print(d.values())
    print(list(d.values()))
    
    # 输出
    dict_values(['one', 'two', 'three', 'four', 'five'])
    ['one', 'two', 'three', 'four', 'five']
    ```
  
- get(key, default=None)  
  - 描述  
    返回指定键的值
    
  - 语法  
    ```
    dict.get(key, defualt=None)
    ```
  
  - 实例  
    ```
    # 输出
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    print(d.get(1))
    print(d.get(6, 'six'))
    
    # 输出
    one
    six
    ```

- setdefault(key, default=None)  
  - 描述  
    返回指定键的值，如果键存在于字典中，则返回对应的值；如果键不存在于字典中，将添加键并将其值设为默认值  
    
  - 语法  
    ```
    dict.setdefault(key, defualt=None)
    ```
  
  - 实例  
    ```
    # 输出
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    print(d.setdefault(1, 'six'))
    print(d.setdefault(6, 'six'))
    print(d)
    
    # 输出
    one
    six
    {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five', 6: 'six'}
    ```
    
- key in dict/ key not in dict  
  - 描述  
    判断键是否存在/不存在于字典中，为真返回 True；为假返回 False

  - 语法  
    ```
    key in dict/key not in dict
    ```
    
  - 实例  
    ```
    # 输入
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}

    if 6 in d:
        print('6在字典d的键中')
    else:
        print('6不在字典d的键中')

    if 6 not in d:
        print('6不在字典d的键中')
    else:
        print('6在字典d的键中')
        
    # 输出
    6不在字典d的键中
    6不在字典d的键中
    ```

- update(dict2)  
  - 描述  
    将字典 dict2 的键值对更新到字典 dict 中  
  
  - 语法  
    dict.update(dict2)
    
  - 实例  
    ```
    # 输入
    d = {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five'}
    d2 = {6: 'six'}
    d.update(d2)
    print(d)
      
    # 输出
    {1: 'one', 2: 'two', 3: 'three', 4: 'four', 5: 'five', 6: 'six'}
    ```
  
## 8、用序列创建字典
- 将两个序列配对组合成字典  
  ```
  mapping = {}
  for key, value in zip(key_list, value_list)
      mapping[key] = value
  ```

- 实例  
  ```
  # 输入
  d = {}
  l1 = [1, 2, 3]
  l2 = ['one', 'two', 'three']
  for key, value in zip(l1, l2):
      d[key] = value
  print(d)
  
  # 输出
  {1: 'one', 2: 'two', 3: 'three'}
  ```
