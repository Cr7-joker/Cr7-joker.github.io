---
title: Browser user information Decrypt
tags: C++ Decrypt VS2019 Chrome Opera Firefox VSInstaller
edit: 2019-07-29
categories: C++ Technology
status: Completed
description: Get the login information (URL, login name, password, etc.) automatically saved by browsers(Chrome，Firefox，Opera) and password decryption
---

# 简介

之前分开进行对不同浏览器的用户登录信息提取及解密，现在就把Chrome，Firefox，Opera三个浏览器的用户信息登录提取和解密整合在一起，对之前的代码进行改进和整理，并创建一个可安装程序。

# 改动

1. 因为Firefox用户登录信息提取解密程序需要在64位环境下编译运行，所以将不同浏览器整合，其环境选定为64位，需要对Chrome和Opera进行用户登录信息提取解密所依赖的`Sqlite3`选定位64位的。[官网](https://www.sqlite.org/download.html)下载64位。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/01.png" width="70%">

   运行cmd，输入

   ```
   "D:\VS2019\VC\Tools\MSVC\14.22.27812\bin\Hostx64\x64\lib.exe" /MACHINE:IX64 /DEF:D:\SQLite3\SQLite3.def /OUT:D:\SQLite3\SQLite3.lib
   ```

   通过VS的64位lib程序进行执行，其余环境配置步骤不变。

2. Firefox版本问题

   之前对Firefox进行用户登录信息提取解密是基于某一特定版本，如今进行改进，从注册表读取所安装Firefox版本信息，在进行下一步操作。

   ```c++
   #define MY_BUFSIZE 128 // Arbitrary initial value.
   // Dynamic allocation will be used.
   constexpr auto Get_failed = "get_InstallationPath Failed";
   // 通过注册表获取软件的安装路径
   string getInstallationPath() {
   	HKEY hKey;
   	TCHAR szProductType[MY_BUFSIZE];
   	DWORD dwBufLen = MY_BUFSIZE;
   	DWORD dwBufLen2 = MY_BUFSIZE;
   	LONG lRet;
   	// 下面是打开注册表, 只有打开后才能做其他操作
   	lRet = RegOpenKeyEx(HKEY_LOCAL_MACHINE, // 要打开的根键
   		TEXT("SOFTWARE\\Mozilla\\Mozilla Firefox"), // 要打开的子子键（火狐目录）
   		0, // 这个一定要为0
   		KEY_QUERY_VALUE,	// 指定打开方式,此为读
   		//KEY_QUERY_VALUE|KEY_WOW64_64KEY, // 32位程序非要获取64位的注册表需要在打开键时，添加参数KEY_WOW64_64KEY
   		&hKey); // 用来返回句柄
   
   	if (lRet == ERROR_SUCCESS) // 判断是否打开成功
   	{
   		// 打开注册表成功
   		// 开始查询火狐版本
   		lRet = RegQueryValueEx(hKey, // 打开注册表时返回的句柄
   			TEXT("CurrentVersion"), //要查询的名称,火狐版本记录在这里
   			NULL, // 一定为NULL或者0
   			NULL,
   			(LPBYTE)szProductType, // 我们要的东西放在这里
   			&dwBufLen);
   
   		if (lRet == ERROR_SUCCESS) // 判断是否查询成功
   		{
   			string versionPath = szProductType;
   			versionPath += "\\Main";
   			lRet = RegOpenKeyEx(hKey, // 要打开的根键
   				TEXT(versionPath.c_str()), // 要打开的子子键（火狐版本）
   				0, // 这个一定要为0
   				KEY_QUERY_VALUE,	// 指定打开方式,此为读
   				//KEY_QUERY_VALUE|KEY_WOW64_64KEY, // 32位程序非要获取64位的注册表需要在打开键时，添加参数KEY_WOW64_64KEY
   				&hKey); // 用来返回句柄
   
   			if (lRet == ERROR_SUCCESS) // 判断是否打开成功
   			{
   				// 打开成功
   				// 开始查询
   
   				lRet = RegQueryValueEx(hKey, // 打开注册表火狐版本目录时返回的句柄
   					TEXT("Install Directory"), //要查询的名称,火狐安装目录记录在这里
   					NULL, // 一定为NULL或者0
   					NULL,
   					(LPBYTE)szProductType, // 我们要的东西放在这里
   					&dwBufLen2);
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
   				printf("打开安装目录失败\n");
   				return Get_failed;
   			}
   		}
   		else {
   			printf("打开火狐版本目录失败\n");
   			return Get_failed;
   		}
   	}
   	else {
   		printf("打开注册表失败\n");
   		return Get_failed;
   	}
   }
   ```

   

# 可安装程序实现

将所写项目进行打包，最后成为一个可安装程序。

1. 我采用的是VS2019，因为最新版本的原因，没有可安装程序的项目创建，所以需要进行下载。

   下载**Visual Studio Installer**。

   [Visual Studio 2017 Installer](https://marketplace.visualstudio.com/items?itemName=visualstudioclient.MicrosoftVisualStudio2017InstallerProjects)

   1. 在解决方案中新建一个**Setup Project**项目

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/02.png" width="70%">

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/03.png" width="70%">

2. 建立成功后，界面如下

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/04.png" width="70%">

   里面最左侧的框框有三个文件夹

   1.“应用程序文件夹”即"Application Folder"表示要安装的应用程序需要添加的文件；

   2.“用户的‘程序’菜单”即"User's Programs Menu"表示：应用程序安装完，用户的“开始菜单”中的显示的内容，一般在这个文件夹中，需要再创建一个文件用来存放：应用程序.exe和卸载程序.exe；

   3.“用户桌面”即"User's Desktop"表示：这个应用程序安装完，用户的桌面上的创建的.exe快捷方式。

3. 右键“应用程序文件夹”—>“Add”—“文件”

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/05.png" width="70%">

   添加的文件一般是已经编译生成过的应用程序项目的release或debug目录下的exe文件（即位于../bin/Release(Debug)文件夹下的主程序exe文件）；

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/06.png" width="70%">

   添加后，一般它会自动把exe程序所需的依赖项也加进来，如各种dll文件，在右侧的“**Detected Dependencies**”里面可以看到它自动导入了哪些依赖项，方便你检查是否有遗漏。

   接下来，可能还剩一些文件夹或者配置文件XML，dll等没有自动加进来，这个时候就需要自己手动添加，方式也是一样，右键“应用程序文件夹”—>“Add”—>“文件”，我们这里就需要将`sqlite3.dll`添加进去。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/07.png" width="70%">

4. 创建快捷方式

   右键主程序exe文件，选择“创建快捷方式到……”

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/08.png" width="70%">

   然后，框里会出现一个快捷方式项，将它剪切，粘贴到“用户桌面”文件夹下。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/09.png" width="70%">

   至于快捷方式的名称、图标、描述等其他属性，可以在属性面板中设置，如下：

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/10.png" width="70%">

5. 添加卸载程序

   既然有安装就有卸载，卸载程序其实是一个Windows操作系统自带的程序（`C：Windows\System32\Msiexec.exe`），只不过是通过给它传特殊的参数命令，来让它执行卸载

   添加和设置卸载程序的操作如下：

   首先，将卸载程序放在“应用程序文件夹”目录下，右键“应用程序文件夹”，添加——文件，在系统盘下找到这个路径文件——`C：Windows\System32\Msiexec.exe`添加进去。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/11.png" width="70%">

   由于`Msiexec.exe`这个名字不够直观，所以一般接下来我们会对它重命名，一般改为“`卸载.exe`”或“`UnInstall.exe`”，然后给它创建快捷方式并将快捷方式放到“用户程序菜单”目录下。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/12.png" width="70%">

   接下来是很关键的一步，**设置卸载参数**，告诉卸载程序该卸载哪个。

   首先，找到安装项目的**ProductCode**，在安装项目的属性面板中可以看到，如下：

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/13.png" width="70%">

   复制此**ProductCode**，粘贴到“卸载.exe”快捷方式的**Arguments**属性，前面加**/x空格**，如下：

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/14.png" width="70%">

6. 其他设置

   如果还想对安装程序进行其他设置，比如，友化安装欢迎界面，自定制安装步骤，修改注册表，设置启动条件（比如要求必须先安装指定的.net FrameWork版本才可以启动）等，可以右键安装项目，在**View**中可以进行选择设置，如下

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/15.png" width="70%">

   有需要可以自行研究……

7. 设置系统必备

   一般我们开发的程序都有一个目标框架，也就是所依赖的**.net Framework**版本环境，如**.net Framework 2.0/3.5/4.0/4.5**等。

   要想我们的程序能在电脑上正常运行，首先就得保证电脑上装有指定的**.net Framework**版本框架，可以在安装包的**属性**中设置，启动安装前检查操作系统中是否安装了指定版本的框架或其他依赖，设置方法如下：

   右键安装包项目，点开“属性”

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/16.png" width="70%">

   然后点击“**Prerequisites……**”

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/17.png" width="70%">

   选择你程序需要的**.net Framework**版本以及其他依赖项。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/18.png" width="70%">

   选择“**从组件供应商的网站上下载系统必备组件**”，这样一来，即使电脑上没有安装需要的**.net Framework**也不要紧，只要设置了这项，安装程序会自动从微软的官网上下载对应的组件并安装。

8. 生成打包安装文件

   右键安装项目，选择**重新生成**。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/19.png" width="70%">

   然后打开解决方案文件夹下的Debug或Release文件夹,就可以看到生成的安装文件。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-29-Browser%20user%20information%20Decrypt/assert/20.png" width="70%">

   生成的setup.exe与setup.msi的区别
   setup.exe里边包含了对安装程序的一些条件的检测，比如需要.net的版本是否安装等，当条件具备后，setup.exe接着调用setup.msi,而setup.msi则可以直接运行，如果你确定条件都具备的情况下。

# 项目已上传至GitHub

[Browser_Decrypt](https://github.com/Cr7-joker/Browser_Decrypt)