---
layout: photo
title: Python3.8中tornado报错NotImplementedError
tags:
  - Python
date: 2020-08-13 21:04:16
categories: Python
photos:
---
在Python3.8环境运行Tornado，记录一下报错原因和解决方案！
<!--more-->
#### 一. 报错信息
```python
Traceback (most recent call last):
  File ".\index.py", line 325, in <module>
    app.listen(port)
  File "C:\Program Files\Python38\lib\site-packages\tornado\web.py", line 2112, in listen
    server.listen(port, address)
  File "C:\Program Files\Python38\lib\site-packages\tornado\tcpserver.py", line 152, in listen
    self.add_sockets(sockets)
  File "C:\Program Files\Python38\lib\site-packages\tornado\tcpserver.py", line 165, in add_sockets
    self._handlers[sock.fileno()] = add_accept_handler(
  File "C:\Program Files\Python38\lib\site-packages\tornado\netutil.py", line 279, in add_accept_handler
    io_loop.add_handler(sock, accept_handler, IOLoop.READ)
  File "C:\Program Files\Python38\lib\site-packages\tornado\platform\asyncio.py", line 99, in add_handler
    self.asyncio_loop.add_reader(fd, self._handle_events, fd, IOLoop.READ)
  File "C:\Program Files\Python38\lib\asyncio\events.py", line 501, in add_reader
    raise NotImplementedError
NotImplementedError
```
#### 二. 报错原因：
  python3.8的asyncio 在 Windows 上默认使用 ProactorEventLoop 造成的，而不是之前的 SelectorEventLoop。jupyter 依赖 tornado，而 tornado 在 Window 上需要使用 SelectorEventLoop，所以报错。
详细信息请查看官方文档：[官方文档](https://www.tornadoweb.org/en/stable/index.html#installation)

#### 三. 解决方案：
在Windows下进行单独处理
```python
# windows 系统下 tornado 使用 使用 SelectorEventLoop
import platform

if platform.system() == "Windows":
    import asyncio
    asyncio.set_event_loop_policy(asyncio.WindowsSelectorEventLoopPolicy())
```

