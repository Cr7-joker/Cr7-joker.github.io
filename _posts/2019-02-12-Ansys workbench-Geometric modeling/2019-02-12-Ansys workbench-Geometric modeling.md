---
title: Ansys workbench-Geometric modeling
tags: Modeling Ansys
edit: 2019-02-01
categories: Technology
status: Completed
description: Drawing a geometric model of the base by three-dimensional modeling by applying the simulation software Ansys workbench.
---

# Ansys workbench的DM三维建模之 绘制底座

## 实验原理

通过对仿真软件`Ansys workbench`的应用来进行`三维建模`绘制一个底座的几何模型

## 实现步骤  

1. 打开`workbench`，点击`File-new`，新建一个`project`。

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/01.png" width="90%">
2. 将`Geometry`放入到`项目概图`中

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/02.png" width="90%">
3. 双击A2，打开`DesignModeler`,在`Units`中选择`毫米`做单位

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/03.png" width="90%">
4. 选择一个平面（YZPlane）创建`草图`，选择草图切换到草图标签

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/04.png" width="90%">
5. 将视图**正视**，选择**直线命令**绘制几条直线

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/05.png" width="90%">
6. 进行标注尺寸，打开`Dimensions`对话框，选择通用标注长度，角度标注

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/06.png" width="90%">
7. 修改尺寸（H1=35mm，V2=35mm，V3=40mm，H4=15mm，A5=82°）

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/07.png" width="90%">
8. 对草图进行拉伸，选择**拉伸命令**（深度为60mm），点击`Generate`生成，切换视图到`ISO格式`查看

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/08.png" width="90%">
9. 拉伸生成底面，切换到面显示，创建一个坐标系，在此坐标系创建草图，选择草图并正视来绘制

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/09.png" width="90%">
10. 切换成线框图，绘制两个矩形，标注两个矩形的尺寸，进行圆角`Fillet`操作，继续标注尺寸，并进行尺寸更改（H1=25mm，H2=25mm，L2=10mm，V1=25mm，R1=10mm）

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/10.png" width="90%">

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/10+.png" width="90%">
11. 使用**拉伸切除**，选项为`Cut Material`，切除深度为15mm，Generate，切换到实体显示

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/11.png" width="90%">

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/12.png" width="90%">

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/13.png" width="90%">
12. **拉伸**生成圆孔，单击面选择，选择要切除的底面

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/14.png" width="90%">
13. 创建坐标系，并创建草图，在此草图上绘制一个圆，选择**圆命令**，绘制圆，展开约束工具栏，找到同心圆命令让绘制的圆和之前绘制的圆角同心，之后约束圆的直径，输入圆的直径为12mm

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/15.png" width="90%">
14. 拉伸切除，生成圆孔，`Cut Material`，切除深度为5mm，`Generate`

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/16.png" width="90%">
15. 在以此圆孔为底面，创建一个贯穿的圆孔，其直径为8mm，`Cut Material`，切除深度为15mm，`Generate`

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/17.png" width="90%">

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/18.png" width="90%">
16. **重复12-15步**，在另一侧绘制圆孔

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/19.png" width="90%">

## 实验结果

绘制底座模型完成

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/20.png" width="90%">

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/21.png" width="90%">

 <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-02-12-Ansys%20workbench-Geometric%20modeling/assert/22.png" width="90%">

## 分析

**Ansys workbench**的几何建模的基本方法，能绘制出一些简单的**机械构件**的模型。通过仿真软件应用软件**Ansys**可以进行**力学模型**，**磁学模型**的绘制和分析。