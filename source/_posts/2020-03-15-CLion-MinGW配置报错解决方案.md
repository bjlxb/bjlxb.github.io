---
layout: photo
title: CLion+MinGW配置报错解决方案
tags:
  - Tool
date: 2020-03-15 22:18:51
categories: Tool
photos:
---
在学习C/C++过程中，使用了Clion工具，安装后配置了MinGW直接报错了，无法正常运行，后来在jetbrains网站中找到了全英文的解决方案，记录一下，方便以后查看！
<!--more-->
#### 一、报错信息
```
CMake Error at D:/Develop/JetBrains/CLion/bin/cmake/win/share/cmake-3.15/Modules/CMakeTestCCompiler.cmake:60 (message):
  The C compiler

    "C:/Soft/mingw64/bin/gcc.exe"

  is not able to compile a simple test program.

  It fails with the following output:

    Change Dir: C:/Users/鏂版尝/CLionProjects/test/cmake-build-debug/CMakeFiles/CMakeTmp
    
    Run Build Command(s):C:/Soft/mingw64/bin/mingw32-make.exe cmTC_52a6a/fast && C:/Soft/mingw64/bin/mingw32-make.exe -f CMakeFiles\cmTC_52a6a.dir\build.make CMakeFiles/cmTC_52a6a.dir/build
    mingw32-make.exe[1]: Entering directory 'C:/Users/鏂版尝/CLionProjects/test/cmake-build-debug/CMakeFiles/CMakeTmp'
    Building C object CMakeFiles/cmTC_52a6a.dir/testCCompiler.c.obj
    C:\Soft\mingw64\bin\gcc.exe    -o CMakeFiles\cmTC_52a6a.dir\testCCompiler.c.obj   -c C:\Users\閺傜増灏漒CLionProjects\test\cmake-build-debug\CMakeFiles\CMakeTmp\testCCompiler.c
    gcc.exe: error: C:\Users\閺傜増灏漒CLionProjects\test\cmake-build-debug\CMakeFiles\CMakeTmp\testCCompiler.c: No such file or directory
    gcc.exe: fatal error: no input files
    compilation terminated.
    mingw32-make.exe[1]: *** [CMakeFiles\cmTC_52a6a.dir\build.make:65: CMakeFiles/cmTC_52a6a.dir/testCCompiler.c.obj] Error 1
    mingw32-make.exe[1]: Leaving directory 'C:/Users/鏂版尝/CLionProjects/test/cmake-build-debug/CMakeFiles/CMakeTmp'
    mingw32-make.exe: *** [Makefile:120: cmTC_52a6a/fast] Error 2
```
#### 二、问题原因
  并不是CLion的问题，是因为使用CMake + MinGW的原因，CMake + MinGW不支持非拉丁符号。

#### 三、解决方案
  1. 首先创建一个文件夹，所处的路径不能有非拉丁符号（例：D:\tmp）。
  2. 在CLion中，选择Help-->Edit Custom VM options...-->create。
  3. 在打开的文件中最后一行添加指定内容：-Djava.io.tmpdir=<path_to_temp_folder> (例： -Djava.io.tmpdir=D:/tmp)。
  4. 在CLion中，选择File-->Save All。
  5. 重启CLion

注：
  如果你的项目路径有非拉丁符号，要将生成目录移动到全部是拉丁符号的路径下。两种方案：
  1. 在CLion中修改File-->Settings-->Build, Execution, Deployment-->CMake-->Generation path。
  2. 将项目放到全部是拉丁符号的路径下。

[参考链接](https://intellij-support.jetbrains.com/hc/en-us/community/posts/360003475400-CLion-MinGW-Test-CMake-run-finished-with-errors)

