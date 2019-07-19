---
title: Opera login information extraction and password decryption
tags: C++ Decrypt VS2019 SQLite3 Opera
edit: 2019-07-19
categories: C++ Technology
status: Completed
description: Get the login information (URL, login name, password, etc.) automatically saved by Opera browser and password decryption
---

# 获得Opera保存的登录信息和密码破解

Opera浏览器的用户信息保存原理和密码加密与Chrome一样，**具体方法步骤**可见之前对Chrome进行用户信息提取及密码解密。[Chrome login information extraction and password decryption](https://www.shangzg.top/c++/technology/Chrome-login-information-extraction-and-password-decryption.html)

# 不同之处

Opera存储用户登录信息文件位于

`C:\Users\username\AppData\Roaming\Opera Software\Opera Stable\Login Data`

所以对于获取路径模块需要进行一定的修改

`ProfilePath_Get.cpp`

```c++
#include "Chrome(Opera)_Decrypt.h"
#include <ShlObj_core.h>
constexpr auto Get_failed = "get_ProfilePath Failed";
string getProfilePath() {
	char* appDataPath = (char*)malloc(sizeof(char) * MAX_PATH);
	if (appDataPath != NULL) {     
       //获取Opera 保存登录信息文件Login Data的路径
		SHGetFolderPathA(NULL, CSIDL_APPDATA, NULL, 0, appDataPath);	// 获取当前用户的文件系统目录C:\Users\username\AppData\Roaming（CSIDL_APPDATA默认为AppData下的Roaming）
		string profilePath = appDataPath;
		profilePath = profilePath + "\\Opera Software\\Opera Stable\\";	// Opera的Login Data所在路径
        
		/*
		//获取Chrome 保存登录信息文件Login Data的路径
		SHGetFolderPathA(NULL, CSIDL_LOCAL_APPDATA, NULL, 0, appDataPath);	// 获取当前用户的文件系统目录C:\Users\username\AppData\Local
		string profilePath = appDataPath;
		//printf("%s\n", appDataPath);
		profilePath = profilePath + "\\Google\\Chrome\\User Data\\Default\\";
		*/

		return profilePath;
	}
	else
		return Get_failed;
}

```

# 项目文件已上传至github

[C++工程项目文件（包含Chrome and Opera浏览器解密）](https://github.com/Cr7-joker/Chrome-and-Opera_Decrypt)

