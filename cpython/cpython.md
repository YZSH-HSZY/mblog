# cpython
一个python的c语言解释器，同样的python解释器实现还有jython、pypy等

[github官网](https://github.com/python/cpython)

## 准备
在学习python的过程中，我对python的一些工作细节感到困惑，因此有了本文。在这里我将学习cpython源码的一些细节记录在下面:

**环境** cpython 3.12.3,ubuntu 20.04 in wsl2,gun/gcc系列编译器
**注意** cpython在编译安装时，需要已有pyhton环境

## cpython编译
在进行cpython的编译时，需要注意可能缺少相应的依赖项，可以使用`apt search`和`apt-file`命令找到包在机器上的安装名和文件存在与那些包中。

这里列出一些需要的安装包
- build-essential 包含一系列的C/C++开发工具，主要为GNU系列编译器
- python3-pip python的pip包管理器
- manpages-dev 适用于开发环境的man手册(包含系统调用和库调用的介绍信息)
- pkg-config 管理库的编译和链接标志的工具，在项目包含依赖库时有用
- cmake 一个简易的、生成makefile文件的项目构建工具
- gdb GNU系列的调试器，进行源码调试的工具

### 编译过程中报缺少模块的错误

一般是由于缺少头文件造成的，可以通过`find`查看有无对应头文件，无则需要安装开发库，可通过`apt-file`搜索可安装包，以下是一些模块对应缺少的依赖库

- no module _ssl
    安装tk-itk4-dev tcl-itcl4-dev libssl-dev
- ctype
    libffi-dev
- readline
    [libreadline-dev | lib32readline-dev]
- _bz2
    libbz2-dev
     介绍:
      high-quality block-sorting file compressor library- development(高质量的块排序文件压缩程序库-开发)
- _lzma
    liblzma-dev
     介绍:
      XZ-format compression library(xz格式的压缩算法库)
      注意: 5.6.0,5.6.1版本中存在xz安全漏洞,请安装低版本
- _gdbm _dbm
    libgdbm-dev libgdbm-compat-dev
     介绍:
      dbm: kv型数据库  
      libgdbm-dev: GNU dbm database routines(GNU数据库例程)
      libgdbm-compat-dev: legacy support development files(遗留支持开发文件)。解决无dbm.h文件问题    

**注意** `apt-file`需要使用`apt install apt-file`安装，并且使用`apt-file update`更新数据库之后，才能使用。

## cpython源码分析

## 分析实例