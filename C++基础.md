<<<<<<< HEAD
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

## 三、循环
### 3.1 while
```c++
//满足条件后执行代码块
while(condition)
{
   statement(s);
}
```
### 3.2 for
```
//初始化后判断条件才执行代码块
for ( init; condition; increment )
{
   statement(s);
}
```
### 3.3 do...while
```
//先执行代码块，再判断条件
do
{
   statement(s);

}while( condition );
```
### 3.4 循环控制符
1. break 终止循环
2. continue 进入下次循环
3. goto 不推荐
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
```c++
#include <iostream>

int main()
{
    double zero {0.0};
    double posinf { 5.0 / zero }; // positive infinity
    std::cout << posinf << '\n';

    double neginf { -5.0 / zero }; // negative infinity
    std::cout << neginf << '\n';

    double nan { zero / zero }; // not a number (mathematically invalid)
    std::cout << nan << '\n';

    return 0;
}
//结果
inf正无穷
-inf负无穷
nan不确定数
```
### 4.9布尔值
```c++
#include <iostream>

int main()
{
	std::cout <<std::boolalpha;	//输出是打印true、false而不是0/1
    bool b1{true};
    bool b2{false};
    bool b3{!true}; //等同于false
    bool b4{!false}; //等同于true
    bool b{5};//整数转bool；非0为true；0为false
    std::cout << b1<< b2 << b3 << b4 << '\n';
    std::cout <<b;//结果true
    return 0;
}
//结果
1001
```
```c++
//输入布尔值：true/false,并成功打印
#include <iostream>

int main()
{
    std::cout << "enter a boolean value:";
    bool b{};
    std::cin >> std::boolalpha;
    std::cin >> b;
    std::cout << b;
    return 0;
}
```
```c++
//返回布尔值
bool isEqual(int a,int b)
{
    return (a==b);
}
int main()
{
    std::cout << "enter an integer:";
    int x{};
    std::cin >> x;

    std::cout << "enter another integer:";
    int y{};
    std::cin >> y;

    std::cout << std::boolalpha;
    std::cout << x << " and " << y << "are equal?";
    std::cout << isEqual(x,y);
    return 0;
}
```
### 4.10字符
```c++
#include <iostream>

int main()
{
    std::cout << "Input a keyboard character: ";

    char ch{};
    std::cin >> ch;
    std::cout << "You entered: " << ch << '\n';
    std::cout << static_cast<int>(ch);

    return 0;
}
```
### 4.11std::string
```c++
#include <iostream>
#include <string>

int main()
{
    // std::string myName{"alex"};
    std::string myName="john";
    std::cout <<myName;
    return 0;
}
```
```c++
//std::getline(std::cin >> std::ws,para)
#include <iostream>
#include <string>

int main()
{
    std::cout << "Enter your full name: ";
    std::string name{};
    std::getline(std::cin >> std::ws, name);//std::ws通知std::cin忽略前导空格

    std::cout << "Enter your age: ";
    std::string age{};
    std::getline(std::cin >> std::ws, age);

    std::cout << "Your name is " << name << " and your age is " << age << '\n';

    return 0;
}
```
```c++
//string.length()返回是无符合整数需要进行数据类型转换
#include <iostream>
#include <string>

int main()
{
    std::string myName{ "Alex" };
    std::cout << myName.length() << '\n' << static_cast<int>(myName.length());
    return 0;
}
```
Q&A
1. 编写一个程序，要求用户输入他们的全名和年龄。作为输出，告诉用户他们的年龄总和和他们名字中的字母数。为简单起见，将名称中的空格算作一个字母

2. sizeof("hello ,world!")和string.length()结果不同？
```c++
#include <iostream>
#include <string>

int main()
{
    std::string name{"hello ,world!"};
    int a{static_cast<int>(name.length())};
    std::cout << a << '\n';
    std::cout << sizeof("hello ,world!");
    return 0;
}
```

### 4.11Literals(文字常量)

