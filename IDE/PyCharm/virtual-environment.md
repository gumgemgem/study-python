# 虚拟环境（Virtualenv）

## 1、为什么要使用虚拟环境？
virtualenv 为应用提供了隔离的 Python 运行环境，解决了不同应用间多版本的冲突问题  
- 不同的项目需要的解释器版本可能不同，如有的要求：Python3.7，有的要求：Python3.8  
- 不同项目需要安装的包的版本不同  
- 将当前项目使用的 packages 与 base interpreter 中的 packages 进行隔离，当前项目使用的 packages 都安装在虚拟环境的 venv 文件夹中解释器的 site-packages 中，防止由于项目过多安装过多包对 base interpreter 环境的污染  

## 2、关于是否 Inherit global site-packages？
[详情见](https://www.jianshu.com/p/b4629ee87e80)  
- 勾选 Inherit global site-packages  
venv/bin 目录中不含有 pip 或 easy_install 的相关文件，在虚拟环境下，安装包时会直接安装到 base interpreter 的 site-packages 中，从而污染了 base interpreter 的环境  

- 不勾选 Inherit global site-packages  
venv/bin 目录中含有 pip 或 easy_install 的相关文件，在虚拟环境下，使用 pip/python install/easy_install安装包时会直接安装到 base interpreter 的 site-packages 中，从而污染了 base interpreter 的环境  