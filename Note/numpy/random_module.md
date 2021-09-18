# numpy.random

随机抽样：[官方参考文档](https://numpy.org/doc/stable/reference/random/index.html)

## 1、numpy.random.uniform

均匀分布随机抽样：[官方参考文档](https://numpy.org/doc/stable/reference/random/generated/numpy.random.uniform.html)

- 描述  
从均匀分布中抽取样本  

- 语法  
`numpy.random.uniform(low=0.0, high=1.0, size=None)`

样本均匀分布在左闭右开的区间 [low, high) 中  

参数说明：  
low -- 样本输出区间的下边界，float 型。默认值为 0  
high -- 样本输出区间的上边界，float 型。默认值为 1.0  
size -- 样本输出数目。整型或元组类型，默认为 None，此时返回一个单个值。输入元组类型，如 (m, n, k) ，返回一个 (m, n, k) 大小的数组  

返回值：  
返回标量类型或数组类型  

- 实例  
```py
# 输入
import numpy as np

a = np.random.uniform(0, 1, 5)
print(a)
b = np.random.uniform(0, 100)
print(b)
c = np.random.uniform(5, 10, (2, 3, 4))
print(c)

# 输出
[0.3417705  0.22384181 0.7263551  0.26615417 0.96187706]
39.537835462092254
[[[7.85685382 5.3660959  5.41407574 5.29864553]
  [6.40956568 9.85055153 7.31574784 9.27203565]
  [9.70002114 5.90785374 5.2727908  5.51111132]]

 [[9.10599865 6.61522287 9.43061062 7.76380515]
  [9.18145088 7.72042425 5.71325433 8.04244683]
  [6.56950643 6.42794116 9.02396237 8.54965579]]]
```