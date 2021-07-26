# Matplotlib

[官方文档](https://matplotlib.org/)

约定导入`Matplotlib`的语法：  
```py
import matplotlib.pyplot as plt
```

## 1、常用函数方法

### matplotlib 显示问题

- windows 系统[（详见）](https://blog.csdn.net/u010472607/article/details/82789887)  
正常显示中文标签：`plt.rcParams['font.sans-serif'] = ['SimHei']`  
正常显示负号：`plt.rcParams['axes.unicode_minus'] = False`


- linux 系统  
[详见](https://www.yuque.com/fcant/python/ptzo53)

### 1.1 savefig()

保存图片  

语法：  
```py
savefig(fname[, dpi=None, facecolor='w', edgecolor='w',
        orientation='portrait', papertype=None, format=None,
        transparent=False, bbox_inches=None, pad_inches=0.1,
        frameon=None, metadata=None])
```

### 1.2 show()

显示图片

语法：  
```py
show([*, block=None])
```

### 1.3 xlabel() 和 ylabel()

设置 x，y 轴的标题  

语法：  
```py
xlabel(xlabel[, fontdict=None, labelpad=None, *, loc=None, **kwargs])
ylabel(ylabel[, fontdict=None, labelpad=None, *, loc=None, **kwargs])
```

### 1.4 title()

设置图片标题  

语法：  
```py
title(label[, fontdict=None, loc=None, pad=None, *, y=None, **kwargs])
```

### 1.5 legend()

解释不同的图例代表的意义  

语法：  
```py
legend(*args, **kwargs)
```

## 2、散点图

- 语法  
```py
plt.scatter(x, y[, s=None, c=None, marker=None, cmap=None, norm=None, vmin=None, vmax=None, alpha=None, linewidths=None, *, edgecolors=None, plotnonfinite=False, data=None, **kwargs])
```

常用参数说明：  
s -- 每个点的大小  
c -- 每个点的颜色  
marker -- 标记的形状  

- 实例  
```py
import numpy as np
import matplotlib.pyplot as plt

arrx = np.arange(6)
arry = np.arange(0, 12, 2)

plt.scatter(arrx, arry, s=100, c='green', marker='*')
plt.show()
```

## 折线图

- 语法  
```py
plt.plot(*args[, scalex=True, scaley=True, data=None, **kwargs])
```

**注意**：当变量是随机生成的一组数或任意一组无序数时，需要先对变量进行排序再定义函数，否则折线图会混乱  

- 实例  
```py
import numpy as np
import matplotlib.pyplot as plt

x = np.arange(6)
y = x ** 2 -1
z = x * 50 + 10

plt.plot(x, y, c='r')
plt.plot(x, z, c='g')
plt.xlabel('week')
plt.ylabel('price')
plt.legend(['Apple', 'IBM'])
plt.show()
```
```py
import numpy as np
import matplotlib.pyplot as plt

random_number = np.random.uniform(0, 100, 10)
random_number.sort()
y = random_number * 10 + 1
z = random_number ** 3 + 20
plt.plot(random_number, y, c='r')
plt.plot(random_number, z, c='g')
plt.show())
```

## 直方图
