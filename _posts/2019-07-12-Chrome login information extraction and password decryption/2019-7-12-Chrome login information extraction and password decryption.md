---
title: Chrome login information extraction and password decryption
tags: C++ Database Decrypt VS2019 SQLite3 Chrome
edit: 2019-07-13
categories: C++ Technology
status: Completed
description: Get the login information (URL, login name, password, etc.) automatically saved by Google Chrome and password decryption
---
#  查看浏览器已保存的密码

1. 在地址栏输入chrome://settings/passwords来查看所有已保存的密码列表，搜索感兴趣的目标站点。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/01.png" width="70%">

2. 进入目标站点的登录页面，输入用户名前几位字符，让浏览器自动填充密码。右键审查元素（F12），选中密码区域，将密码字段代码的**type=”password”**改为**type=”text”**，即可查看明文密码。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/02.png" width="70%">

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/03.png" width="70%">

# 获得Chrome保存的登录信息和密码破解

## Chrome中保存的登录信息位置

Chrome将用户的登录信息(保存的密码被加密)保存在SQLite数据库文件中，位置如下：

`C:\Users\Joker\AppData\Local\Google\Chrome\User Data\Default\Login Data`

以文本方式打开`Login Data`文件可以看到其头部有`SQLite format 3`标记，说明其是`Sqlite3`的文件。使用使用[SQLiteStudio](https://sqlitestudio.pl/index.rvt)（在上篇[博文](https://www.shangzg.top/c++/C++-Basic-use-of-sqlite3.html#额外工具使用sqlitestdio辅助)有简单介绍）打开。

成功读取数据库文件保存的信息，但password段无法显示，如下图

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/04.png" width="70%">

选择Form view，查看十六进制格式，获得二次加密后的用户密码，如下图

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/05.png" width="70%">

**注：**如果Chrome正在运行，无法使用SQLiteStudio打开数据库文件Login Data，可将该文件复制后再打开

## C++编程实现登录信息提取及密码破解（VS2019）

1. VS2019导入SQLite3

   具体环境配置实现见之前博文[C++ Basic use of sqlite3](https://www.shangzg.top/c++/C++-Basic-use-of-sqlite3.html)

2. 头文件`CryptUnprotectData.h`

   ```c++
   #pragma once
   #ifndef _CryptUnProtectData_
   #define _Crypt_UnProtectData_
   #include <windows.h>
   #include <iostream>
   using namespace std;
   
   string getProfilePath();
   string Password_Handle(char* input);
   char* U2G(const char* utf8);
   
   #endif // !CryptUnProtectData.h
   
   ```

   包含获取存储登录信息文件路径方法（getProfilePath）和字符转换方法（U2G）和解密后密码处理方法（Password_Handle）。

3. 获取路径模块`ProfilePath_Get.cpp`

   ```c++
   #include "CryptUnprotectData.h"
   #include <ShlObj_core.h>
   constexpr auto Get_failed = "get_ProfilePath Failed";
   string getProfilePath() {
   	char* appDataPath = (char*)malloc(sizeof(char) * MAX_PATH);
   	if (appDataPath != NULL) {
   		//获取Chrome 保存登录信息文件Login Data的路径
   		SHGetFolderPathA(NULL, CSIDL_LOCAL_APPDATA, NULL, 0, appDataPath);	// 获取当前用户的文件系统目录C:\Users\username\AppData\Local
   		string profilePath = appDataPath;
   		//printf("%s\n", appDataPath);
   		profilePath = profilePath + "\\Google\\Chrome\\User Data\\Default\\";
   		return profilePath;
   	}
   	else
   		return Get_failed;
   }
   
   ```
   
   **SHGetFolderPathA**：参考window开发文档[SHGetFolderPathA function](https://docs.microsoft.com/zh-cn/windows/win32/api/shlobj_core/nf-shlobj_core-shgetfolderpatha)
   
   
   
   
   
4. 执行模块`run.cpp`（包含数据库操作及密码解密）

   ```c++
   #include "CryptUnprotectData.h"
   #include <Wincrypt.h>
   #include "sqlite3.h"
   #pragma comment(lib,"crypt32.lib")
   #pragma warning(disable:4996)
   
   int main(int argc, char* argv[])
   {
   	sqlite3* DB = NULL; // 一个打开的数据库实例
   	sqlite3_stmt* stmt = NULL;// sqlite3_stmt 预编译语句对象. 由sqlite3_prepare()创建，由sqlite3_finalize()销毁
   	string LoginDataPath = getProfilePath() + "Login Data";
   	const char* path = LoginDataPath.c_str();	// Login Data sql文件的路径
   	char** dbResult; // 是 char ** 类型，两个*号
   	int nRow, nColumn;// 表的行数，列数
   	int index;
   	DATA_BLOB DataOut;
   	DATA_BLOB Dataput;
   	LPWSTR pbtest = NULL;
   
   	// 根据文件路径打开数据库连接。如果数据库不存在，则创建。
   	// 数据库文件的路径必须以C字符串传入。
   	int result = sqlite3_open(path, &DB);
   
   	if (result == SQLITE_OK) {
   		std::clog << "打开数据库连接成功\n";
   		//开始查询，传入的 dbResult 已经是 char **，这里又加了一个 & 取地址符，传递进去的就成了char ***
   		const char* sql = "Select * from logins";
   		int result1 = sqlite3_prepare_v2(DB, sql, -1, &stmt, NULL);
   		int result2 = sqlite3_get_table(DB, "Select * from logins", &dbResult, &nRow, &nColumn, NULL);
   		if (result1 == SQLITE_OK && result2 == SQLITE_OK)
   		{
   			//查询成功
   			printf("表格共%d 记录!\n", nRow);
   			printf("表格共%d 列!\n", nColumn);
   			printf("字段名|字段值\n");
   			index = nColumn;
   			for (int i = 0; i < nRow; i++)
   			{
   				printf("第 %d 条记录\n", i);
   				for (int j = 0; j < nColumn; j++)
   				{
   					if (!(strcmp(dbResult[j], "password_value")))//如果列名为password_value，则需要对该列的列值进行解密操作
   					{
   						if (sqlite3_step(stmt) == SQLITE_ROW) {
   							//初始化加密结构DataOut
   							BYTE* pbDataInput = (BYTE*)sqlite3_column_text(stmt, j);
   							DWORD cbDataInput = sqlite3_column_bytes(stmt, j);
   							DataOut.pbData = pbDataInput;
   							DataOut.cbData = cbDataInput;
   						}
   						if (CryptUnprotectData(&DataOut, &pbtest, NULL, NULL, NULL, 0, &Dataput))
   						{
   							string s = Password_Handle((char*)Dataput.pbData);//解密后的密码处理
   							strcpy(dbResult[index], (char*)s.c_str());
   						}
   						else
   						{
   							printf("Decryption error!\n");
   						}
   					}
   					printf("字段名: %s | 字段值: %s\n", dbResult[j], U2G(dbResult[index]));
   					index++;
   					// dbResult 的字段值是连续的，从第0索引到第 nColumn - 1索引都是字段名称，从第 nColumn 索引开始，后面都是字段值，它把一个二维的表（传统的行列表示法）用一个扁平的形式来表示
   				}
   				printf("--------------------------------------------------------------------------------\n");
   			}
   		}
   		//清理语句句柄，准备执行下一个语句
   		sqlite3_finalize(stmt);
   		//到这里，不论数据库查询是否成功，都释放 char** 查询结果dbResult，使用 sqlite 提供的功能来释放
   		//sqlite3_free_table(dbResult); //执行会抛出断点，因为在运行过程中dbResult的地址已改变，不是最初分配给他的
   		//关闭数据库
   		sqlite3_close(DB);
   	}
   	else {
   		std::clog << "打开数据库连接失败\n";
   	}
   	return 0;
   }
   ```

   这里采用了

   `sqlite3_prepare_v2()`执行sql语句。

   `sqlite3_get_table()`方法用于获取数据库文件`Login Data`中所有信息，方便输出。

   `sqlite3_column_text()`方法读取某行中指定列的列值。

   `sqlite3_column_bytes()`获得指定列列值的长度大小。

   `CryptUnprotectData()`解密函数，其结构及功能介绍与具体使用见博文[Data encryption and decryption](https://www.shangzg.top/technology/Data-encryption-and-decryption-Data-encryption-and-decryption.html)。

   

   

5. 密码处理模块`Password_Handle.cpp`

   ```c++
   #include "CryptUnprotectData.h"
   #include <algorithm>
   string Password_Handle(char* input) {
   	string s = input;
   	int* a = new int[11];
   	a[0] = s.find("\x1");
   	a[1] = s.find("\x2");
   	a[2] = s.find("\x3");
   	a[3] = s.find("\x4");
   	a[4] = s.find("\x5");
   	a[5] = s.find("\x6");
   	a[6] = s.find("\x7");
   	a[7] = s.find("\x8");
   	a[8] = s.find("\x9");
   	a[9] = s.find("\a");
   	a[10] = s.find("\b");
   	for (int i = 0; i < 11; i++)
   	{
   		if (a[i] == -1) {
   			a[i] = 100;
   		}
   	}
   	int n = *min_element(a, a + 11);
   	return s.substr(0, n);
   }
   ```

   通过解密函数解密之后得到的密码会在尾部填充一些字段乱码，由于Chrome在加密时采用分组加密，每个密码单独分组，且分组长度相同（分组长度大于最大密码长度），空余部分用不影响读取的符号填充，所以直接解密后输出会在尾部出现乱码，需要对解密后的密码进行截取，只需要前面正确的部分。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/07.png" width="70%">

   填充的乱码一般是十六进制的"\x1"—"\x9"和"\a"，"\b"，所以进行乱码之前的密码子串的截取。

   

   

6. 字符格式转换模块`UTF8_Trans.cpp`

   ```c++
   #include "CryptUnprotectData.h"
   
   char* U2G(const char* utf8)//字符串转换函数
   {
   	int len = MultiByteToWideChar(CP_UTF8, 0, utf8, -1, NULL, 0);
   	wchar_t* wstr = new wchar_t[len + 1];
   	memset(wstr, 0, len + 1);
   	MultiByteToWideChar(CP_UTF8, 0, utf8, -1, wstr, len);
   	len = WideCharToMultiByte(CP_ACP, 0, wstr, -1, NULL, 0, NULL, NULL);
   	char* str = new char[len + 1];
   	memset(str, 0, len + 1);
   	WideCharToMultiByte(CP_ACP, 0, wstr, -1, str, len, NULL, NULL);
   	if (wstr) delete[] wstr;
   	return str;
   }
   ```

   如果用户名或其他信息中有中文字符，直接输出会产生乱码，需要进行转码之后输出，同理如果密码中有中文字符，解密之后也需要进行格式转换后才能正确显示。

   # 集成测试

   运行run.cpp，其结果如下图：

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-Chrome%20login%20information%20extraction%20and%20password%20decryption/assert/06.png" width="70%">

   用户信息提取成功，并获得解密后的密码。

   

   **注**：如果Chrome浏览器处于打开状态可能读取信息失败！！！

   [C++工程项目文件（包含Opera浏览器解密）](https://github.com/Cr7-joker/Google-browser-login-information-extraction-and-password-cracking)已上传到github。

