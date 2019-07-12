---
title: C++ Basic use of sqlite3
tags: C++ Database
edit: 2019-07-12
categories: C++
status: Completed
description: Basic operation of sqlite3 database through C++
---

# SQLite3简介

SQLite3只是一个轻型的嵌入式数据库引擎，占用资源非常低，处理速度比Mysql还快，专门用于移动设备上进行适量的数据存取，它只是一个文件，不需要服务器进程。

SQL语句是SQL操作的指令，我们用C/C++访问数据库时，需要用char*即C字符串来保存SQL语句，然后调用相应sqlite3库的函数，传入C字符串，来执行SQL指令。

常用术语**：**表(table)、字段(column，列，属性)、记录(row，record)。

# **SQL(structured query language)语句** 

**特点**：不区分大小写，每条语句后加";"结尾。

**关键字**：select、insert、update、delete、from、creat、where、desc、order、by、group、table、alter、view、index等，数据库中不能使用关键字命名表和字段。

**存储类型：**integer(整型)、real(浮点型)、text(文本字符串)、blob(二进制数据)。

实际上SQLite是无类型的，建表时声明的类型是为了方便程序员之间的交流，是一种良好的编程规范。

## 数据定义语句(DDL：Data Definition Language)

1. 新建表 ⟹ create：create table 表名 (字段名1 字段类型1，字段名2 字段类型2，……); create table if not exists 表名 (字段名1 字段类型1，字段名2 字段类型2，……);

   ```sql
   CREATE TABLE IF NOT EXISTS Person (id integer PRIMARY KEY AUTOINCREMENT, name text NOT NULL, age integer NOT NULL);
   ```

2. 删除表 ⟹ drop：dorp table 表名；drop table if exists 表名；

   ```sql
   DROP TABLE IF EXISTS Person; 
   ```

## 数据操作语句(DML：Data Manipulation language)

1. 添加表中的数据 ⟹ insert：insert into 表名 (字段1，字段2，……) values (字段1的值，字段2的值);

   *字符串内容用单引号。*

   ```sql
   INSERT INTO Person (name, age) VALUES ('Leslie', 20); 
   ```

2. 修改表中的数据 ⟹ update：update 表名 set 字段1 ＝ 字段1的值，字段2 ＝ 字段2的值，……;

   ```sql
   UPDATE Person SET name = 'Shang', age = 18; /* 把表中name字段的值全部改成Shang，age字段的值全部改成18。*/
   ```

   ```sql
   UPDATE Person SET age = 12 WHERE name = 'Leslie'; /* 把表中name字段值是Leslie的age值改为12。*/
   ```

3. 删除表中的数据 ⟹ delete：delete from 表名；delete from 表名 where 字段 ＝ 字段值。

   ```sql
   DELETE FROM Person WHERE age > 12 AND age < 15; /* 删除表中年龄大于12且小于15的记录。*/
   ```

## **数据查询语句(DQL：Data Query Language)**

1. select：select 字段1， 字段2， 。。。 from 表名；select 字段1， 字段2，…… from 表名 where 字段 ＝ 某值；select * from 表名；(查询所有的字段)

   ```sql
   SELECT name, age FROM Person WHERE age < 20; 
   ```

   ```sql
   SELECT * FROM Person WHERE age < 20; 
   ```

2. 计算记录条数：select count(字段或者*) from 表名；

   ```sql
   SELECT count(name) FROM Person WHERE age > 20; 
   ```

   ```sql
   SELECT count(*) FROM Person WHERE age > 20; 
   ```

3. where：where 字段 ＝ 某值；where 字段 is 某值；where 字段 !＝ 某值；where 字段 is not 某值；where 字段 > 某值；where 字段1 ＝ 某值1 and 字段2 < 某值2；where 字段1 ＝ 某值1 or 字段2 > 某值2；

4. order by：select * from 表名 order by 字段(默认升序)；select * from 表名 order by 字段 desc(降序)；select * from 表名 order by 字段 asc(升序)；select * from 表名 order by 字段1 asc(先按字段1升序)，字段2 desc(再按字段2降序)；

   ```sql
   SELECT * FROM Person WHERE age < 20 ORDER BY age DESC, name ASC; /* 先按年龄降序，再按名字升序。*/  
   ```

