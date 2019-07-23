---
title: C++ U Disk content copy program
tags: C++ VS2019 UDisk
edit: 2019-07-23
categories: C++ Technology
status: Completed
description: Check the inserted disk (U disk) to read the disk data and copy it to the corresponding location based on C++.
---

# 头文件	UDisk.h

```c++
#pragma once
#ifndef _UDisk_
#define _UDisk_

#include <iostream>
#include <stdlib.h>
#include <io.h>
#include <windows.h>
#include <string>
#include <sys/types.h>
#include <sys/stat.h>

using namespace std;
constexpr auto NO_UDisk = "There is no new UDisk";
string CreateDirc(); // 创建用于接收拷贝文件的路径
string UDisk_Path(DWORD first);	// 获得磁盘路径
void copyfiles(string source, char* target);	//CopyFiles

#endif // !_UDisk_
```

头文件包含三个方法：

**string CreateDirc()**：创建用于接收拷贝文件的路径

**string UDisk_Path(DWORD first)**：获得磁盘路径

**void copyfiles(string source, char* target)**：CopyFiles





# 创建路径	CreateDirc.cpp

```c++
#include"UDisk.h"
//创建一个文件夹路径用来保存拷贝的文件
string CreateDirc() {
	char path[100] = "D:\\CopyFile\\";
	while (_access(path, 0) == 0) { // if directory already exist,this will auto add '\1' back it;
		strcat(path, "1\\");
	}
	return path;
}
```

**_access**函数：

主要用于文件读取方面——判断文件是否存在，并判断文件是否可写。Linux下，该函数为access，位于头文件<unistd.h>中，而在标准C++中，该函数为_access，位于头文件<io.h>中，两者的使用方法基本相同，只是在一些参数方面可能会有一些不同的宏定义。下面是标准C++为例做一下总结：

**头文件**：<io.h>

**函数原型**：int _access(const char *pathname, int mode);

**参数**：pathname 为文件路径或目录路径 mode 为访问权限（在不同系统中可能用不能的宏定义重新定义）

**返回值**：如果文件具有指定的访问权限，则函数返回0；如果文件不存在或者不能访问指定的权限，则返回-1。

**备注**：当pathname为文件时，\_access函数判断文件是否存在，并判断文件是否可以用mode值指定的模式进行访问。当pathname为目录时，_access只判断指定目录是否存在，在Windows NT和Windows 2000中，所有的目录都只有读写权限。

**mode的值和含义如下所示**：

00——只检查文件是否存在

02——写权限

04——读权限

06——读写权限





# 监测磁盘(U盘)	UDisk_Judgement.cpp

```c++
#include"UDisk.h"

string UDisk_Path(DWORD first) {
	DWORD second = 0;
	char n = 0;
	string UDiskPath = "0";
	second = GetLogicalDrives();	//检索表示此时可用磁盘驱动器的位掩码。
	if (second > first) {	// 若检测到插入磁盘
		second -= first;
		while (second >>= 1) n++;	//进行右移1位操作，判断盘符
		UDiskPath[0] = n + 65;	//获取盘符
		UDiskPath += ":\\";
		return UDiskPath;
	}
	else
	{
		return NO_UDisk;
	}
}
```

