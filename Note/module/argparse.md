# argparse  
详细教程请参考：<https://docs.python.org/3/py-modindex.html>

## 1、描述  
命令行选项、参数和子命令解析器  

## 2、步骤  
- 创建一个解析器 [—— ArgumentParser 对象](#3ArgumentParser-对象)
- 添加参数  [—— add_argument() 方法](#4add_argument-方法)
- 解析参数

## 3、ArgumentParser 对象
- 语法
  ```
  class argparse.ArgumentParser(prog=None, usage=None, description=None, epilog=None, parents=[], formatter_class=argparse.HelpFormatter, prefix_chars='-', fromfile_prefix_chars=None, argument_default=None, conflict_handler='error', add_help=True, allow_abbrev=True, exit_on_error=True)
  ```

- 实例
  ```
  import argparse
  parser = argparse.ArgumentParser()
  ```

## 4、add_argument() 方法
- 语法
  ```
  ArgumentParser.add_argument(name or flags...[, action][, nargs][, const][, default][, type][, choices][, required][, help][, metavar][, dest])
  ```
  常用参数说明：  
  - name or flags  
    一个命名（即位置参数）或者一个选项字符串（即可选参数）的**列表**，如：`foo`或者`-f、--foo`，**不可省略**  
    对于可选参数而言，首选第一个出现的长参数名（--开头），如果没有长参数，则选择第一个出现的的短参数名（-开头）  
  
- 实例
  - name or flags
    ```
    import argparse
    parser = argparse.ArgumentParser()
    parser = add_argument('bar')  # 创建位置参数，此时命令行输入参数时必须要含有位置参数
    parser = add_argument('-f', '--foo')  # 创建选项，此时命令行输入参数时可以选择性进行参数传递
    parser.parse_args(['BAR'])  # 输入正确，bar = 'BAR'，foo = None
    parser.parse_args(['BAR', '--foo', 'FOO'])  # 输入正确，bar = 'BAR'，foo = 'FOO'
    parser.parse_args(['BAR', '-f', 'F', '--foo', 'FOO'])  # 输入正确，bar = 'BAR'，foo = 'FOO'
    parser.parse_args(['BAR', '-f', 'F'])  # 输入正确，bar = 'BAR'，foo = 'F'
    parser.parse_args(['-f', 'F'])  # 输入错误，error: the following arguments are required: bar
    ```    
