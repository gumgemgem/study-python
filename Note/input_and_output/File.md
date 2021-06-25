# 文件方法

## open()
- 描述  
  `open()`方法用于打开一个文件，并返回文件对象；如果文件对象无法被打开，则会抛出`OSError`  
  **注意**：使用`open()`方法结束后一定要保证关闭文件对象，即调用`close()`方法  
  
- 语法  
  ```py
  open(file, [mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None])
  ```
  参数说明：  
  - file: 文件路径（相对或者绝对路径）（**必需**）  
  - mode: 可选，文件打开模式（**常用**）  
  - buffering: 设置缓冲  
  - encoding: 一般使用utf8  
  - errors: 报错级别  
  - newline: 区分换行符  
  - closefd: 传入的file参数类型
  - opener: 设置自定义开启器，开启器的返回值必须是一个打开的文件描述符  
  
  `mode`常用参数：  
  - 'r'：只读模式（**默认**）  
  - 'w'：只写模式。如果该文件已经存在则**从头**开始编辑，即原有内容将会被删除；如果文件不存在，将创建新文件  
  - 'a'：追加到现有文件。如果文件已经存在，文件指针将放在文件的结尾，新的内容将会被写入到已有的内容之后；如果文件不存在，将创建新文件进行写入  
  - 'b'：附加说明某模式用于二进制文件，如 'rb' 或 'wb'  
  - 'r+'：打开一个文件用于读写，文件指针将放在文件的开头，如果文件不存在则会报错  
  - 'w+'：打开一个文件用于读写，文件指针将放在文件的开头，如果文件不存在则创建新文件  
  - 'a+'：打开一个文件用于读写，文件指针将放在文件的结尾，如果文件不存在则创建新文件  
  
  关于 'r+' 和 'a+'：  
  - 用 'r+' 打开文件：  
    1. 文件一打开即用`write()`，则**从头**开始覆盖写  
    2. 文件打开后用`seek()`指定文件指针的位置，再执行`write()`，则**从指针位置**开始覆盖写  
    3. 文件打开后执行了`readline()`，再执行`write()`，则**从文件结尾**实现附加写  
    ```py
    '''
    访问文件：example.csv
    文件内容：
    abcdefg
    hijk
    lmn
    opq
    rst
    uvwxyz
    '''
    
    # 输入
    with open('example.csv', 'r+') as f:
        print('访问的文件名为：', f.name)
        print('文件指针位置： ', f.tell())
        f.write('123456\n')
        print('文件指针位置： ', f.tell())
        print('文件关闭前的文件内容：', f.readlines())
        print('文件指针位置： ', f.tell())

    with open('example.csv', 'r') as f:
        print('文件关闭后的文件内容：\n{}'.format(f.read()))
        
    # 输出
    访问的文件名为： example.csv
    文件指针位置：  0
    文件指针位置：  7
    文件关闭前的文件内容： ['\n', 'hijk\n', 'lmn\n', 'opq\n', 'rst\n', 'uvwxyz\n']
    文件指针位置：  32
    文件关闭后的文件内容：
    123456

    hijk
    lmn
    opq
    rst
    uvwxyz

    ```
    ```py
    '''
    访问文件：example.csv
    文件内容：
    abcdefg
    hijk
    lmn
    opq
    rst
    uvwxyz
    '''
    
    # 输入
    with open('example.csv', 'r+') as f:
        print('访问的文件名为：', f.name)
        print('文件指针位置1： ', f.tell())
        print(f.readline())
        print('文件指针位置2： ', f.tell())
        f.write('123456\n')
        print('文件指针位置3： ', f.tell())
        print('文件关闭前的文件内容：', f.readlines())
        print('文件指针位置4： ', f.tell())

    with open('example.csv', 'r') as f:
        print('文件关闭后的文件内容：\n{}'.format(f.read()))
        
    # 输出
    访问的文件名为： example.csv
    文件指针位置1：  0
    abcdefg

    文件指针位置2：  8
    文件指针位置3：  39
    文件关闭前的文件内容： ['hijk\n', 'lmn\n', 'opq\n', 'rst\n', 'uvwxyz\n']
    文件指针位置4：  39
    文件关闭后的文件内容：
    abcdefg
    hijk
    lmn
    opq
    rst
    uvwxyz
    123456

    ```
  
  - 用 'a+' 打开文件：  
    1. 文件打开后指针的起始位置为文件末尾  
    2. `write()`始终是附加写，即使将文件指针指到中间再执行`write()`仍然是**附加写**
    ```py
    # 输入
    with open('example.csv', 'w') as f:
        f.write('0123456789abcd')

    with open('example.csv', 'a+') as f:
        f.write('efg')
        print('当前文件的内容：', f.read())   # 当文件的指针在文件结尾，read()将返回空字符串
        f.seek(0, 0)
        print('当前文件指针的位置1：', f.tell())
        f.write('hijk')
        print('当前文件指针的位置2：', f.tell())
        f.seek(0, 0)   # 文件的指针移到文件开头
        print('当前文件的内容：', f.read())
    
    # 输出
    当前文件的内容： 
    当前文件指针的位置1： 0
    当前文件指针的位置2： 21
    当前文件的内容： 0123456789abcdefghijk
    ```
    
