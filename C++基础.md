[TOC]
[学习网站链接]: https://www.learncpp.com/

## 一、基础
### 1.1语言与程序结构
#### Q&A
1. 什么是语句？
答:是计算机程序中的一个指令，它告诉计算机去执行一个操作
2. 什么是函数？
答:函数是一系组按顺序执行的语句
3. 所有程序必现具备的函数？
答：main函数
4. 程序执行从哪里开始？
答：main函数的第一个语句开始执行
5. c++语句以什么结尾？
答：semicoion(:)，分号
6. 什么是语法错误？
答：程序违反c++语言语法规则时编译产生错误
7. 什么是C++标准库？
答：库文件是可打包复用在其他程序的预编译代码集合，c++标准库是c++语言附加库，包含一些附加功能可被用于你的程序

### 1.1注释
```c++
单行注释
//单行
多行注释
/*多行*/
```
### 1.3对象和变量
1. 一般程序中对象通常指变量、内存中的数据结构、或者函数，c++中对象不包括函数
2. 变量实例化 int x;
3. 数据类型（int，double等）
4. 定义多个变量
```
int a,b;
int a;
double b;
```
#### Q&A
1. 什么是数据？
答：可以被计算机移动，处理，存储的一些信息
2. 什么是值？
答：存储在内存中的单块数据
3. 什么是变量？
答：一个命名的内存空间
4. 什么是标识符？
答：被访问变量的名称
5. 什么是类型？
答：告诉程序怎么在内存中解释一个值
6. 什么是整数？
答：没有小数部分写入数字

### 1.4变量赋值和初始化
#### 变量赋值
```C++
int width;
width=5;
```

#### 初始化
```C++
//复制初始化
int width=5;//将值 5 的初始化复制到变量width
//直接初始化(对于简单数据类型与复制初始化一致，对复杂数据类型，直接初始化更有效率)
int width(5);
//列表初始化
int width{5};
int height = {6};
int depth {};
int eidth={4.5};//小数部分值不适用于整数类型，此时初始化会删掉小数部分
//值初始化+零初始化
int x{0};
std::cout << x;//zero初始化
int x{};
std::cout >>x;//值初始化
```
#### 初始化变量
1. 在创建时初始化
2. 初始化多个变量
```
int a,b;
int a=5,b=6;
int a(5),b(6);
int e{9},f{10};
```
3. 建议直接初始化或者列表初始化

#### Q&A
1. 初始化与赋值区别？
答：初始化在变量创建时提供初始值，赋值在变量创建之后为变量赋予一个值
2. 使用什么形式初始化？
答：直接使用列表初始化

### 1.5iostream简介：cout、cin、endl
#### std::cout
```
//将文本输出到终端
#include <iostream>
int main()
{
	std::cout << "hello world";//使用提取操作符
	return 0;
}
```
#### std::end1 vs '\n'

```c++
{
	std::cout << "hello world" << std::end1;
	/*std::end1换行后会进行刷新但是std::cout输出本来就好刷新输出*/
	std::cout << "hello world" << '\n'; //'\n'不会进行多余刷新，性能更好
	return 0;
}
```

#### std::cin 
```c++
#include <iostream>
int main()
{
	int x{}
	std::cin >> x; //从控制台获取数值并保存到变量x
	std::cout << "you entered:" << x << '\n'
}
```

### 1.7关键词和命名标识符
#### 关键词
在c++中有特殊含义
#### 命名标识符
* 标识符不能是关键字。保留关键字
* 标识符只能由字母（小写或大写）、数字和下划线字符组成。这意味着名称不能包含符号（下划线除外）或空格（空格或制表符）
* 标识符必须以字母（小写或大写）或下划线开头。它不能以数字开头
* C++ 区分大小写，因此区分大小写字母。 `nvalue`不同于`nValue`不同于 不同于`NVALUE`
```c++
/*变量命名,小写字母开头，如果是一个词则全是小写*/
int value;
int my_variable_name;//多词用_分隔
int my_variable_name();
int myVariableNmae;//后续第一个词大写形式
int myVariableNmae();
/**/
```
### 1.8空格和基本格式
#### 空格
1. 空格缩进在c++中没有要求，分成两行也能编译（输出字符串除外）
```c++
std::cout << "helllo
			world"//not allowed
```
#### 基本格式
	* 可以使用制表符或空格进行缩进
	* 函数形式
	```c++
	int main()
	{
		std::cout<<"helloworld";
	}
	```
	* 花括号内的每个语句都应该从它所属函数的左大括号开始一个制表符
	* 每行不超过80字符
	* 运算符拆分长行，运算符放在下一行开头
	```c++
	std::cout << 3+4
		+5+6
		*7*8;
	```
	* 通过对齐值或注释或在代码块之间添加间距，使用空格使您的代码更易于阅读

### 1.9常量和运算符
#### 常量
常量的值不可变，变量的值可变
```c++
std::cout << "Hello world!";//“hello world！”是常量
int x{ 5 };//5是常量
```
#### 运算符
```
加减乘除：+-*/
赋值:=
插入提取:<< >>
链式操作符：std::cout << 1+2*3*4;
```

### 1.10表达式介绍
#### Q&A
1. 什么是表达式？
答：表达式被执行时，每一项会被计算，直到剩单个值为止，该值为表达式结果
```
2               // 2 is a literal that evaluates to value 2
"Hello world!"  // "Hello world!" is a literal that evaluates to text "Hello world!"
x               // x is a variable that evaluates to the value of x
2 + 3           // 2 + 3 uses operator + to evaluate to value 5
x = 2 + 3       // 2 + 3 evaluates to value 5, which is then assigned to variable x
std::cout << x  // x evaluates to the value of x, which is then printed to the console
常量的值是自身，变量的值是value

```
2. 什么是表达式语句？
答：由表达式+分号组成的语句，当语句被执行，表达式被计算