```c++
//八进制和十六进制
#include <iostream>
#include <string>

int main()
{
    int x{012};//result:10
    int y{0xC};//result：12
    std::cout << x << '\n' << y;
    return 0;
}
```
```c++
//打印十/八/十六进制数
```

## 五、函数
### 5.1 内联函数
```c++
#include<iostream>
inline int add(int a,int b)//内联函数不允许循环和switch语句
{
    return a+b;
}
```
### 5.2 函数模板
```c++
#include<iostream>
/*
typename 类型1,typename 类型2，....
template <模板形参表>返回类型 函数名
*/
template <typename T> 
T add(T a,T b)
{
    return a+b;
}

int main()
{
    std::cout << add(10,20) << '\n';
    std::cout <<add(10.2,20.5) << '\n';
    return 0;
}
```

### 5.3 函数嵌套
```c++
#include<iostream>
#include<cmath>

double f(double x)
{
    return x*x*x-5*x*x+16*x-80;
}
double point(double a,double b)
{
    return (a*f(b)-b*f(a))/(f(b)-f(a));
}
double root(double a,double b)
{
    double x,y,y1;
    y1=f(a);
    do
    {
        x=point(a,b);
        y=f(x);
        if (y*y1>0) y1=y,a=x;
        else b=x;
    } while (fabs(y)>= 0.00001);
    return x;
}
int main()

{
    double a,b;
    std::cin >>a >> b;
    std::cout << "root=" << root(a,b) << '\n';
    return 0;
}
```
### 5.4 函数递归
```c++
//汉若塔
#include<iostream>

void Hanoi(int n,char A,char B,char C)
{
    if(n==1) std::cout<< A << "->" <<C<< '\n';
    else
    {
        Hanoi(n-1,A,C,B);
        std::cout<< A << "->" <<C<< '\n';
        Hanoi(n-1,B,A,C);
    }
}

int main()
{
    int x;
    std::cout << "输入X：";
    std::cin >> x;
    Hanoi(x,'A','B','C');
}
```

## 六、数组
**定义：**数组表示一组数据的集合，方便表示大数据，能够循环处理大量数据
```c++
//定长一维数组,实际元素可少于设定长度但不可大于
int A[10]={1,2,3,4}
//不定长,自动捕获数组长度，不设定
int B[]={4,6,5}
//二维数组一维表示法
int A[2][3]={4,6,5}
//二维数组二维表示法
int A[2][3]={{1，3，6}，{8，9}}
//静态数组不初始化，值默认为0；动态默认为随机数
static int A[3]; //全是0
int B[3];//全是随机数
```
### 6.1 数组遍历
```c++
#include<iostream>

int main()
{
    int A[2][3]={1,2,3,4,5,6},AT[3][2],i,j;
    for ( i = 0; i < 2; i++)
        for (j = 0; j < 3; j++)
            AT[j][i]=A[i][j];
    std::cout << "A:"<<'\n';
    for ( i = 0; i < 2; i++)
    {
        for (j = 0; j < 3; j++)
        {
            std::cout << A[i][j] << " ";
        }
        std::cout << '\n'; 
    }
    std::cout << "AT："<< '\n';
    for ( i = 0; i < 3; i++)
    {
        for (j = 0; j < 2; j++)
        {
            std::cout << AT[i][j] << " ";
        }
        std::cout << '\n'; 
    }
    return 0;
}
```

### 6.2 冒泡排序和选择排序
```c++
//冒泡
#include<iostream>
// using namespace std;
#define N 10

int main()
{
    int A[N],i,j,t;
    for ( i = 0; i < N; i++) std::cin >>A[i];//输入数组
    for ( j = 0; j < N-1; j++)
    {
        for (i = 0; i < N-1-j; i++)
        {
            if (A[i] > A[i+1])
            {
                t=A[i],A[i]=A[i+1],A[i+1]=t;
            }
        }
    }
    for (i = 0; i < N; i++) std::cout << A[i] << " ";
    return 0;
}
```
```c++
//选择排序
#include<iostream>
#include<ctime>

void SelectionSort(int A[],int n)
{
    int i,j,k,t;
    for ( i = 0; i < n-1; i++)
    {
        k=i;
        for (j = i+1; j < n; j++)
        {
            if (A[j] < A[k]) k=j;
        }
        if (i!=k)
        {
            t=A[i],A[i]=A[k],A[k]=t;
        }
    }
}

#define N 10
int main()
{
    int A[N],i;
    srand((unsigned int)time(0));
    for ( i = 0; i < N; i++)
    {
        A[i]=rand()%100;
        std::cout <<A[i] << " ";
    }
    std::cout << '\n';
    SelectionSort(A,N);
    for ( i = 0; i < N; i++)
    {
        std::cout << A[i] << ' ';
    }
    return 0;
}
```

