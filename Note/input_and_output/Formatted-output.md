# Formatted output

## 1、%
- 描述  
`%`是一个特殊的操作符，该操作符会将后面的变量值，替换掉前面字符串中的占位符

- 语法  
```py
%[key][flags][width][.precision][length type]conversion type % values
```

说明：  
`'%m.nf' % value` -- value 保留 n 位有效数字，并且总共占据 m 个字符（包括小数点，且 m > n+1 才有意义)  
`'%.nf' % value` -- value 保留 n 位有效数字，不用考虑占位多少字符  
`'%a.nf %b.mf ...' % (value1, value2, ...)` -- 同时结构化输出多个数值  
`'%m.nf%%' % value` -- value 保留 n 位有效数字，并加 % 输出  
`'%m.nf$' % value` -- value 保留 n 位有效数字，并加 $ 输出  

- 实例  
```py
# 输入
print('%7.2f' %99.123456)
print('%.2f' %99.123456)
print('%.2f %.2f' %(99.123456, 99.999999))
print('%.2f%%' %99.123456)
print('%.2f $' %99.123456)

# 输出
  99.12
99.12
99.12 100.00
99.12%
99.12 $
```

## 2、format
- 语法  
```py
'... {[field_name][!conversion][:format_spec]} ...'.format(arguments)
```

说明：  
`'{}'.format(argument)` -- 格式化输出单个变量  
`'{} {} ...'.format(argument1, argument1, ...)` -- 格式化输出单个变量（不按顺序）  
`'{0} {1} ...'.format(argument1, argument1, ...)` -- 格式化输出单个变量（按顺序） 
`'{:m.nf}'.format(value)` -- 四舍五入输出变量值  

- 实例  
```py
# 输入
print('I love {}'.format('China!'))
print('I love {}, and I love {}!'.format('China', 'world'))
print('I love {1}, and I love {0}!'.format('China', 'world'))
# 以下输出中的 0 是必须的，它代表的是后面一整个字典，换成列表等可索引的变量是一样的
print('I love {0[A]}, and I love {0[B]}!'.format({'A': 'China', 'B': 'world'}))
print('I love {A}, and I love {B}!'.format(A='China', B='world'))
print('{:.2f}'.format(99.123456))

# 输出
I love China!
I love China, and I love world!
I love world, and I love China!
I love China, and I love world!
I love China, and I love world!
99.12
```