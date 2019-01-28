---
title: How to use Typora
tags: Blog Markdown
edit: 2019-01-28
categories: Blog
status: Completed
description:Typora is the ultimate compact markdown editor that supports the editing of mathematical formulas, can be exported to pdf and HTML, etc. I will briefly describe the basic usage of typora.
---


# Why Typora?

==Readable & Writable==

Typora will give you a seamless experience as both a reader and a writer. It removes the preview window, mode switcher, syntax symbols of markdown source code, and all other unnecessary distractions. Replace them with a real live preview feature to help you concentrate the content itself.

# Its characteristics

1. 完全免费，目前已支持中文
2. 跨平台，支持windows,mac,linux
3. 支持数学公式输入，图片插入
4. 极其简洁，无多余功能
5. 界面所见即所得

# 区域元素

## YAML FONT Matters

在文章最上方输入---，按换行键产生，输入内容即可



## 菜单

输入[toc]+换行键，产生标题，自动更新

```
[toc]
```

### 效果

[TOC]

## 段落

按换行键建立新的一行
可在行尾插入打断线，禁止向后插入

```
按换行键建立新的一行<br/>
```



## 标题

开头#的个数表示，空格+文字。标题有1~6个级别，#表示开始，按换行键结束

```
# H1
## H2
###### H6
```



## 引注

```
> ni
>
> ni hao
```

### 效果

> ni
>
> >
> >
> >> nihao



## 序列

开头*/+/-，空格+文字，可以创建无序序列，换行键换行，删除键+shift+tab跳出

开头1.，空格+后接文字，可以创建有序序列

```
*   Red
+   Green
-   Blue
 
1.  Red
2.  Green
3.  Blue
```



## 代码块

开头```+语言名，开启代码块，换行键换行，光标下移键跳出

```
​```python
```



## 数学块

使用MtathJax建立数学公式

开头$$+换行键，产生输入区域，输入Tex/LaTex格式的数学公式

```
$$

$$
```



## 表格

开头|+列名+|+列名+|+换行键，创建一个2*2表格

将鼠标放置其上，弹出编辑尺寸，个数，文字等

```
|first|second|
```

| first | second |
| ----- | ------ |
|       |        |



## 脚注

在需要添加脚注的文字后面+[+^+序列+]，注释的产生可以鼠标放置其上单击自动产生，添加信息

或人工添加+[+^+序列+]+:

```
脚注产生的方法[^footnote].
[^footnote]:这个就是*脚注*
```



## 水平线

输入***/---，换行键换行

```
***
---
```

---

***

# 特征元素



## 超链接

用[]括住要超链接的内容，紧接着用()括住超链接源+名字，超链接源后面+超链接命名

```
This is [an example](http://example.com/ "Title") inline link.
 
[This link](http://example.net/) has no title attribute.
```

This is [an example](http:*//example.com/ "Title"**) inline link.

[This link](http:*//example.net/**) has no title attribute.



## URLs

用<>括住url，可手动设置url

对于标准URLs，可自动识别

```

<www.Shangzg.top>
www.baidu.com
```

<www.Shangzg.top>

www.baidu.com



## 图片

1. 手动添加：类似链接，前面需加！
2. 用鼠标拖图片进入，然后鼠标放置其上修改

```
![joker](https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/joker.jpg)
```

![joker](https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/joker.jpg)



![illidan](https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/illidan.jpg)



## 斜体

以*或__括住

```
*Cr7-joker.github.io*
_Cr7-joker.github.io_
```

*Cr7-joker.github.io*
_Cr7-joker.github.io_



## 加粗

开头双\*或双\_，结尾双\*或双\_，建议双*

```
**Cr7-joker.github.io**
__Cr7-joker.github.io__
```

**Cr7-joker.github.io**
__Cr7-joker.github.io__



## 删除线

用两个~开头，两个~结尾

```
~~shangzg.top~~
```

~~shangzg.top~~



## 下划线

使用HTML标签

```
<u>Underline</u>
```

<u>Underline</u>



## 代码

用两个`在正常段落总表示代码

```
Use the `printf()` function.
```

Use the `printf()` function.



##  `Preference` Panel -> `Markdown` Tab启动

![markdown](https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/markdown.png)



## 数学式

需 `Preference` Panel -> `Markdown` Tab启动，

输入$，然后按ESC键，之后输入Tex命令，可预览

```
$\lim_{x\to\infty}\exp(-x)=0$
```

$\lim_{x\to\infty}\exp(-x)=0​$



## 下标

需 `Preference` Panel -> `Markdown` Tab启动，

使用~括住内容

```
H~2~O
```

H~2~O



## 上标

需 `Preference` Panel -> `Markdown` Tab启动，

使用^括住内容

```
X^2^
```

X^2^



## 高亮

需 `Preference` Panel -> `Markdown` Tab启动，

使用==括住内容

```
==highlight==
```

==highlight==



# 其他

其实也可以通过鼠标右击完成，选项都有

![other](https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-01-28-How-to-use-Typora/assets/other.png)