### 6.3 顺序查找和二分查找
```c++
//顺序查找
#include<iostream>
int Search(int A[],int n,int find)
{
    int i;
    for ( i = 0; i < n; i++)
    {
        if (A[i]==find) return i;  
    }
    return -1;
}
#define N 10
int main()
{
    int A[N]={18,-3,-12,34,101,211,12,90,77,45},i,find;
    std::cin >> find;
    i=Search(A,N,find);
    if(i>=0) std::cout << "A[" << i << "]=" << find << '\n';
    else std::cout << "not found" << '\n';
    return 0;
}
//二分查找
#include<iostream>

int BinarySearch(int A[],int n,int find)
{
    int low,upper,mid;
    low=0,upper=n-1;
    while (low<=upper)
    {
        mid=low+(upper-low)/2;
        if(A[mid]<find) low=mid+1;
        else if(A[mid]>find) upper=mid-1;
        else return mid;
    }
    return -1;
}

#define N 10
int main()
{
    int A[N]={8,24,30,47,62,68,83,90,92,95},i,find;
    std::cin >>find;
    i=BinarySearch(A,N,find);
    if(i>=0) std::cout << "A[" << i << "]=" << find << '\n';
    else std::cout << "not found" << '\n';
    return 0;
}
```
## 七   指针
### 7.1 指针的定义
* 数据指针、函数指针、数据成员指针、成员指针不能相互转换，复习
```c++
//指针初始化 *指针变量名=地址初值
int a;
int *p=&a;
//指针创建
int a,*p;
p=&a;
//改变指向地址储存的值
#include<iostream>
int main()
{
    int a=10;
    int *p;
    p=&a;
    *p=20;
    std::cout << a;
    return 0;
}
//指针const限定,不允许通过指针来改变const对象的值
#include<iostream>
int main()
{
    const int a=10;
    const int *p;
    p=&a;
    *p=20;//fault
    std::cout << a;
    return 0;
}
//pc不能再指向其他对象,指向int对象的const指针
int a=10,b=20;
int *const pc=&a;
pc=&b;//fault
//指向const对象的const指针
const double pi=3.1415;
const double *const cpc =&pi;
//cpc为指向const对象的const指针
```
### 7.2 指针与数组
```c++
//下面两等价
int a[5],*p
p=a;//1
p=&a[0];//2
//指针访问一维数组
#include<iostream>
int main()
{
    int a[5]={5,8,4,3,4},*p;
    p=a;
    p++;//8
    p++;//4
    std::cout <<*p;//4
    return 0;
}
//通过指针变量间接访问数组元素
#include<iostream>
int main()
{
    int a[5]={5,8,4,3,4},*p;
    for (p=a;p<a+5;p++) std::cout << *p << " ";
    return 0;
}
//通过地址间接访问数组元素
#include<iostream>
int main()
{
    int a[5]={5,8,4,3,4},i;
    for (i=0;i<5;i++) std::cout << *(a+i) << " ";
    return 0;
}
```
### 指针与字符串
```c++
//遍历字符串
#include<iostream>
int main()
{
    char str[]="C language",*p=str;
    while (*p!='\0')
    {
        std::cout << *p++;
    }
    return 0;
}
//访问字符串
#include<iostream>
int main()
{
    char str[]="C language",*p=str;
    std::cout << p << '\n';
    std::cout << p+3 << '\n';
    return 0;
}
```
### 指针与函数
最重要的应用:指针是函数参数传递的重要工具
```c++
//交换变量值,避免了全局变量
#include<iostream>
//交换两变量值
void swap(int *p1,int *p2)
{
    int t;
    t=*p1,*p1=*p2,*p2=t;
}

int main()
{
    int a,b;
    std::cin>> a >> b;
    if(a>b) swap(&a,&b);
    std::cout << "min=" << a << ",max=" << b;
    return 0;
}
//数组做为形参
#include<iostream>

double average(double *a,int n)
{
    double avg=0.0,*p=a;
    int i;
    for ( i = 0; i < n; i++,p++)
    {
        avg=avg+*p;
    }
    return n<=0? 0:avg /n;
}
int main()
{
    double A[5]={1,2,3,4,5};
    std::cout<< "average=" << average(A,5) << '\n';
    return 0;
}
```
## 八  动态分配和内存
### 8.1 new和delete
```c++
//new创建动态对象使用完成后，必须用delete进行销毁
//delete只能销毁由new创建的动态对象，否则程序错误
//避免出现迷途指针，释放内存后要及时设置为空指针
#include<iostream>
int *f1(int n)
{
    int *p,i;
    p=new int[n];
    for ( i = 0; i < n; i++)
    {
        // *(p+i)=i;
        p[i]=i;
    }
    return p;
}
void f2(int *p,int n)
{
    while (n-->0)
    {
        std::cout << *p++ << " ";
    }
}
void f3(int *p)
{
    delete [] p;
}
int main()
{
    int *pi;
    pi=f1(5);
    f2(pi,5);
    f3(pi);
    return 0;
}
```
```c++
#include<iostream>
int main()
{
    int *p1;
    char *pz1;
    p1=new int;
    pz1=new char[80];
    delete p1;
    delete [] pz1;
}
```
### 8.2 动态分配数组
```c++
//计算n*n二维数组平均值

#include<iostream>

double AVE(double *A,int N)
{
    int i,j,sum;
    for ( i = 0; i < N; i++)
    {
        for ( j = 0; j < N; j++)
        {
            sum=sum+*(A+i*N+j);
        }
    }
    return sum/(N*N);
}

int main()
{
    int i,j,n=3;
    double *A=new double[n*n];
    for ( i = 0; i < n; i++)
    {
        for ( j = 0; j < n; j++)
        {
            std::cin >> *(A+i*n+j);
        }
    }
    std::cout <<"AVE=" << AVE(A,n) << '\n';
    delete [] A;
    return 0;
}
```
### 8.3 动态分配字符串
```c++
#include<iostream>
int main()
{
    char *p= new char[1000];//分配字符串空间
    std::cin>>p;//输入
    std::cout <<p;//输出
    delete [] p;//释放空间
}
```

