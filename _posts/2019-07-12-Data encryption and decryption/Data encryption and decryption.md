---
title: Data encryption and decryption
tags: Decrypt Encrypt
edit: 2019-07-12
categories: Technology
status: Completed
description: Encrypting and decrypting data based on Windows API CryptProtectData()/CryptUnProtectData()
---

# CryptProtectData function

The **CryptProtectData** function performs encryption on the data in a DATA_BLOB structure. Typically, only a user with the same logon credential as the user who encrypted the data can decrypt the data. In addition, the encryption and decryption usually must be done on the same computer.

## Syntax

```c++
DPAPI_IMP BOOL CryptProtectData(
  DATA_BLOB                 *pDataIn,
  LPCWSTR                   szDataDescr,
  DATA_BLOB                 *pOptionalEntropy,
  PVOID                     pvReserved,
  CRYPTPROTECT_PROMPTSTRUCT *pPromptStruct,
  DWORD                     dwFlags,
  DATA_BLOB                 *pDataOut
);
```

## Parameters

```
pDataIn
```

A pointer to a DATA_BLOB structure that contains the plain text to be encrypted.

```
szDataDescr
```

A string with a readable description of the data to be encrypted. This description string is included with the encrypted data. This parameter is optional and can be set to **NULL**.

```
pOptionalEntropy
```

A pointer to a DATA_BLOB structure that contains a password or other additional entropy used to encrypt the data. The **DATA_BLOB** structure used in the encryption phase must also be used in the decryption phase. This parameter can be set to **NULL** for no additional entropy.

```
pvReserved
```

Reserved for future use and must be set to **NULL**.

```
pPromptStruct
```

A pointer to a CRYPTPROTECT_PROMPTSTRUCT structure that provides information about where and when prompts are to be displayed and what the content of those prompts should be. This parameter can be set to **NULL** in both the encryption and decryption phases.

```
dwFlags
```

This parameter can be one of the following flags.

| Value                          | Meaning                                                      |
| :----------------------------- | :----------------------------------------------------------- |
| **CRYPTPROTECT_LOCAL_MACHINE** | When this flag is set, it associates the data encrypted with the current computer instead of with an individual user. Any user on the computer on which **CryptProtectData** is called can use CryptUnprotectData      to decrypt the data. |
| **CRYPTPROTECT_UI_FORBIDDEN**  | This flag is used for remote situations where presenting a user interface (UI) is not an option. When this flag is set and a UI is specified for either the protect or unprotect operation, the operation fails and GetLastError returns the ERROR_PASSWORD_RESTRICTION code. |
| **CRYPTPROTECT_AUDIT**         | This flag generates an audit on protect and unprotect operations. |

```
pDataOut
```

A pointer to a DATA_BLOB structure that receives the encrypted data. When you have finished using the **DATA_BLOB** structure, free its **pbData** member by calling the LocalFree function.

## Return Value

If the function succeeds, the function returns **TRUE**.

If the function fails, it returns **FALSE**.



# CryptUnprotectData function

The **CryptUnprotectData** function decrypts and does an integrity check of the data in a DATA_BLOB structure. Usually, the only user who can decrypt the data is a user with the same logon credentials as the user who encrypted the data. In addition, the encryption and decryption must be done on the same computer. 

## Syntax

```c++
DPAPI_IMP BOOL CryptUnprotectData(
  DATA_BLOB                 *pDataIn,
  LPWSTR                    *ppszDataDescr,
  DATA_BLOB                 *pOptionalEntropy,
  PVOID                     pvReserved,
  CRYPTPROTECT_PROMPTSTRUCT *pPromptStruct,
  DWORD                     dwFlags,
  DATA_BLOB                 *pDataOut
);
```

## Parameters

```
pDataIn
```

A pointer to a DATA_BLOB structure that holds the encrypted data. The **DATA_BLOB** structure's **cbData** member holds the length of the **pbData** member's byte string that contains the text to be encrypted.

```
ppszDataDescr
```

A pointer to a string-readable description of the encrypted data included with the encrypted data. This parameter can be set to **NULL**. When you have finished using *ppszDataDescr*, free it by calling the LocalFree function.

