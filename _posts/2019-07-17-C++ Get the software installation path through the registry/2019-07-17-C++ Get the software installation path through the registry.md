---
title: C++ Get the program installation path
tags: C++ VS2019 Registry Installtion Path
edit: 2019-07-17
categories: C++ Technology
status: Completed
description: Get the installation path of the program in the registry based on C++
---

# 注册表查询

在运行里面输入：**regedit**，打开注册表编辑器。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-17-C++%20Get%20the%20software%20installation%20path%20through%20the%20registry/assert/01.png" width="70%">

软件的安装路径查询一般在**HKEY_LOCAL_MACHINE\SOFTWARE**里面。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-17-C++%20Get%20the%20software%20installation%20path%20through%20the%20registry/assert/02.png" width="70%">

以Firefox浏览器为例，路径为**\HKEY_LOCAL_MACHINE\SOFTWARE\Mozilla\Mozilla Firefox\67.0.4 (x64 zh-CN)\Main**，里面的**Install Directory**则保存了软件的安装路径。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-17-C++%20Get%20the%20software%20installation%20path%20through%20the%20registry/assert/03.png" width="70%">

# C++ 编程实现

```c++
#include <iostream>
#include <windows.h>
using namespace std;
int main(void)
{
#define MY_BUFSIZE 128 // Arbitrary initial value.
	// Dynamic allocation will be used.
	HKEY hKey;
	TCHAR szProductType[MY_BUFSIZE];
	DWORD dwBufLen = MY_BUFSIZE;
	LONG lRet;
	// 下面是打开注册表, 只有打开后才能做其他操作
	lRet = RegOpenKeyEx(HKEY_LOCAL_MACHINE, // 要打开的根键
		TEXT("SOFTWARE\\Mozilla\\Mozilla Firefox\\67.0.4 (x64 zh-CN)\\Main"), // 要打开的子子键（火狐版本67.0.4 (x64 zh-CN)）
		0, // 这个一定要为0
		KEY_QUERY_VALUE, // 指定打开方式,此为读
        //KEY_QUERY_VALUE|KEY_WOW64_64KEY, // 32位程序非要获取64位的注册表需要在打开键时，添加参数KEY_WOW64_64KEY
		&hKey); // 用来返回句柄
	if (lRet == ERROR_SUCCESS) // 判断是否打开成功
	{
		cout << "打开注册表成功" << endl;
	}
	else {
		cout << "打开注册表失败" << endl;
		return 1;
	}
		
	// 下面开始查询
	lRet = RegQueryValueEx(hKey, // 打开注册表时返回的句柄
		TEXT("Install Directory"), //要查询的名称,Firefox安装目录记录在这个里面
		NULL, // 一定为NULL或者0
		NULL,
		(LPBYTE)szProductType, // 我们要的东西放在这里
		&dwBufLen);
	if (lRet == ERROR_SUCCESS) // 判断是否查询成功
	{
		cout << "获得安装目录成功" << endl;
		RegCloseKey(hKey);
		cout << (char*)szProductType << endl;
	}
	else
	{
		cout << "获得安装目录失败" << endl;
		return 1;
	}
	
}
```

**注意**：32位程序非要获取64位的注册表需要在打开键时，添加参数**KEY_WOW64_64KEY**，我一开始用的VS2019 ×86 来运行程序，始终找不到注册文件，换成×64即可运行找到，如果用×86编译，一定要加上参数**KEY_WOW64_64KEY**才能获得正常的路径找到注册文件！！！

结果截图：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-17-C++%20Get%20the%20software%20installation%20path%20through%20the%20registry/assert/04.png" width="70%">