## 九  结构体
* 结构体对象允许赋值,不能算术运算
### 9.1 结构体和数组
```c++
#include<iostream>
#define N 2
struct tagSTUDENT
{
    int no;
    char name[21];
    double score;
} A[N],t;//定义对象
//结构体与数组
int main()
{
    // tagSTUDENT A[N],t;
    int i,j;
    for (i=0;i<N;i++) std::cin >> A[i].no>>A[i].name>>A[i].score;
    for (i=0;i<N-1;i++)
    for (j=1;j<N;j++)
        if (A[i].score<A[j].score||(A[i].score==A[j].score && A[i].no>A[j].no))
        {
            t=A[i],A[i]=A[j],A[j]=t;
        }
    for ( i = 0; i < N; i++)
    {
        std::cout <<A[i].no << "," <<A[i].name << "," <<A[i].score << '\n';
    }
    return 0;
}

```
### 9.2 结构体和指针
```c++
//指针法（p->成员）
//对象法（(*p).成员）
#include<iostream>
struct DATE
{
    int year,month,day;
} d={1981,1,1};
struct TEACHER
{
    int no;
    char name[21];
    DATE *pbirthday;
} a={1001,"lifdf",&d},*p=&a;

int main()
{
    std::cout << p->no << " " <<  a.no << " " << (*p).name<<'\n';
    std::cout << p->pbirthday->year <<" "<< (*p).pbirthday->month;
    return 0;
}
```
### 9.3 结构体和函数
```c++
//结构体对象为实参传递给函数
struct DATA
{
    int data;
    char name[10];
};
void fun1(DATA x);
void fun2()
{
    DATA a={1,"dfjkd"};
    fun1(a);
}
//结构体数组为函数实参
struct DATA
{
    int data;
    char name[10];
};
void fun1(DATA x[]);
void fun2()
{
    DATA A[]={1,"dfjkd",2,"dfjdkgf"};
    fun1(A);
}
//结构体指针为实参
struct DATA
{
    int data;
    char name[10];
};
void fun1(DATA *p);
void fun2()
{
    DATA a={1,"dfjkd"};
    fun1(&a);
}
//函数返回类型是结构体
struct DATA
{
    int data;
    char name[10];
};
DATA fun8()
{
    DATA a={1,"dfdf"};
    return a;//返回结构体对象
}
void fun9()
{
    DATA b;
    b=fun8();
}
```