5. limit：select * from 表名 limit 数值1，数值2；分页查询，数值1表示跳过前面多少条，数值2表示取出之后多少条。select * from 表名 limit 数值2；(跳过前面0条，相当于select * from 表名 limit 0，数值2，表示最前面多少条数据)

   ```sql
   SELECT * FROM Person WHERE age < 20 ORDER BY age DESC, name ASC LIMIT 3, 5; /* 先筛选，后排序，再分页。*/ 
   ```

6. like：模糊查询，select 字段1， 字段2， 。。。 from 表名 where 字段 like ％某值％；

   ```sql
   SELECT * FROM Person WHERE name like '%esli%'; 
   ```

## 字段约束

- not null：字段的值不能为空。
- unique：字段的值必需唯一。
- default：指定字段的默认值。
- primary key：主键，用来唯一的标识某条记录，相当于记录的身份证。主键可以是一个或多个字段，应由计算机自动生成和管理。主键字段默认包含了not null和unique两个约束。
- autoincrement：当主键是integer类型时，应该增加autoincrement约束，能实现主键值的自动增长。

```sql
CREATE TABLE IF NOT EXISTS Person (id integer PRIMARY KEY AUTOINCREMENT, name text NOT NULL UNIQUE, age integer NOT NULL DEFAULT 30); 
```

## 外键

利用外键约束可以用来建立表与表之间的联系，一般是一张表的某个字段，引用着另一张表的主键的字段。

1. 创建一个表：

   ```sql
   CREATE TABLE IF NOT EXISTS Class (id integer PRIMARY KEY AUTOINCREMENT, name text NOT NULL UNIQUE);
   ```

2.  创建一个带外键的表：Student表中有一个叫做fk_student_class的外键，这个外键的作用是让Student表中的class_id字段引用Class表中的id字段。

   ```sql
   CREATE TABLE IF NOT EXISTS Student (id integer PRIMARY KEY AUTOINCREMENT, name text NOT NULL, age integer NOT NULL, class_id integer NOT NULL, CONSTRAINT fk_student_class FOREIGN KEY (class_id) REFERENCES Class(id)); 
   ```

3. 利用外键来查询多张表中的数据：

   ```sql
   SELECT s.name s_name, s.age s_age, c.name c_name FROM Student s, Class c WHERE s.class_id = c.id;　// 查询所有学生对应的班级 
   ```

   ```sql
   SELECT * FROM Student WHERE class_id = (SELECT id FROM Class WHERE name = '四班'); // 查询四班的所有学生
   ```

# C++ 上使用SQLite3

## 项目环境配置

