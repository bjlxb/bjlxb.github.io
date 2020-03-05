---
layout: photo
title: Windows下Scoop使用
tags:
  - Tool
date: 2020-01-28 19:38:49
categories: Tool
photos:
---

介绍一下Windows下命令行软件管理工具Scoop

<!--more-->
主要是为了Windows上安装软件安装繁琐，路径不统一，而且更新卸载麻烦，包管理系统可以完美的解决这些问题！

目前Windows平台下比较流行的两种包管理平台：
- chocolatey 和 scoop

> Chocolatey中软件安装路径默认在C盘
> scoop自由度高，可以将软件部署到任意盘中

#### 官方信息
- 官方网址:
https://scoop.sh/
- 官方快速入门:
https://github.com/lukesampson/scoop/wiki/Quick-Start

#### 环境准备
操作环境: Windows10 或Windows7 
确保PowerShell 版本 >= 3. win7或许低于3，需要升级。

---

打开PowerShell方式：
	1. win + R 打开运行，输入PowerShell，确定。
	2. cmd中输入PowerShell然后回车。
	3. 在开始菜单中查找。
	4. 开始菜单右键，选择Windows PowerShell或i打开。

1. 命令行查看自己的PowerShell 版本
```powershell
$psversiontable.psversion.major
```
2. 确保你允许PowerShell执行本地脚本
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

执行策略更改
执行策略可帮助你防止执行不信任的脚本。更改执行策略可能会产生安全风险，如 https:/go.microsoft.com/fwlink/?LinkID=135170
中的 about_Execution_Policies 帮助主题所述。是否要更改执行策略?
[Y] 是(Y)  [A] 全是(A)  [N] 否(N)  [L] 全否(L)  [S] 暂停(S)  [?] 帮助 (默认值为“N”): A
```
#### 安装Scoop
1. 不指定安装路径，使用默认安装路径（将会安装到默认目录C:\Users\user(自己的用户名)\scoop）
```powershell
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```
2. 指定安装目录
```powershell
[environment]::setEnvironmentVariable('SCOOP','指定安装路径','User')
$env:SCOOP='指定安装路径'
iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
```

3. 安装scoop可能遇到的错误：

```powershell

使用“1”个参数调用“DownloadString”时发生异常:“基础连接已经关闭: 发送时发生错误。”
所在位置 行:1 字符: 1
+ iex (new-object net.webclient).downloadstring('https://get.scoop.sh')
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], MethodInvocationException
    + FullyQualifiedErrorId : WebException问

```


原因：由于墙的原因无法安装
解决：确保浏览器在能访问到https://get.scoop.sh （使用shadowsocks全局代理）

#### 使用Scoop
在cmd和PowerShell中输入以下命令均可，因为已经为Scoop自动设置了环境变量

###### 常用命令

```powershell
# 帮助语法
scoop help
# 安装操作
scoop install 软件名
# 更新操作（此更新操作是对scoop本身以及bucket库的更新）
scoop update
# 更新所有已安装应用
scoop update *
# 移除所有旧版本
scoop cleanup *
# 卸载操作
scoop uninstall 软件名
```
###### Bucket软件源

scoop的bucket软件源策略，由社区来维护
	1. 社区地址：
	https://github.com/rasa/scoop-directory/blob/master/by-score.md
	2.	bucket语法：
	scoop bucket add [软件源名字(随意)] [源地址]
	3.bucket源推荐：

>     官方：
>     scoop bucket add main # 默认
>     scoop bucket add extras # 推荐
>     scoop bucket add versions
>     scoop bucket add nightlies
>     scoop bucket add nirsoft
>     scoop bucket add php
>     scoop bucket add nerd-fonts
>     scoop bucket add nonportable
>     scoop bucket add java
>     scoop bucket add games
>     scoop bucket add jetbrains # 推荐
>     国内常用软件：
>     微信、QQ、钉钉
>     scoop bucket add dorado https://github.com/h404bi/dorado    

    小新Bucket：
    FSCapture、Shadowsocksrr、UninstallTool、Notepad3、Wechat……
    scoop bucket add dajiu https://github.com/dajiiu/dajiu-scoop
    
    其他：
    scoop bucket add dodorz https://github.com/dodorz/scoop-bucket

###### 常用软件

```powershell
# 01. 7zip：
scoop install 7zip
# 02. git：
scoop install git
# 03.aria2：
scoop install aria2
#04.vim：
scoop install vim
#05.wget：
scoop install wget
#06.everything：
scoop install everything
#07.Q-Dir：
scoop install q-dir
#08.chrome：
scoop install googlechrome
#09.firefox：
scoop install firefox
#10.opera：
scoop install opera
#11.vivaldi：
scoop install vivaldi
#12.python：
scoop install python
#13.golang：
scoop install go
#14.notepadplusplus：
scoop install notepadplusplus
#15.sublime-text：
scoop install sublime-text
#16.vscode：
scoop install vscode
#17.idea：
scoop install idea
#18.pycharm：
scoop install pycharm
#19.goland：
scoop install goland
#20.snipaste：
scoop install snipaste
#21.telegram：
scoop install telegram
#22.typora：
scoop install typora
```
###### 导出软件列表

```powershell
scoop list > F:/scoop/ScoopAppList.txt
```
###### 版本切换

```powershell
scoop reset python
scoop reset python27
```

###### 提高下载速度

1. 建议安装aria2： scoop install aria2 

2. 使用代理(每次进入dos或PowerShell都需设置一遍)： PC端→shadowsocker右键「设置选项」→本地代理下的「允许来自互联网的连接」勾选上 

3. set http_proxy=http://127.0.0.1:1080 set https_proxy=http://127.0.0.1:1080

或：

   在scoop 的配置文件（~/.config/scoop/config.json）中添加

   > scoop config proxy [username:password@]host:port
   > 例如 scoop config proxy 127.0.0.1:1080