### 9.4 共用体类型
```c++
#include<iostream>
union A//共用体共用内存空间
{
    int m;
    char a,b;
    short n;
};

int main()
{
    union A x={ 5678 };
    std::cout <<sizeof(x.m) <<" "<< x.m << '\n';
    std::cout <<sizeof(x.n) <<" "<< x.n  << '\n';
    std::cout <<sizeof(x.a) <<" "<< x.a << '\n';
    std::cout <<sizeof(x.b) <<" "<< x.b << '\n';
    return 0;
}
```

### 9.5 枚举类型
```c++
enum COLORS {RED=10,GREEN=8,BLUE,BLACK,WHITE};
//blue=9,black=10,white=11
enum COLORS {RED,GREEN,BLUE,BLACK,WHITE};
//不指定.red=0,green=1....white=4
typedef char byte;//声明一个新类型名代替已有类型
```

## 十 链表
### 10.1 单链表

```c++
//头插法
//头插法创建链表
#include<iostream>
typedef int ElemType;
struct LNode
{
    ElemType data;
    LNode *next;
};
/*int *p//指针类型是int**/
typedef LNode* LinkList;//LNode* 指向节点的指针类型
void input(ElemType *ep)
{
    std::cin >> *ep;
}

void CreateLinkF(LinkList *L,int n,void(*input)(ElemType*))//*input指向函数
{
    LinkList s;
    int i;
    *L =new LNode;
    (*L)->next=nullptr;
    for (i = 0; i < n; i++)
    {
        s=new LNode;
        input(&s->data);
        s->next=(*L)->next;
        (*L)->next=s;
    }
    

}

int main()
{
    LinkList L;
    int n;
    std::cin >> n;
    CreateLinkF(&L,n,input);//L已经是指针，函数传&L传的指针的地址，函数接收指针的指针
}
```
```c++
//尾插法
#include<iostream>
typedef int ElemType;

struct LNode
{
    ElemType data;
    LNode *next;
};

typedef LNode* LinkList;
void input(ElemType *ep)
{
    std::cin >> *ep;
}
void CreateLinkR(LinkList *L, int n,void(*input)(ElemType*))
{
    LinkList p,s;
    int i;
    p=new LNode;
    for ( i = 0; i < n; i++)
    {
        s=new LNode;
        input(&s->data);
        p->next=s,p=s;
    }
    p->next=nullptr;
}
void DestroyList(LinkList *L)//销毁链表
{
    LinkList q,p=*L;
    while (p!=nullptr)
    {
        q=p->next;
        delete p;
        p=q;
    }
    *L=NULL;
}

int main()
{
    LinkList L;
    int n;std::cout>>n;
    CreateLinkR(&L,n,input);
    return 0;
}
```

