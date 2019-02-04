---
title: Cloud desktop configuration
tags: Win10
edit: 2019-02-04
categories: Technology
status: Completed
description: Win10多用户远程登录，不同的电脑使用不同的账号可以同时登录一台windows主机
---

# win10多用户远程登录

**实现效果：不同的电脑可以同时登录一台windows主机，但是必须使用不同的账号**

**注：**需windows专业版

## 首先，我们来创建一个新用户

点击设置，搜索用户

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/01.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/02.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/03.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/04.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/05.png" width="70%">

点击下一步，一个普通用户就创建完成了。



## 配置属性

然后，打开远程设置，右键此电脑，属性，

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/06.png" width="70%">

接下来给这个普通用户添加可以远程登录的权限

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/07.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/08.png" width="70%">

点击检查名称，如果前面出现电脑主机名，表示成功

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/09.png" width="70%">

确认

最后解决多用户同时登录的问题，在cmd中输入gpedit进入本地组策略编辑器

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/10.png" width="70%">

选择【管理模板】->【Windows组件】->【远程桌面服务】->【远程桌面会话主机】->【连接】选择【管理模板】->【Windows组件】->【远程桌面服务】->【远程桌面会话主机】->【连接】

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/11.png" width="70%">

配置 【限制连接的数量】，允许的RD最大连接数 即为最大的连接数量，6个9

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/12.png" width="70%">

 配置【将远程桌面服务用户限制到单独的远程桌面服务会话】，改成 “已禁用”

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/13.png" width="70%">



## 下载配件

下载一个

[链接](https://pan.baidu.com/s/1LRGmZOZTj2WFilUOAhoCbA) 

提取码: wi3g 


运行步骤：install.bat->update.bat->RDPConf.exe

注意，上面三个程序均需要右键以管理员身份运行，且保证电脑网络畅通。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-04-Cloud%20desktop%20configuration/assert/14.png" width="70%">

点击OK，配置结束