- 实例  
  ```py
  f = open('example.csv')
  for line in f:
      print(line)

  f.close()
  ```
  
- `with`语句  
  `with`语句更容易清理打开的文件，这样可以在退出代码块时自动关闭文件，避免出现文件忘关的情况  
  ```python3
  with open('example.csv', 'r') as f:
      for line in f:
          print(line)
  ```
  
## file 对象的方法
#### read()
- 描述  
  从文件读取指定的字节数，包括 "\n"，如果未给定或者为负数则读取所有  
  
- 语法  
  ```py
  fileObject.read([size])
  ```
  size -- 从文件中读取的字节数，默认为-1，表示读取整个文件  

- 实例   
  ```py
  '''
  访问文件：example.csv
  文件内容：
  在这个世界上，
  一星陨落，
  黯淡不了星空灿烂，
  一花凋零，
  荒芜不了整个春天。
  '''
  
  # 输入
  with open('example.csv') as f:
      print('访问的文件名为：', f.name)
      line = f.read(10)
      print(line)
      
  # 输出
  访问的文件名为： example.csv
  在这个世界上，
  一星
  ```

#### readline()
- 描述  
  从文件读取整行，包括 "\n" 字符
  
- 语法  
  ```py
  fileObject.readline([size])
  ```
  size -- 从文件中**某行**读取的字节数，包括 "\n" 字符；当给定参数超过了该行的字节数，则返回一整行即止  

- 实例  
  ```py
  '''
  访问文件：example.csv
  文件内容：
  在这个世界上，
  一星陨落，
  黯淡不了星空灿烂，
  一花凋零，
  荒芜不了整个春天。
  '''
  
  # 输入
  with open('example.csv') as f:
      print('访问的文件名为：', f.name)
      line = f.readline()
      print(line)
      words = f.readline(10)
      print(words)
      print(len(words))
  
  # 输出
  访问的文件名为： example.csv
  在这个世界上，

  一星陨落，

  6
  ```

#### readlines()
- 描述  
  读取文件中所有的行并返回**列表**  

- 语法  
  ```py
  fileObject.readlines()
  ```

- 实例  
  ```py
  '''
  访问文件：example.csv
  文件内容：
  在这个世界上，
  一星陨落，
  黯淡不了星空灿烂，
  一花凋零，
  荒芜不了整个春天。
  '''
  
  # 输入
  with open('example.csv') as f:
      print('访问的文件名为：', f.name)
      lines = f.readlines()
      print(lines)
      for line in lines:
          print(line, end='')
          
  # 输出
  访问的文件名为： example.csv
  ['在这个世界上，\n', '一星陨落，\n', '黯淡不了星空灿烂，\n', '一花凋零，\n', '荒芜不了整个春天。\n']
  在这个世界上，
  一星陨落，
  黯淡不了星空灿烂，
  一花凋零，
  荒芜不了整个春天。
  ```