### 10.2 链表遍历
1. 通过头指针L先访问节点p=L->next；然后令p=p->next指向后继节点如此循环访问链表全部结点
2. 链表遍历算法实现步骤
	* 令指针p指向L开始结点
	* p为0后，表示已到链尾
	* p指向后继结点，即p=p->next，防止重复
```c++
void visit(ElemType *ep)
{
    std::cout << *ep << " ";
}

void ListTraverse(LinkList L,void(*visit)(ElemType*))
{
    LinkList p=L->next;
    while (p!=nullptr)
    {
        visit(&(p->data));
        p->next;
    }
}
```
### 10.3 查找结点
```c++
int compare(ElemType *ep1,ElemType *ep2)
{
    if (*ep1 == *ep2) return 1;
    return 0;
}

int LocateElem(LinkList L,ElemType e,int(*compare)(ElemType*,ElemType*))
{
    int i=0;
    LinkList p=L->next;
    while (p!=nullptr)
    {
        i++;
        if (compare(&(p->data),&e)) return i;
        p=p->next;
    }
    return 0;
}
```

### 10.4 插入结点
```c++
int ListInsert(LinkList *L,int i,ElemType e)
{
    LinkList s,p=*L;
    while (p!=nullptr && i>1)
    {
        p=p->next;
        i--;
    }
    if(p==nullptr|| i<1) return 0;
    s=new LNode;
    s->data =e;
    s->next =p->next,p->next=s;
    return 1;
}
```

### 10.5 删除结点
```c++
int ListDelete(LinkList *L,int i,ElemType *ep)
{
    LinkList p=nullptr,q=*L;
    while (q!=nullptr && i>=1)
    {
        p=q;
        q=q->next;
        i--;
    }
    if (p==nullptr||q==nullptr) return 0;
    p->next=q->next;
    if(ep!=nullptr) *ep=q->data;
    delete q;
    return 1;
}
```

## 十一 预处理命令
### 11.1 不带参数宏定义
### 11.2 带参数的宏定义
```c++
#include <iostream>
#define PI 3.14.5926//不带参数宏
#define mix(a,b) (((a)>(b))? (a):(b))//带参数宏
int main()
{
    int a=8,b=2;
    std::cout << mix(a,b);
    return 0;
}
```
### 11.3 #和##预处理运算
```c++
#include<iostream>
#define PRI_MSG1(x) printf(#x);
#define PRI_MSG2(x) printf(x);
#define PRI_MSG3(x) A##x=x;
PRI_MSG3(1);//替换为A1=1
```
### 11.4 文件包含
```c++
#include <xxxx>
#include "xx.h"
```
### 11.5 条件编译
```c++
//#ifdef条件编译
#ifndef TEST
	。。。
#endif
//第二种
#ifdef TEXT
	...
#else
	...
#endif
```
```c++
//if条件
#if

#else

#endif
//second
#if

#elseif

#else

#endif
```

## 十二 类
### 12.1定义类及成员的访问
```c++
#include<iostream>

class Data
{//类定义：一般放在程序开头或者头文件中
    void set(int d);//h函数原型
    int get()
    {
        return data;
    }
    int data;
};

void Data::set(int d)
{
    data=d;
}
```
```c++
class Data
{
    int a,b;
//顺序通常是：public,protected,private
public://类成员和类用户都能访问，公用
    void ste(int i,int j,int k,int l,int m,int n)
    {a=i,b=j,c=k,d=l,e=m,f=n}
protected://与private性质一致，但是能被派生类访问
    int c,d;
private://只有类成员可以访问，隐私
    int e,f;
};
```

### 12.2类的数据成员、类的成员函数、类的声明
```c++
class Data
{
    long color;
    double x,y,z,side;//数据成员
    void set(int a,int b);
    struct Point//结构体定义
    {
        int x,y;
    };
    typedef Point* LPPoINT;//声明
    inline int gety(){ return y;}//内联函数
    inline void setxy(int _x,int _y);
    void display();
};

void Data::set(int a,int b)//外部定义类函数
{
    data=a+b;
}
void Data::setxy(int _x,int _y)
{
    x=_x,y=_y;
}
void Data::display()
{
    //
}
```
```c++
class Point;
class Line{
    Point a;//false，没有定义
    Point *pp,&rp;//类可以定义定义该类的指针或引用
    Line b;//false
    Line *p1,&r1;//类可以指向自身类型的指针或引用数据成员
}
```

