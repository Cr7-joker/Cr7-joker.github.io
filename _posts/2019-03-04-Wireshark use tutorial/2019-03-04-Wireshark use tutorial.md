---
title: Wireshark use tutorial
tags: Ansys Network
edit: 2019-03-04
categories: Technology
status: Writing
description: The use tutorial from entry to mastery of network analysis tool Wireshark
---

# 【基础】软件使用调试

# Wireshark安装入门

### 软件介绍

Wireshark（前称Ethereal）是一个[网络封包](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E5%B0%81%E5%8C%85)分析软件。网络封包分析软件的功能是撷取网络封包，并尽可能显示出最为详细的网络封包资料。Wireshark使用WinPCAP作为接口，直接与网卡进行数据报文交换。

Wireshark是目前全球使用最广泛的开源抓包软件(前身为Ethereal)，是一个通用化的网络数据嗅探器和协议分析器，由Gerald Combs编写并于1998年以GPL开源许可证发布。如果是网络工程师，可以通过Wireshark对网络进行故障定位和排错；如果是安全工程师，可以通过wireshark对网络黑客渗透攻击进行快速定位并找出攻击源;如果是测试或者软件工程师，可以通过wireshark分析底层通信机制等等。

### 软件功能

1. 分析网络底层协议
2. 解决网络故障问题
3. 找寻网络安全问题

### 适合人群

1. 网络管理员
2. 网络工程师
3. 安全工程师
4. IT运维工程师

### 平台支持

1. Windows
2. MacOS
3. Linux/Unix

### 相关地址

1. http://www.wireshark.org/
2. http://www.wiresharkbook.com/
3. http://wiki.wireshark.org/

### 相关软件

1. Sniffer
2. Omnipeek
3. Fiddler
4. Httpwatch
5. 科来网络分析系统

## 抓包原理

### 网络原理

#### 本机环境

直接抓包本机网卡进出流量

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/01.png" width="70%">

#### 集线器环境

流量防洪，同一冲突域

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/02.png" width="70%">

#### 交换机环境

1. 端口镜像

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/03.png" width="70%">

2. ARP欺骗

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/04.png" width="70%">

3. MAC泛洪

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/05.png" width="70%">

### 底层原理

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/06.png" width="70%">

#### Win-/libpcap

Wireshark抓包时依赖的库文件

#### Capture

捕包引擎，利用libpcap/Winpcap从底层抓取网络数据包，libpcap/Winpcap提供了通用的抓包接口，能从不同类型的网络接口（包括以太网，令牌环网，ATM网等）获取数据包

#### Wiretap

格式支持，从抓包文件中读取数据包，支持多种文件格式

#### Core

核心引擎，通过函数调用将其他模块连接在一起，起到联动调度的作用

#### GTK1/2

图像处理工具，处理用户的输入输出显示

## 初始安装

从官网下载，默认选项即可

## 快速抓包

1. 初始界面

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/07.png" width="70%">

2. 选择网卡

   双击选中的网卡

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/08.png" width="70%">

3. 停止抓包

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/09.png" width="70%">

4. 保存数据包

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/10.png" width="70%">
