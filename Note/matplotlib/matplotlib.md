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
matplotlib.pyplot.savefig(fname[, dpi=None, facecolor='w', edgecolor='w',
                          orientation='portrait', papertype=None, format=None,
                          transparent=False, bbox_inches=None, pad_inches=0.1,
                          frameon=None, metadata=None])
```

### 1.2 show()

显示图片

语法：  
```py
matplotlib.pyplot.show([*, block=None])
```

### 1.3 xlabel() 和 ylabel()

设置 x，y 轴的标题  

语法：  
```py
matplotlib.pyplot.xlabel(xlabel[, fontdict=None, labelpad=None, *, loc=None, **kwargs])
matplotlib.pyplot.ylabel(ylabel[, fontdict=None, labelpad=None, *, loc=None, **kwargs])
```

### 1.4 title()

设置图片标题  

语法：  
```py
matplotlib.pyplot.title(label[, fontdict=None, loc=None, pad=None, *, y=None, **kwargs])
```

### 1.5 legend()

解释不同的图例代表的意义  

语法：  
```py
legend(*args, **kwargs)
```

### 1.6 xticks() 和 yticks()
获得或者设置 x 轴和 y 轴的坐标位置及标签

- 语法  
```py
matplotlib.pyplot.xticks(ticks=None, labels=None, **kwargs)
matplotlib.pyplot.yticks(ticks=None, labels=None, **kwargs)
```

参数说明：  
ticks -- 数组、列表等类型；位置列表，传递一个空列表会删除所有刻度位置（**可选**）  
labels -- 数组、列表等类型；要放置在给定刻度位置的标签，只有在同时传递了刻度线时，才能传递此参数（**可选**）  
**kwargs -- 文本属性，可用于控制标签的外观  

返回值：  
locs -- 刻度位置的列表  
labels -- 刻度标签列表的对象

- 调用方法（Call signatures）  
```py
locs, labels = xticks()            # 获取 x 轴刻度的位置和标签
locs, labels = yticks()            # 获取 y 轴刻度的位置和标签

xticks(ticks, [labels], **kwargs)  # 设置 x 轴刻度的位置和标签
yticks(ticks, [labels], **kwargs)  # 设置 y 轴刻度的位置和标签
```

- 实例  
```py
import numpy as np
import matplotlib.pyplot as plt

locs, labels = plt.xticks()        # 获取 x 轴刻度的位置和标签
plt.xticks(np.arange(0, 10, 2))    # 设置 x 轴刻度的位置
plt.xticks([0, 1, 2], ['January', 'February', 'March'])   # 设置 x 轴刻度的位置和标签
plt.xticks([0, 1, 2], ['January', 'February', 'March'],
           rotation=45)            # 设置 x 轴刻度的位置，标签和属性
plt.xticks([])                     # 删除 x 轴刻度的位置
```

### 1.7 text()
给图像 x, y 位置处添加文本 s  

- 语法  
```py
matplotlib.pyplot.text(x, y, s, fontdict=None, **kwargs)
```

参数说明：  
x, y -- 浮点型；设置文本的位置  
s -- 需要设置的文本信息  
fontsize -- 用于覆盖默认文本属性的字典  
**kwargs -- 文本属性，可用于控制文本的外观  

- 实例  
```py
import matplotlib.pyplot as plt

plt.text(i, j + 0.1, j, fontsize=12, ha='center')
```

## 2、散点图

- 语法  
```py
matplotlib.pyplot.scatter(x, y, s=None, c=None, marker=None, cmap=None,
                          norm=None, vmin=None, vmax=None, alpha=None,
                          linewidths=None, *, edgecolors=None,
                          plotnonfinite=False, data=None, **kwargs)
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

## 3、折线图

- 语法  
```py
matplotlib.pyplot.plot(*args[, scalex=True, scaley=True, data=None, **kwargs])
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

## 4、条形图 or 柱状图

- 语法  
```py
matplotlib.pyplot.bar(x, height, width=0.8, bottom=None, *, align='center',
                      data=None, **kwargs)
```

- 实例  
```py
x = ['aa', 'bb', 'cc', 'dd', 'ee', 'ff', 'gg', 'hh']
y = [2.3, 3.4, 1.2, 6.6, 7.0, 5.7, 4.6, 3.9]
plt.bar(x, y)
plt.xlabel('state')
plt.ylabel('GDP')
plt.title('GDP for each state')
plt.xticks(rotation=45)