**GetLogicalDrives()**函数：[GetLogicalDrives function](https://docs.microsoft.com/en-us/windows/win32/api/fileapi/nf-fileapi-getlogicaldrives)

函数返回值是一个long型，将其用二进制显示时，其中第0位表示A盘，第1位表示B盘，当某位为1时说明存在这个盘，即00000011表示有A盘和B盘。

[位掩码(BitMask)的介绍与使用](https://www.jianshu.com/p/4e73512c03b8)





# 拷贝	CopyFile.cpp

```c++
#include"UDisk.h"
// 拷贝文件

void copyfiles(string source, char* target) {
	WIN32_FIND_DATA FindFileData;	// 包含文件的信息
	HANDLE hFind;	// 句柄
	string str = source + "*";
	hFind = FindFirstFile(str.c_str(), &FindFileData); // find the target dirctory's frist file;
	while (1) {
		if (hFind == INVALID_HANDLE_VALUE || hFind == (HANDLE)ERROR_FILE_NOT_FOUND) { // file found error
			cout << " 没有找到文件 " << endl;
			break;
		}

		else {
			char tempPath[200], tempSource[200];
			if (FindFileData.dwFileAttributes & FILE_ATTRIBUTE_DIRECTORY) { // 判断是否为文件夹
				if (strcmp(FindFileData.cFileName, ".") && strcmp(FindFileData.cFileName, "..") && strcmp(FindFileData.cFileName, "System Volume Information")) { // take out . & .. & System Volume Information dirc
					strcpy(tempSource, source.c_str());
					strcat(tempSource, FindFileData.cFileName);
					strcpy(tempPath, target);
					strcat(tempPath, FindFileData.cFileName);
					if (CreateDirectory(tempPath, NULL) == 0) {	// 创建文件夹目录
						cout << "创建目录失败" << endl;
					}
					strcat(tempSource, "\\");
					strcat(tempPath, "\\");
					copyfiles(tempSource, tempPath); // Recursion 递归函数
				}
			}
			else { //if is a file,copy to target dirc
				strcpy(tempSource, source.c_str());
				strcpy(tempPath, target);
				strcat(tempPath, FindFileData.cFileName);
				strcat(tempSource, FindFileData.cFileName);
				if (CopyFile(tempSource, tempPath, false))	// 表示将文件tempSource拷贝到tempPath，如果B已经存在则覆盖（第三参数为TRUE时表示不覆盖）
				{
					cout << tempSource << " ----------拷贝成功!!! " << endl;
				}
				else
				{
					cout << tempSource << " ----------拷贝失败!!! " << endl;
				}
			}
			if (FindNextFile(hFind, &FindFileData) == 0) break; // found the next file
		}
	}
	FindClose(hFind); // handle closed;
}
```

**FindFirstFile()**函数：[FindFirstFileA function](https://docs.microsoft.com/zh-cn/windows/win32/api/fileapi/nf-fileapi-findfirstfilea)

**CreateDirectory()**函数：[CreateDirectory function](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-createdirectory)

**CopyFile()**函数：[CopyFile function](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-copyfile)





# RUN.cpp

```c++
#include"UDisk.h"
int main() {
	string path = CreateDirc();	
	if (CreateDirectory(path.c_str(), NULL)) {	// //创建用于保存Copy文件的文件夹
		while (1) { // every 3 seconds to estimate if there is a USB device
			DWORD first = GetLogicalDrives();	// 检索表示当前可用磁盘驱动器的位掩码。
			cout << " waiting…… " << endl;
			Sleep(3000);
			if (UDisk_Path(first) != NO_UDisk)
			{
				copyfiles(UDisk_Path(first), (char*)path.c_str());	//Copy
				return 0;
			}
		}
	}
}
```

# 运行测试

运行**RUN.cpp**，程序正在等待磁盘(U盘)插入。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-23-C++%20U%20Disk%20content%20copy%20program/assert/01.png" width="70%">

即将插入U盘信息如下：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-23-C++%20U%20Disk%20content%20copy%20program/assert/02.png" width="70%">

程序监测到U盘插入，并进行数据资料读取拷贝。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-23-C++%20U%20Disk%20content%20copy%20program/assert/03.png" width="70%">

最后，在指定路径查看，拷贝成功。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-23-C++%20U%20Disk%20content%20copy%20program/assert/04.png" width="70%">

# **注**：VS2019可能产生如下报错：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-23-C++%20U%20Disk%20content%20copy%20program/assert/05.png" width="70%">

**问题原因**：
C语言的标准函数中，一些读取或写入内存的函数存在内存越界的问题，从而使得内存数据变得不安全。如scanf、gets、strcat等函数都存在着这样的问题。 

为了避免这个问题，在VS中，另外提供了如scanf_s，get_s，strcat_s等相关的改进函数，来替代原来的标准函数的功能，并通过添加内存读取范围的限制来解决不安全的问题。 

**问题解决**：

在项目**属性**—>**C/C++**—>**预处理器**—>**预处理器定义**中添加**_CRT_SECURE_NO_WARNINGS**即可不产生报错。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-23-C++%20U%20Disk%20content%20copy%20program/assert/06.png" width="70%">

# 项目文件已上传至GitHub

[U Disk content copy program](https://github.com/Cr7-joker/U-Disk-content-copy-program)