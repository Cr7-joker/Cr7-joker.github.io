---
title: C++ based calculator development
tags: C++ Calulator
edit: 2019-03-25
categories: C++
status: Completed
description: 基于C++的计算器开发，包括数学表达式的判断正误，以及计算
---

# 表达式正误判断

## 原理

通过**递归下降法**进行数学表达式的判断

### 终结符与非终结符：

**终结符**是一个形式语言的基本符号。就是说，它们能在一个形式语法的推导规则的输入或输出字符串存在，而且它们不能被分解成更小的单位。确切地说，一个语法的规则不能改变终结符。例如说，下面的语法有两个规则：

1. *x* -> *xa*
2. *x* -> *ax*

在这种语法之中，*a*是一个终结符，因为没有规则可以把*a*变成别的符号。不过，有两个规则可以把*x*变成别的符号，所以*x*是非终结符。一个形式语法所推导的形式语言必须完全由终结符构成。

---

**非终结符**是可以被取代的符号。一个形式文法中必须有一个起始符号；这个起始符号属于非终结符的集合。

在上下文无关文法中，每个推导规则的左边只能有一个非终结符而不能有两个以上的非终结符或终结符。并非所有的语言都可以被上下文无关文法产生。

### 递归下降法

是语法分析中的一种方法，主要原理：

对每个**非终结符**按其产生式结构构造相应语法分析子程序，其中**终结符**产生匹配命令，而**非终结符**则产生过程调用命令。

递归下降分析程序的实现思想是：识别程序由一组子程序组成。每个子程序对应于一个非终结符号。

每一个子程序的功能是：选择正确的右部，扫描完相应的字。在右部中有非终结符号时，调用该非终结符号对应的子程序完成。

## 数据结构

```c++
vector<pair<string, int>> word	//可变数组pair类型存储符号数字及对于标识ID
string expr; //数学表达式
```

## 词法分析

```c++
int word_analysis(vector<pair<string, int>>& word, string expr)
{
	//删除 开放sqrt 中qrt字符串
	int pos = 0;
	while ((pos = expr.find("qrt")) != -1)
	{
		expr.erase(pos, 3);
	}

	word.push_back(make_pair(" ", 0));
	for (int i = 0; i < expr.length(); ++i)
	{
		// 如果是 + - * / ( ) ^ 
		if (expr[i] == '(' || expr[i] == ')' || expr[i] == '+'
			|| expr[i] == '-' || expr[i] == '*' || expr[i] == '/' 
			|| expr[i] == '^' || expr[i] == 'S')
		{
			string tmp;
			tmp.push_back(expr[i]);
			switch (expr[i])
			{
			case '+':
				word.push_back(make_pair(tmp, 1));
				break;
			case '-':
				word.push_back(make_pair(tmp, 2));
				break;
			case '*':
				word.push_back(make_pair(tmp, 3));
				break;
			case '/':
				word.push_back(make_pair(tmp, 4));
				break;
			case '(':
				word.push_back(make_pair(tmp, 6));
				break;
			case ')':
				word.push_back(make_pair(tmp, 7));
				break;
			case '^':
				word.push_back(make_pair(tmp, 8));
				break;
			case 'S':
				word.push_back(make_pair(tmp, 9));
				break;
			}
		}
		// 如果是数字开头
		else if (expr[i] >= '0' && expr[i] <= '9')
		{
			string tmp;
			while (expr[i] >= '0' && expr[i] <= '9')
			{
				tmp.push_back(expr[i]);
				++i;
			}
			if (expr[i] == '.')
			{
				++i;
				if (expr[i] >= '0' && expr[i] <= '9')
				{
					tmp.push_back('.');
					while (expr[i] >= '0' && expr[i] <= '9')
					{
						tmp.push_back(expr[i]);
						++i;
					}
				}
				else
				{
					return -1;  // .后面不是数字，词法错误
				}
			}
			word.push_back(make_pair(tmp, 5));
			--i;
		}
		// 如果以.开头
		else
		{
			return -1;  // 以.开头，词法错误
		}
	
	}
	for (int i = 1; i < word.size(); ++i) 
	{
		if (word[i].second == 9)
		{
			if (word[i + 1].second != 6)
				return -1;	//根号后面必须跟左括号
			if (word[i - 1].second == 5)
				return -1;	//根号前面必须是符号
		}
	}
	
	return 0;
}
```

**解释：**为每个运算符分配相应的数字ID，若是数字则读取到下一个非数字符号将以读取数字字符串分配数字ID。对逗号（**.**），开方（**Sqrt**）,做简单的格式判断

## 语法分析

```c++
int idx = 1;
int sym;	//标识ID
int err = 0;	// 错误

void T();
void F();
void X();

// 读下一单词的种别编码
void Next()
{
	if (idx < word.size())
		sym = word[idx++].second;
	else
		sym = 0;
}

// E → T { +T | -T } 
void E()
{
	T();
	while (sym == 1 || sym == 2)
	{
		Next();
		T();
	}
}

// T → F { *F | /F } 
void T()
{
	F();
	while (sym == 3 || sym == 4)
	{
		Next();
		F();
	}
}

// F→	X { ^F | sqrt(F } 
void F()
{
	X();
	while (sym == 8 || sym == 9)
	{
		Next();
		X();
	}
}

// X → (E) | d
void X()
{
	if (sym == 5)
	{
		Next();
	}
	else if (sym == 6)
	{
		Next();
		E();
		if (sym == 7)
		{
			Next();
		}
		else
		{
			err = -1;
		}
	}
	else if (sym == 2)
	{
		if (word[idx - 2].second != 6) {
			err = -1;
		}
	}
	else if (sym == 9)
	{
		if (word[idx - 2].second == 5) {
			err = -1;
		}
	}
	else
	{
		err = -1;
	}
}

```

**解释：**读下一单词的标识数字ID，根据不同的ID，进行相应的子程序，并进行循环递归调用，直到标识ID**sym**读取完成归0，根据**err**的内容进行判断正误

## 主函数

```c++
int main()
{
	cin >> expr;
	int err_num = word_analysis(word, expr);
	if (-1 == err_num)
	{
		cout << "Wrong Expression." << endl;
	}
	else
	{
		// 测试输出
		Next();
		E();
		if (sym == 0 && err == 0)  // 注意要判断两个条件
			cout << "Right Expression." << endl;
//		{			
//			try
//			{
//				double tmp = getInfo(expr);
//				if (isinf(tmp) || isnan(tmp)) {
//					cout << "Wrong Expression." << endl;
//				}
//				else {
//					cout << tmp << endl;
//				}
//			}
//			catch (exception e)
//			{
//				cout << "Wrong Expression." << endl;
//			}
//		}
		else
			cout << "Wrong Expression." << endl;
	}
	system("pause");
	return 0;
}
```

**解释：**先调用词法分析，在进行语法分析，调用**Next()**函数，进行下一单词的读取，**E()**函数判断开始，最后根据返回值判断。

# 表达式计算

此部分请看[合作开发计算模块代码](<http://www.ljijcj.top/2019/03/22/calculator/>)**（代码加解释）**

# [Github源码](<https://github.com/Cr7-joker/Calculator>)

