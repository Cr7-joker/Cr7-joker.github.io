---
title: Socket network programming
tags: Socket UDP TCP
edit: 2019-02-11
categories: Python
status: Completed
description: Implement socket network programming in python, use TCP, UDP protocol, and complete file transfer function
---

# What is socket?

•Socket是电脑网络中进程间数据流的端点

•Socket是操作系统的通信机制

•应用程序通过Socket进行网络数据的传输

# 简单TCP过程

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-11-Socket%20network%20programming/assert/TCP.png" width="90%" alt="TCP通信过程">

# Socket通信过程

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-11-Socket%20network%20programming/assert/socket.png" width="90%" alt="socket通信过程">

# Socket通信方式

•Socket分为UDP和TCP两种不同的通信方式

# 为什么是socket？

•Socket能够适应多种网络协议

•服务器传输大量涉及网络协议，离不开socket应用

# Socket参数

**•family：地址簇** 

  socket.AF_INET         IPV4(默认)

  socket.AF_INET6       IPV6

  socket.AF_UNIX        只能够用于单一的unix系统进程间通信

**•type：类型**

  socket.SOCK_STREAM     流式socket，for TCP（默认）

  socket.SOCK_DGRAM       数据报式socket，for UDP

# 文件传输

•遇到文件上传的情况，又没有第三方软件支持的时候

•可以自己实现

# 代码实现

参见[GitHub——（python-socket）](https://github.com/Cr7-joker/python-socket)

有`TCP`和`UDP`两种协议的简单传输，都分为`Client`端和`Server`端，附加`非阻塞TCP传输`代码

还有`文件传输`的代码