#### tell()
- 描述  
  返回文件的当前位置，即文件指针当前的位置  
  - 表示为**二进制模式**下时从文件开始的字节数，以及**文本模式**下的意义不明的数字  
  - `tell()`函数把`\n`换行符当成一个字符而不是两个字符  

- 语法  
  ```py
  fileObject.tell()
  ```
  返回值 -- 返回文件指针当前的位置  

- 实例  
  ```
  '''
  访问文件：example.csv
  abcdefg
  hijk
  lmn
  opq
  rst
  uvwxyz
  '''
  
  # 输入
  with open('example.csv', 'r+') as f:
      print('访问的文件名为：', f.name)
      print(f.tell())
      print(f.readline(), end='')
      print(f.tell())
      print(f.readline(), end='')
      print(f.tell())
  
  # 输出
  访问的文件名为： example.csv
  0
  abcdefg
  8
  hijk
  13
  ```

#### write()
- 描述  
  向文件中写入指定字符串  
  - 在文件关闭前或缓冲区刷新前，字符串内容存储在缓冲区中，这时在文件中是看不到写入的内容的  
  - 如果文件是以二进制的模式打开的（即打开模式带 'b'），参数`str`要用 encode 方法转化为 bytes 模式，即`b(str)`  
  - `write()`无法实现插入写，只能进行覆盖写或附加写  
  
- 语法  
  ```py
  fileObject.write([str])
  ```
  返回值 -- 返回写入字符串的长度  
  
- 实例  
  ```py
  ‘’‘
  example.csv 文件已存在于本地端，当用 'w' 的模式打开时，文件原本的内容将会清空
  ’‘’
  
  # 输入
  with open('example.csv', 'w') as f:
      f.write('Hello World!\n')

  with open('example.csv', 'r') as f:
      print(f.read())
      
  # 输出
  Hello World!
  
  ```

#### writelines()
- 描述  
  向文件中写入一序列的字符串。序列字符串可以是由迭代对象产生的，如一个字符串列表  

- 语法  
  ```py
  fileObject.writelines([seq])
  ```
  seq -- 要写入文件的字符串序列  
  返回值 -- 无返回值
  
- 实例  
  ```py
  ‘’‘
  example.csv 文件已存在于本地端，当用 'w' 的模式打开时，文件原本的内容将会清空
  ’‘’
  
  # 输入
  seq = ['Hello World!\n', '你好 世界！']
  with open('example.csv', 'w') as f:
      f.writelines(seq)

  with open('example.csv', 'r') as f:
      print(f.read())
      
  # 输出
  Hello World!
  你好 世界！
  ```
  
#### seek()
- 描述  
  用于移动文件读取指针到指定位置  

- 语法  
  ```py
  fileObject.seek(offset[, whence])
  ```
  
  参数说明：  
  offset -- 开始的偏移量。也就是代表需要移动偏移的字节数，如果是负数表示从倒数第几位开始  
  whence -- **可选**，默认值为 0，表示从哪个位置开始偏移。0 ：从文件开头开始算起；1 ：从当前位置开始算起；2 ：从文件末尾开始算起  
  
  返回值：  
  如果操作成功，则返回新的文件的位置；如果操作失败，则返回 -1  

- 实例  
  ```py
  ’‘
  example.csv 文件已存在于本地端，当用 'w' 的模式打开时，文件原本的内容将会清空
  ’‘’
  
  # 输入
  with open('example.csv', 'wb+') as f:
      f.write(b'0123456789abcdef')
      f.seek(5)   # 移动到文件的第6个字节
      print(f.read(1))
      f.seek(-3, 2)   # 移动到文件倒数第三个字节
      print(f.read(1))
      
  # 输出
  b'5'
  b'd'
  ```
