---
layout: photo
title: Python中pickle用法
tags:
  - Python
date: 2020-03-12 22:57:12
categories: Python
photos:
---
pickle 实现了对一个 Python 对象结构的二进制序列化和反序列化。
<!--more-->
一、pickling和unpickling
pickling将 Python 对象及其所拥有的层次结构转化为一个字节流的过程，而 unpickling是相反的操作。
为了避免混乱，此处采用术语封存 (pickling)和解封 (unpickling)。
注：
 pickle 模块是不安全的。你只应该对你信任的数据进行unpickle操作。
 构建恶意的 pickle 数据来在解封时**执行任意代码**是可能的。绝对不要对不信任来源的数据和可能被篡改过的数据进行解封。
 考虑使用 hmac 来对数据进行签名，确保数据没有被篡改。
 在处理不信任数据时，更安全的序列化格式如 json 可能更为适合。

二、与其他模块关系
1. 与 marshal 间的关系：
 marshal是一个更原始的序列化模块，但pickle 应该在序列化 Python对象时首选。marshal主要是为了支持 Python 的 .pyc 文件。
 
 pickle模块与marshal模块不同点：
 
 1. pickle 模块会跟踪已被序列化的对象，所以该对象之后再次被引用时不会再次被序列化。marshal 不会这么做。
 2. 序列化的类及其实例不能使用marshal。pickle能够透明地存储并保存类实例，然而此时类定义必须能够从与被存储时相同的模块被引入。
 3.  marshal不保证数据能移植到不同的 Python 版本，marshal主要任务是支持 `.pyc` 文件，必要时会以破坏向后兼容的方式更改这种序列化格式，为此 Python 的实现者保留了更改格式的权利。只要 pickle 协议合适，pickle可以在不同版本的 Python 中实现兼容。若pickle在Python 2与Python 3之间使用，封存和解封的代码在 2 和 3 之间是不同的。

2. 与 json 间的比较：
 Pickle 协议和 JSON (JavaScript Object Notation) 本质的不同。
  1. JSON 是一个文本序列化格式（输出 unicode 文本，但大多数情况为 utf-8 编码），而 pickle 是一个二进制序列化格式。
  2. JSON 可阅读，而 pickle 无法阅读。
  3. JSON被大部分语言支持，而pickle则是Python专用的。
  4. JSON 只能表示 Python 内置类型的子集，不能表示自定义的类， pickle 可以表示大量的 Python 数据类型（合理使用 Python 对象内省功能自动地表示大多数类型，复杂情况可以通过实现 specific object APIs）。
  5. pickle对不信任文件进行反序列化可能出现代码执行漏洞，JSON对不信任文件进行反序列化的操作本身不会造成任意代码执行漏洞。
    
```

```