### 12.3 构造函数定义
构造函数是为了初始化参数，列表只能放在函数定义中，不能放在函数声明中
函数名 （形参）：初始化列表 {函数体}
```c++
#include<iostream>
class Cuboid
{
public:
    Cuboid(int l,int h,int d);
    int volumn() {return length*height*depth;}
private:
    int lenght,height,depth;
};
//构造函数初始化列表
Cuboid::Cuboid(int l,int h,int d) : lenght(l),height(h),depth(d)
{
    std::cout << "Cuboid: " << "L=" << l<<",H="<<h<<".D="<<d<<'\n';
}


```
### 12.4 构造函数重载
```c++
//注意：有默认参数的可以不给实参，此时与无参数的构造函数产生歧义，重载可能产生问题
#include<iostream>
class Point
{
public:
    Point() {x=y=0;}
    Point(int a,int b) : x(a),y(b) {}
    void display() {std::cout << "x="<<x<<",y=" <<y<<'\n';}
private:
    int x,y;
};

int main()
{
    Point m;
    m.display();
    Point n(1,2);
    n.display();
    return 0;
}
```
### 12.5 默认构造函数和隐式转换
* 构造函数在定义对象后会先调用
```c++
#include<iostream>
#include<string>
class Data
{
public:
    Data(const std::string& str="") : s1(str) { }
    //构造函数的一般形式：类名(const 指定数据类型& obj)
    void SetString(const Data& r)
    {s1=r.s1;}
    void print() {std::cout << s1 << '\n';}
private:
    std::string s1;
};
int main()
{
    Data a,b,c("world");
    std::string i="string";
    a.SetString(c);
    b.SetString(std::string("world"));
    a.print();
    b.print();
    Data d=Data(i);//将string转换Data对象隐式转换
    d.print();
    return 0;
}
```
```c++
//类名(const 指定类型& obj)
//类名(要转换的数据类型)调用
```
### 12.6 复制构造函数与合成构造函数
* 一般没必要用限定符const
```
Point pt1(10,20);
Point pt2=pt2;复制初始化，调用复制构造函数
Point pt3(pt1);直接初始化，调用与实参匹配的构造函数
```
```c++
#include<iostream>
#include <string.h>
class CA
{
public:
    CA(int b,char *cstr)
    {
        a=b;str=new char[b];
        strcpy(str,cstr);
    }
    CA(const CA &C)
    {
        a=C.a;str=new char[a];
        if(str!=0) strcpy(str,C.str);
    }
    void show()
    {
        std::cout << str << '\n';
    }
    ~CA()
    {
        delete str;
    }
private:
    int a;char *str;
};
int main()
{
    CA a(10,"hello");
    CA b=a;
    b.show();
    return 0;
}
```

### 12.7 析构函数
* 一个类只能有一个析构函数
* 析构函数在类有指针复制操作时编写
* 结束整个程序析构函数类会调用
* 先构造的后析构，后构造的先析构
```c++
#include<iostream>
#include<string.h>

class CString
{
public:
    CString(const char *str);
    ~CString();
    void show() {std::cout << p << '\n';}
private:
    char *p;
};

CString::CString(const char *str)
{
    p=new char[strlen(str)+1];
    strcpy(p,str);
    std::cout << "构造:" << str << '\n';
}

CString::~CString()
{
    std::cout<< "析构：" <<p<<'\n';
    delete [] p;
}

int main()
{
    CString s1("C++"),s2="JavaScript";
    s1.show();s2.show();
    return 0;
}
```
### 12.8 对象数组和对象指针
* 成员指针与类的类型和成员类型有关，只应用于类的非静态成员
* 成员函数后面加const就不能改变数据成员的值`char get() const;`
* this指针代表类的对象
* 