# 用列表 x 的坐标作为横坐标
# for i in range(len(x)):
#     plt.text(i, y[i] + 0.1, y[i], fontsize=12, ha='center')

# 用列表 x 的值作为横坐标
# for i in range(len(x)):
#     plt.text(x[i], y[i] + 0.1, y[i], fontsize=12, ha='center')

# 用列表 x 的坐标作为横坐标，并且使用 zip() 函数进行打包
# for i, j in zip(range(len(x)), y):
#     plt.text(i, j + 0.1, j, fontsize=12, ha='center')

# 用列表 x 的值作为横坐标，并且使用 zip() 函数进行打包
for i, j in zip(x, y):
    plt.text(i, j + 0.1, j, fontsize=12, ha='center')

plt.show()
```

## 5、直方图
直方图和条形图的区别：  
直方图是用面积表示各组频数的多少，矩形的高度表示每一组的频数或频率，宽度则表示各组的组距，因此其高度与宽度均有意义；其次，由于分组数据具有连续性，直方图的各矩形通常是连续排列。  
条形图矩形的宽度不具有实际的意义，可以随意调节，因此是分开排列的  

- 语法  
```py
matplotlib.pyplot.hist(x, bins=None, range=None, density=False, weights=None,
                       cumulative=False, bottom=None, histtype='bar',
                       align='mid', orientation='vertical', rwidth=None,
                       log=False, color=None, label=None, stacked=False, *, 
                       data=None, **kwargs)
```

常用参数说明：  
x -- 数组或序列；输入值  
bins -- 整数、序列或字符串；  
        当为整数时，从 xmin 开始，每次增加 (xmax - xmin)/bins 的范围进行分布统计；   
        当为序列时，范围按照左闭右开的区间进行分布统计；  
denisty -- False（**默认**）或 True；按照统计频率的方式进行分布显示  
weights -- 类数组型；  
           给频数加权重；当 denisty=True 时，权重会进行归一化，保证频率之和为1  
orientation -- 'vertical'(**默认**) 或 'horizontal'  
color -- 单个颜色值或颜色组成的类数组型  

- 实例  
```py
import matplotlib.pyplot as plt

m = [2, 3, 68, 10, 12, 45, 36, 28, 19, 44, 12, 23]
b = [0, 10, 20, 30, 40, 50]
plt.hist(m, b)
plt.show()
```

## 6、饼图
- 语法  
```py
matplotlib.pyplot.pie(x, explode=None, labels=None, colors=None, autopct=None,  
                      pctdistance=0.6, shadow=False, labeldistance=1.1, 
                      startangle=0, radius=1, counterclock=True, 
                      wedgeprops=None, textprops=None, center=0, 0, frame=False,
                      rotatelabels=False, *, normalize=None, data=None)
```

说明：  
- 当 sum(x) >= 1 时，每个扇形所占的面积为圆的 x/sum(x)  
- 当 sum(x) < 1 时，将不会被归一化，x 即为每个扇形所占圆的面积的占比，圆的剩余空白部分将为 1-sum(x)  
- 默认情况下是从 x 轴开始，逆时针进行排列  

常用参数说明：  
x -- 一维类数组类型；每个扇形区域的面积  
explode -- 类数组类型；每个扇形区域的突出的偏移量，不偏移置为 0  
labels -- 列表类型；为每个扇形区域添加列表  
colors -- 类数组类型；为每个扇形区域提供颜色  
autopct -- 字符串类型或可被调用的函数类型；  
           如果是字符串类型，则显示每个扇形区域的百分比（可规定保留的位数）  
           如果是可被调用的函数，则会调用函数  
shadow -- 布尔类型（**默认为 False**）；在饼图下添加阴影  
counterclock -- 布尔类型；设置扇形排列的方向：逆时针（**默认**） or 顺时针  

- 实例  
```py
import matplotlib.pyplot as plt

labels = ['walking', 'driving', 'sleeping', 'relaxing']
slides = [2, 1, 7, 14]
colors_list = ['r', 'y', 'g', 'b']
plt.title('Pie Graph')
plt.pie(slides, labels=labels, shadow=True, colors=colors_list,
        explode=[0.2, 0, 0, 0], autopct='%.2f%%')
plt.show()
```