```
pOptionalEntropy
```

A pointer to a DATA_BLOB structure that contains a password or other additional entropy used when the data was encrypted. This parameter can be set to **NULL**; however, if an optional entropy **DATA_BLOB** structure was used in the encryption phase, that same **DATA_BLOB** structure must be used for the decryption phase. 

```
pvReserved
```

This parameter is reserved for future use and must be set to **NULL**.

```
pPromptStruct
```

A pointer to a CRYPTPROTECT_PROMPTSTRUCT structure that provides information about where and when prompts are to be displayed and what the content of those prompts should be. This parameter can be set to **NULL**.

```
dwFlags
```

A **DWORD** value that specifies options for this function. This parameter can be zero, in which case no option is set, or the following flag.

| Value                              | Meaning                                                      |
| :--------------------------------- | :----------------------------------------------------------- |
| **CRYPTPROTECT_UI_FORBIDDEN**      | This flag is used for remote situations where the user interface (UI) is not an option. When this flag is set and UI is specified for either the protect or unprotect operation, the operation fails and GetLastError returns the ERROR_PASSWORD_RESTRICTION code. |
| **CRYPTPROTECT_VERIFY_PROTECTION** | This flag verifies the protection of a protected BLOB. If the default protection level configured of the host is higher than the current protection level for the BLOB, the function returns **CRYPT_I_NEW_PROTECTION_REQUIRED** to advise the caller to again protect the plain text contained in the BLOB. |

```
pDataOut
```

A pointer to a DATA_BLOB structure where the function stores the decrypted data. When you have finished using the **DATA_BLOB** structure, free its **pbData** member by calling the LocalFree function.

## Return Value

If the function succeeds, the function returns **TRUE**.

If the function fails, it returns **FALSE**.

# Example

```c++
#pragma comment(lib, "crypt32.lib")
#include <iostream>
#include <windows.h>

int main()
{
	DATA_BLOB DataIn;
	DATA_BLOB DataOut;
	DATA_BLOB DataVerify;
	BYTE* pbDataInput = (BYTE*)"Hello world of data protection.";
	DWORD cbDataInput = strlen((char*)pbDataInput) + 1;
	DataIn.pbData = pbDataInput;
	DataIn.cbData = cbDataInput;
	LPWSTR pDescrOut = NULL;
	//-------------------------------------------------------------------
	//  Begin processing.
	printf("The data to be encrypted is: %s\n", pbDataInput);
	//-------------------------------------------------------------------
	//  Begin protect phase.
	if (CryptProtectData(
		&DataIn,
		L"This is the description string.", // A description string. 
		NULL,                               // Optional entropy
		NULL,                               // Reserved.
		NULL,                      // Pass a PromptStruct.
		0,
		&DataOut))
	{
		printf("The encryption phase worked. \n");
	}
	else
	{
		printf("Encryption error!");
	}
	//-------------------------------------------------------------------
	//   Begin unprotect phase.
	if (CryptUnprotectData(
		&DataOut,
		&pDescrOut,
		NULL,                 // Optional entropy
		NULL,                 // Reserved
		NULL,        // Optional PromptStruct
		0,
		&DataVerify))
	{
		printf("The decrypted data is: %s\n", DataVerify.pbData);
		printf("The description of the data was: %S\n", pDescrOut);
	}
	else
	{
		printf("Decryption error!");
	}
	//-------------------------------------------------------------------
	//  Clean up.
	LocalFree(pDescrOut);
	LocalFree(DataOut.pbData);
	LocalFree(DataVerify.pbData);
} // End of main
```

`CryptProtectData()`和`CryptUnprotectData()`在`Windows.h`头文件下，且函数依赖于`crypt32.lib`静态链接文件，使用前需将其都导入项目中。

加密的测试数据为`“Hello world of data protection.”`，上述函数的加密基于`DATA_BLOB`数据类型，其中`pbData`存储字节类型的数据，`cbData`为数据长度，且C++中`BYTE*`类型其实为`unsigned char*`类型，其长度比`char*`长一(多一个`'\0'`)。