# 关于自定义安装 Python 和 Anaconda 共存问题

# 1、Python 版本管理

实际上，往往会存在已经自定义安装了 Python，但同时需要安装 Anaconda 的情况，但 Anaconda 中自带 Python，版本管理就十分重要  

Windows Python 版本管理：  

1. 找到自定义安装 Python 和 Anaconda 目录下的 python.exe 应用程序  
2. 分别将 python.exe 复制粘贴在各自的目录下  
3. 分别将 Python 目录下和 Anaconda 目录下的副本重命名 e.g. `python38.exe` 和 `python-ana.exe`  
4. 需要使用哪个版本的 Python，调用对应的 python 应用程序

# 2、pip 版本管理

如果自定义安装 Python 和 Anaconda 同时存在，在未指定所运行的 Python 版本环境时，pip 将会默认安装在 sys.path 环境中，e.g.  

在 Jupyter Notebook 中使用 `!pip install 库名`，库将会安装在 sys.path 下，即自定义安装的 Python 环境中，不会安装在 Anaconda 的 Python 环境中；但导入库时，默认是从 Anaconda 的环境中导入。这样会出现导入库不存在的情况  

pip 版本管理：  

1. 可以直接找到所运行环境中 pip.exe 应用程序所在路径，从该路径下打开终端运行 e.g.   
`!pip install 库名`  
2. 直接在终端的任意路径下或 Jupyter Notebook 中指定 Python 的应用程序，再通过模块启动的方式进行导入 e.g.  
`python38 -m pip install 库名`  
`python-ana -m pip list`  
`!python-ana -m pip install 库名`
3. 关于 Python 的模块启动，详情见 [参考](https://www.cnblogs.com/xueweihan/p/5118222.html)  
(1) `-m` 等价于 `mod`：`run library module as a script (terminates option list)`  
(2) 不论是否有 Python 版本冲突的问题，模块启动的方式都能在任何路径下安装库  