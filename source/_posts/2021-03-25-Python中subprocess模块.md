---
layout: photo
title: Python中subprocess模块
tags:
  - Python
date: 2021-03-25 15:52:09
categories: Python
photos:
---
Python中subprocess模块使用教程
<!--more-->
subprocess 模块允许你生成新的进程，连接它们的输入、输出、错误管道，并且获取它们的返回码。此模块打算代替一些老旧的模块与功能：
```python
os.system
os.spawn*
```

## 使用 [`subprocess`](https://docs.python.org/zh-cn/3/library/subprocess.html#module-subprocess) 模块

推荐的调用子进程的方式是在任何它支持的用例中使用 run() 函数。对于更进阶的用例，也可以使用底层的 Popen 接口。

### subprocess模块中的常用函数

| 函数                            | 描述                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| subprocess.run()                | Python 3.5中新增的函数。执行指定的命令，等待命令执行完成后返回一个包含执行结果的CompletedProcess类的实例。 |
| subprocess.call()               | 执行指定的命令，返回命令执行状态，其功能类似于os.system(cmd)。 |
| subprocess.check_call()         | Python 2.5中新增的函数。 执行指定的命令，如果执行成功则返回状态码，否则抛出异常。其功能等价于subprocess.run(..., check=True)。 |
| subprocess.check_output()       | Python 2.7中新增的的函数。执行指定的命令，如果执行状态码为0则返回命令执行结果，否则抛出异常。 |
| subprocess.getoutput(cmd)       | 接收字符串格式的命令，执行命令并返回执行结果，其功能类似于os.popen(cmd).read()和commands.getoutput(cmd)。 |
| subprocess.getstatusoutput(cmd) | 执行cmd命令，返回一个元组(命令执行状态, 命令执行结果输出)，其功能类似于commands.getstatusoutput()。 |

**说明：**

1. 在Python 3.5之后的版本中，官方文档中提倡通过subprocess.run()函数替代其他函数来使用subproccess模块的功能；
2. 在Python 3.5之前的版本中，我们可以通过subprocess.call()，subprocess.getoutput()等上面列出的其他函数来使用subprocess模块的功能；
3. subprocess.run()、subprocess.call()、subprocess.check_call()和subprocess.check_output()都是通过对subprocess.Popen的封装来实现的高级函数，因此如果我们需要更复杂功能时，可以通过subprocess.Popen来完成。
4. subprocess.getoutput()和subprocess.getstatusoutput()函数是来自Python 2.x的commands模块的两个遗留函数。它们隐式的调用系统shell，并且不保证其他函数所具有的安全性和异常处理的一致性。并且，从Python 3.3.4开始才支持Windows平台。



```python
subprocess.run(args, *, stdin=None, input=None, stdout=None, stderr=None, capture_output=False, shell=False, cwd=None, timeout=None, check=False, encoding=None, errors=None, text=None, env=None, universal_newlines=None, **other_popen_kwargs)

```



<img src="/image/">