1. 下载需要的文件

   [官方下载地址](https://www.sqlite.org/download.html)

   SQLite官方下载页只提供*SQLite3.def*和*SQlite3.dll*文件的下载，若使用VS2019编程的话，还需要SQLite3.lib库文件，才能调用编译成功。我们可以使用 VS2019 提供的 **X:\VS2019\VC\Tools\MSVC\14.22.27812\bin\Hostx64\x86\lib.exe** 程序生成 SQLite3.lib 库文件。(我用的是VS2019)

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/01.png" width="70%">

   下载适合自己的*dll*文件，我这里下载的是*win32位 x86*的。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/02.png" width="70%">

   下载源代码文件*amalgamation*。

2. 解压文件到文件夹

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/03.png" width="70%">

3. cmd命令行运行lib.exe程序生成*SQLite3.lib*和*SQlite3.exp*文件

   运行cmd，输入

   `"D:\VS2019\VC\Tools\MSVC\14.22.27812\bin\Hostx64\x86\lib.exe" /MACHINE:IX86 /DEF:D:\SQLite3\SQLite3.def /OUT:D:\SQLite3\SQLite3.lib`

   结果如下图所示：

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/04.png" width="70%">

   也可以将lib.exe程序路径加入环境变量，方便cmd命令行输入。

   我的电脑，右键`属性`,选择`高级系统设置`，进入`环境变量`，在`系统变量`里选择`Path`进行`编辑`，`新建`，将lib程序路径添加进来。

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/05.png" width="70%">

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/06.png" width="70%">

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/07.png" width="70%">

   即可在cmd命令行使用lib命令了。

4. VS2019中配置SQLite3

   1. 打开解压后的amalgamation文件夹，将`sqlite3.h`文件复制粘贴进VS2019的`include`目录，路径为`D:\VS2019\VC\Tools\MSVC\14.22.27812\include`。
   2. 将运行产生的`SQLite3.lib`文件放入VS2019的`lib`目录，路径为`D:\VS2019\VC\Tools\MSVC\14.22.27812\lib\x86`。*(根据VS不同编译器选择是放在x86还是x64，不确定可以都放)*
   3. 将解压产生的`SQLite3.dll`文件放入VS2019`bin`的目录，路径为`D:\VS2019\VC\Tools\MSVC\14.22.27812\bin\Hostx64\x86`（根据VS不同编译器选择是放在Host64/x86还是Host64/x64还是Host86/x86还是Host86/x64，不确定可以都放）。

5. 创建新项目，引入SQLite3.h和链接`SQLIte3.lib`即可使用

   ```c++
   #include "sqlite3.h"
   #pragma comment(lib,"sqlite3.lib")
   ```

（PS：这种环境配置方法可以使以后创建的所有项目引入`SQLite3.h`文件和链接`SQLIte3.lib`文件后就可以使用SQLite3）

**另一种对单个项目添加SQLite3环境的方法**：

1. 新建项目

2. 项目属性

   a）添加包含目录，即刚才下载解压后`sqlite3.h`所在路径。

   b）添加库目录，即添加`SQLite3.lib`所在文件路径。 

   <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/08.png" width="70%">

   c）链接器-输入-附加依赖项，输入`SQLite3.lib`。

    <img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/09.png" width="70%">

3. 将`SQLite3.dll`文件放入VS2019`bin`的目录。*（和第一种方法一样）*

## 使用SQLite3

1. 打开或者创建数据库。

   ```c++
   #include <stdio.h>
   #include "sqlite3.h"
   #pragma comment(lib,"sqlite3.lib")
   int main(int argc, char* argv[])
   {
   	sqlite3* db;
   	char* zErrMsg = 0;
   	int rc;
   
   	rc = sqlite3_open("test.db", &db);
   
   	if (rc) {
   		fprintf(stderr, "Can't open database: %s\n", sqlite3_errmsg(db));
   
   	}
   	else {
   		fprintf(stderr, "Opened database successfully\n");
   	}
   	sqlite3_close(db);
   
   	return 0;
   }
   
   ```

2. 执行不返回数据的SQL语句(增、删、改)。

   ```c++
   const char* sql = "INSERT INTO Person(name, age) VALUES('Leslie', 20); ";        //SQL语句
   	sqlite3_stmt* stmt = NULL;        //stmt语句句柄
   
   	//进行插入前的准备工作——检查语句合法性
   	//-1代表系统会自动计算SQL语句的长度
   	int result = sqlite3_prepare_v2(db, sql, -1, &stmt, NULL);
   
   	if (result == SQLITE_OK) {
   		std::clog << "添加数据语句OK";
   		//执行该语句
   		sqlite3_step(stmt);
   	}
   	else {
   		std::clog << "添加数据语句有问题";
   	}
   	//清理语句句柄，准备执行下一个语句
   	sqlite3_finalize(stmt);
   ```

3. 执行返回数据的SQL语句(查)。

   ```c++
   const char* sql = "SELECT name, age FROM t_person WHERE age < 30;";    //SQL语句
   	//进行查询前的准备工作——检查语句合法性
   	//-1代表系统会自动计算SQL语句的长度
   	int result = sqlite3_prepare_v2(db, sql, -1, &stmt, NULL);
   
   	if (result == SQLITE_OK) {
   		std::clog << "查询语句OK";
   		// 每调一次sqlite3_step()函数，stmt语句句柄就会指向下一条记录
   		while (sqlite3_step(stmt) == SQLITE_ROW) {
   			// 取出第0列字段的值
   			const unsigned char* name = sqlite3_column_text(stmt, 0);
   			// 取出第1列字段的值
   			int age = sqlite3_column_int(stmt, 1);
   			//输出相关查询的数据
   			std::clog << "name = " << name << ", age = " << age;
   		}
   	}
   	else {
   		std::clog << "查询语句有问题";
   	}
   	//清理语句句柄，准备执行下一个语句
   	sqlite3_finalize(stmt);
   ```

4. 关闭数据库。

   ```c++
   sqlite3_close(db);
   ```

## 额外工具，使用SQLiteStdio辅助

SQLiteStudio是一个可视化的数据库管理工具。

通过可视化界面，它可以方便快捷地查看或操作数据库信息。

它是程序sqlite数据调试检查不可或缺的辅助工具。

界面大概如下：

<img src="https://raw.githubusercontent.com/Cr7-joker/Cr7-joker.github.io/master/_posts/2019-07-12-C++ Basic%20use%20of%20sqlite3/assert/10.png" width="70%">

[SQLite下载地址](https://sqlitestudio.pl/index.rvt)