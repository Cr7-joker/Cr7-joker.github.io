---
title: Wireshark use tutorial
tags: Ansys Network
edit: 2019-03-04
categories: Technology
status: Writing
description: The use tutorial from entry to mastery of network analysis tool Wireshark
---

# [基础]软件使用调试

## Wireshark安装入门

### 软件介绍

Wireshark（前称Ethereal）是一个[网络封包](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E5%B0%81%E5%8C%85)分析软件。网络封包分析软件的功能是撷取网络封包，并尽可能显示出最为详细的网络封包资料。Wireshark使用WinPCAP作为接口，直接与网卡进行数据报文交换。

Wireshark是目前全球使用最广泛的开源抓包软件(前身为Ethereal)，是一个通用化的网络数据嗅探器和协议分析器，由Gerald Combs编写并于1998年以GPL开源许可证发布。如果是网络工程师，可以通过Wireshark对网络进行故障定位和排错；如果是安全工程师，可以通过wireshark对网络黑客渗透攻击进行快速定位并找出攻击源;如果是测试或者软件工程师，可以通过wireshark分析底层通信机制等等。

#### 软件功能

1. 分析网络底层协议
2. 解决网络故障问题
3. 找寻网络安全问题

#### 适合人群

1. 网络管理员
2. 网络工程师
3. 安全工程师
4. IT运维工程师

#### 平台支持

1. Windows
2. MacOS
3. Linux/Unix

#### 相关地址

1. http://www.wireshark.org/
2. http://www.wiresharkbook.com/
3. http://wiki.wireshark.org/

#### 相关软件

1. Sniffer
2. Omnipeek
3. Fiddler
4. Httpwatch
5. 科来网络分析系统

### 抓包原理

#### 网络原理

##### 本机环境

直接抓包本机网卡进出流量

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/01.png" width="70%">

##### 集线器环境

流量防洪，同一冲突域

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/02.png" width="70%">

##### 交换机环境

1. 端口镜像

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/03.png" width="70%">

2. ARP欺骗

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/04.png" width="70%">

3. MAC泛洪

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/05.png" width="70%">

#### 底层原理

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/06.png" width="70%">

##### Win-/libpcap

Wireshark抓包时依赖的库文件

##### Capture

捕包引擎，利用libpcap/Winpcap从底层抓取网络数据包，libpcap/Winpcap提供了通用的抓包接口，能从不同类型的网络接口（包括以太网，令牌环网，ATM网等）获取数据包

##### Wiretap

格式支持，从抓包文件中读取数据包，支持多种文件格式

##### Core

核心引擎，通过函数调用将其他模块连接在一起，起到联动调度的作用

##### GTK1/2

图像处理工具，处理用户的输入输出显示

### 初始安装

从官网下载，默认选项即可

### 快速抓包

1. 初始界面

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/07.png" width="70%">

2. 选择网卡

   双击选中的网卡

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/08.png" width="70%">

3. 停止抓包

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/09.png" width="70%">

4. 保存数据包

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/10.png" width="70%">

### 界面介绍

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/11.png" width="70%">

1. 标题栏
2. 菜单栏
3. 工具栏
4. 数据包过滤栏
5. 数据包列表区
6. 数据包详细区
7. 数据包字节区
8. 数据包统计区

## Wireshark进阶调试

### 显示界面设置

#### 显示大小

在`菜单栏`可调整字体显示大小

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/12.png" width="70%">

#### 列设置

1. 增加列

   在`数据包详细区`可选择想要作为列的信息，**右键**，**应用为列**，在`数据包列表区`即可显示相应增加的列

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/13.png" width="70%">

2. 修改列

3. 隐藏列

4. 删除列

   在`数据包列表区`的列名**右键**，即可完成操作

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/14.png" width="70%">

#### 时间设置

1. 设置时间格式

   在`视图`里设置

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/15.png" width="70%">

2. 设置参考时间

   选择想要设置为参照点的数据包，**右键**，**设置为时间参考**

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/16.png" width="70%">

#### 名字解析

1. 功能：将MAC地址，IP地址，端口号等转换成名字，默认是开启MAC地址解析

2. 开启名字解析

   在**Capture捕获**里点击**选项**开启想要解析的

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/17.png" width="70%">

3. 手工设置解析

   在想要手动解析的数据包**右键**，**编辑解析的名字**

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/18.png" width="70%">

### 数据包操作

#### 标记数据包

1. 标记/高亮数据包

   选择所想标记/高亮数据包，**右键**，**标记分组**

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/19.png" width="70%">

2. 修改数据包颜色
   1. 直接在数据包列表修改

      在数据包，**右键**，**会话着色**，可对不同协议设置不同颜色（*仅对本次进程有效，程序重启恢复默认*）

      <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/20.png" width="70%">

   2. 修改数据包默认颜色方案

      在`视图`里点击**着色规则**，在里面选择想要修改的数据包类型，通过修改**前景**，**后景**来修改默认颜色

      <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/21.jpg" width="70%">

      <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/22.png" width="70%">

#### 注释数据包

功能：为数据包编写注释信息

在所想注释数据包**右键**，**分组注释**，写下自己的注释，然后在`数据包详细区`即可显示自己所写注释

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/23.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/24.jpg" width="70%">

#### 合并数据包

功能：将两个数据包文件合并

在`文件`里点击`合并`，选择想要合并的数据包文件

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/25.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/26.png" width="70%">

#### 打印数据包

在`文件`里点击`Print`

#### 导出数据包

在`文件`里点击`导出特定分组`，选定导出的种类（All packets,Selected packet etc.）

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/27.png" width="70%">

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/28.png" width="70%">

导出为其他格式文件，如CSV格式

在`文件`里点击`导出分组解析结果`，选择想导出的类型

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/29.png" width="70%">

### 首选项设置

功能：设置默认软件参数

1. 修改默认打开目录

   在`编辑`里点击`首选项`，点击**Appearance**里即可更改打开路径

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/30.png" width="70%">

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-03-04-Wireshark%20use%20tutorial/assert/31.png" width="70%">

2. 修改用户界面

   在`编辑`里点击`首选项`，点击**Appearance**里的**Layout**，**Columns**，**Font and Colors**即可调整用户界面

3. 修改抓包设置

   功能：

   1. 网卡设置
   2. 抓包过滤器
   3. 多文件连续保存
   4. 停止抓包规则
   5. 名字解析

4. 修改名字解析

**都在`编辑`里点击`首选项`里面设置**

### 抓包选项设置



### 过滤器设置

## Wireshark高级功能

