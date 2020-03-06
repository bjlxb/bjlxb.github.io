---
layout: photo
title: PowerShell不兼容Anaconda虚拟环境解决方案
tags:
  - Tool
date: 2020-02-14 23:15:24
categories: Tool
photos:
---
在Windows中PowerShell使用Anaconda虚拟环境时会报错，原因是不兼容，需要使用开源库进行兼容！
<!--more-->

1. 打开Windows PowerShell
<img src="/image/Anaconda/Anaconda-6.png">

2.运行如下命令
```powershell
conda install -n root -c pscondaenvs pscondaenvs
```
<img src="/image/Anaconda/Anaconda-7.png">

3. 上面命令执行结束后，再执行下方命令
```powershell
Set-ExecutionPolicy RemoteSigned
```
执行效果如下：
```powershell
PS C:\Windows\system32> Set-ExecutionPolicy RemoteSigned
 
执行策略更改
执行策略可帮助你防止执行不信任的脚本。更改执行策略可能会产生安全风险，如 https:/go.microsoft.com/fwlink/?LinkID=135170
中的 about_Execution_Policies 帮助主题所述。是否要更改执行策略?
[Y] 是(Y)  [A] 全是(A)  [N] 否(N)  [L] 全否(L)  [S] 暂停(S)  [?] 帮助 (默认值为“N”): Y
PS C:\Windows\system32>
```