### 1.12总结
#### Q&A
1. 初始化和赋值区别？
答：初始化是在变量创建时给初始值，赋值是创建后给变量一个值
2. 什么时候会发生未定义行为？后果是什么？
答：没有按c++语言规范做事，可能会crash，产生错误

## 二、函数和文件
### 2.1函数介绍

return为函数提供一种将值返回给调用者的方法

函数提供一种减少冗余程序的方法

#### 定义函数示例
```c++
return-type identifier() // 用函数名替换的标识符
{
// 你的代码在这里
}
/*
1. return-type:返回类型；void表示不返回；int表示返回整数
2. 函数名：identifier
3. 标识符后面加()告诉编译器我们在定义函数
4. 花括号+中间语句是函数体*/
```
#### 函数多次调用and函数调用函数
```c++
#include <iostream>

void doB()
{
    std::cout << "In doB()\n";
}

void doA()
{
    std::cout << "Starting doA()\n";
    doB();
    std::cout << "Ending doA()\n";
}

int main()
{
    std::cout << "Starting main()\n";
    doA();
    doB();
    doB();
    std::cout << "Ending main()\n";
    return 0;
}
```
#### 注意
c++函数不支持嵌套函数

### 2.2函数返回值

#### 返回值
```c++
#include <iostream>

int getValueFromUser()
{
    int num{};
    std::cin>> num;
    return num;//返回值
}
int main()
{
    int num{getValueFromUser()};
    std::cout << "double is " << 2*num <<'\n';
    return 0;
}
```
#### 无效返回值
```c++
void doPrint() // void is the return type
{
    std::cout << "In doPrint()" << '\n';//返回类型是void，表示不需要返回值
}
```
#### 函数重用

减少冗余代码

```c++
#include <iostream>

int getValueFromUser()
{
 	std::cout << "Enter an integer: ";
	int input{};
	std::cin >> input;

	return input;
}

int main()
{
    int x{ getValueFromUser() }; // first call to getValueFromUser
    int y{ getValueFromUser() }; // second call to getValueFromUser

    std::cout << x << " + " << y << " = " << x + y << '\n';

    return 0;
}
```

### 2.3函数参数和实参
```c++
#include <iostream>

int doubleNumber(int x)
{
    return 2*x;
}

int main()
{
    int x{};
    std::cin >> x;
    std::cout << doubleNumber(x) << '\n';
    return 0;
}
```
### 2.4局部作用域
### 2.5前向声明
### 2.6多文件程序
### 2.7命名空间
### 2.8预处理器
一旦预处理器完成，该文件中所有定义的标识符都将被丢弃。这意味着指令仅从定义点到定义它们的文件末尾有效。在一个代码文件中定义的指令不会影响同一项目中的其他代码文件
```c++
#include <iostream> //预处理
#define PRINT_JOE   //宏定义

int main()
{
#ifdef PRINT_JOE    //条件编译
    std::cout << "Joe\n";
#endif 

#ifdef PRINT_BOB
    std::cout << "Bob\n";
#endif
    return 0;
}
```
### 2.9头文件
1. 扩展名后缀是（xxx.h）
2. 偶尔会看到它们带有 .hpp 扩展名或根本没有扩展名
3. 头文件的主要目的是将声明传播到代码文件
```c++
//add.h文件
int add(int x, int y);
//main.cpp
#include "add.h" 
#include <iostream>

int main()
{
    std::cout << "The sum of 3 and 4 is " << add(3, 4) << '\n';
    return 0;
}
//add.cpp
#include "add.h"

int add(int x, int y)
{
    return x + y;
}
```

### 2.10头部保护
1. 解决重复定义问题
```c++
#ifndef ADD_H
#define ADD_H

int add(int x, int y);

#endif
```

## 三、调试
## 四、基本数据类型
```c++
#include <iostream>

int main()
{
    int x{};
    std::cout << "x is " << sizeof(x) << " bytes\n";//sizeof查看内存大小

    return 0;
}
```
```c++
//unsigned定义的整数不会溢出，会环绕超出1位输出0，超出2输出1，超出3输出2
#include <iostream>

int main()
{
    unsigned short x{ 65535 }; // largest 16-bit unsigned value possible
    std::cout << "x was: " << x << '\n';

    x = 65536; // 65536 is out of our range, so we get wrap-around
    std::cout << "x is now: " << x << '\n';

    x = 65537; // 65537 is out of our range, so we get wrap-around
    std::cout << "x is now: " << x << '\n';

    return 0;
}
/*结果
x was: 65535
x is now: 0
x is now: 1
*/
```
```c++
//反向超出环绕输出:-1输出最大位，-2输出最大位减一
#include <iostream>

int main()
{
    unsigned short x{ 0 }; // smallest 2-byte unsigned value possible
    std::cout << "x was: " << x << '\n';

    x = -1; // -1 is out of our range, so we get wrap-around
    std::cout << "x is now: " << x << '\n';

    x = -2; // -2 is out of our range, so we get wrap-around
    std::cout << "x is now: " << x << '\n';

    return 0;
/*
x was: 0
x is now: 65535
x is now: 65534
*/
}
```
```c++
#include <cstddef> // std::size_t
#include <iostream>

int main()
{
	std::cout << sizeof(std::size_t) << '\n';//size_t可以查询系统byte数

	return 0;
}
```