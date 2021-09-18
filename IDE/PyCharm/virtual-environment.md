# 虚拟环境

[如何创建虚拟环境](https://www.jetbrains.com/help/pycharm/creating-empty-project.html)  
[PyCharm 项目环境配置](https://blog.chintsan.com/archives/149)

Loction -- 第一个 Location 表示项目所在的目录  
New environment using -- 选择 Virtualenv  
Loction -- 第二个 Location 表示虚拟环境所在的目录，会自动根据第一个 Loction 自动生成  
Base interpreter -- 需要使用的 Python 环境  
Inherit global site-packages -- 是否使用全局环境安装的包（**一般勾选**）  
Make available to all projects -- 其它项目是否可以使用当前的虚拟环境（**一般不勾选**）  

## 1. 包管理

### 1.1 查看 Python 安装的库：

- 本地环境  
进入 pip.exe 所在的目录：`Python 安装目录\Scripts`  
打开终端，输入 `pip list`  
**或 **任何路径下打开终端，输入 `python -m pip list`  

- 虚拟环境  
进入虚拟环境的终端，切换到 pip.exe 所在目录：`虚拟环境所在项目\venv\Scripts`  
输入 `pip list`  

**注意**：虚拟环境不可以采用在任何路径下打开终端，输入 `python -m pip list` 的方式，因为此时调用的仍然是本地的 Python 环境  

### 1.2 查看 Python 安装第三方包的路径：

- 本地环境  
进入 pip.exe 所在的目录：`Python 安装目录\Scripts`  
打开终端，输入 `pip -V`  
**或 **任何路径下打开终端，输入 `python -m pip -V`  
**包安装路径**：`Python 安装目录\Lib\site-packages`  

- 虚拟环境  
进入虚拟环境的终端，切换到 pip.exe 所在目录：`虚拟环境所在项目\venv\Scripts`  
输入 `pip list`  
**包安装路径**：`虚拟环境所在项目\venv\Lib\site-packages`  

**结论**：虽然勾选了 Inherit global site-packages，继承了本地的 Python 环境以及安装的第三方包，但虚拟环境中新安装的包仍然是和本地 Python 安装的第三方包隔离的，因此不会污染本地的包环境 