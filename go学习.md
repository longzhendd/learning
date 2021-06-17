# goland学习
[toc]

## __语言结构__
go语言组成部分：
+ 包声明
+ 引入包
+ 函数
+ 变量
+ 语句&表达式
+ 注释  

```go
package main
import "fmt"

func main(){
	/*这是一个简单程序*/
	fmt.Println("hello world")
}
```
各组成部分解析：
1. package main定义包名。每个go语言都包名一个名为main的包名
2. 导入fmt包，fmt包实现了格式化I/O
3. func main()是程序执行，一般第一个执行（如果有init()函数则先执行此函数）
4. /\*...\*/是多行注释（块注释）,单行注释可以用//
5. fmt.Println(...)将字符输出到控制台且最后加上换行字符\n
6. 当标识符（包括常量、变量、类型、函数名、结构字段等等）以大写字母开头，则可被外部包调用

```go
//go语言执行
go run test.go //test.go是代码文件
```

## __Go语言基础语法__
### go标记
go程序可以由多个标记组成（关键字，标识符，常量，字符串，符号）
`fmt.Println("hello,world!")`
标记：
1. fmt
2. .
3. Println
4. (
5. "hello,world"
6. )  

### 行分隔符
将多个语句写在同一行，它们则必须使用 ; 人为区分，但在实际开发中我们并不鼓励这种做法
```go
fmt.Println("hello,world")
fmt.Println("test")
```
### 注释
```go
/*learning
多行注释*/
//单行注释
```

### 标识符
+ 定义：命名变量、类型等程序实体
+ 组成：字母+数字+下划线
+ 字符首位不能是数字

### 字符串连接
通过`+`来连接字符串
```go
package main
import "fmt"
func main(){
	fmt.Println("Google"+"Runoob")
}
//实际输出
GoogleRunoob
```

### 关键字
25 个关键字或保留字

<table class="reference">
<tbody><tr>
<td style="width:20%">break</td><td style="width:20%">default</td><td style="width:20%">func</td><td style="width:20%">interface</td><td style="width:20%">select</td></tr>
<tr><td>case</td><td>defer</td><td>go</td><td>map</td><td>struct</td></tr>
<tr><td>chan</td><td>else</td><td>goto</td><td>package</td><td>switch</td></tr>
<tr><td>const</td><td>fallthrough</td><td>if</td><td>range</td><td>type</td></tr>
<tr><td>continue</td><td>for</td><td>import</td><td>return</td><td>var</td></tr>
</tbody></table>
36个预定义标识符
<table class="reference">
  <tbody><tr>
    <td>append</td>
    <td>bool</td>
    <td>byte</td>
    <td>cap</td>
    <td>close</td>
    <td>complex</td>
    <td>complex64</td>
    <td>complex128</td>
    <td>uint16</td>
  </tr>
  <tr>
    <td>copy</td>
    <td>false</td>
    <td>float32</td>
    <td>float64</td>
    <td>imag</td>
    <td>int</td>
    <td>int8</td>
    <td>int16</td>
    <td>uint32</td>
  </tr>
  <tr>
    <td>int32</td>
    <td>int64</td>
    <td>iota</td>
    <td>len</td>
    <td>make</td>
    <td>new</td>
    <td>nil</td>
    <td>panic</td>
    <td>uint64</td>
  </tr>
  <tr>
    <td>print</td>
    <td>println</td>
    <td>real</td>
    <td>recover</td>
    <td>string</td>
    <td>true</td>
    <td>uint</td>
    <td>uint8</td>
    <td>uintptr</td>
  </tr>
</tbody></table>

### 空格
* 变量声明用空格隔开`var age int;`
* 变量与运算符间加上空格，更美观`a = b +c;`

### 格式化字符串
```go
package main
import "fmt"

func main(){
	//%d代表整数，%s代表字符串
	var stockcode=123
	var enddate="2020-12-31"
	var url="Code=%d&endDate=%s"
	var target_url=fmt.Sprintf(url,stockcode,enddate)
	fmt.Println(target_url)
}
//输出结果
Code=123&endDate=2020-12-31
```

## **Go 数据类型**
+ 布尔类型
```go
//true false
var b bool=true
```
+ 数字类型
```go
//整数类型
uint8/uint16/uint32/uint64
int8/int16/int32/int64
//浮点型
float32/float64
//复数
complex64/complex128
//其他数字类型
byte(类似uint8)/rune(类似 int32)/uint(32 或 64 位)/int(与 uint 一样大小)/uintptr(无符号整型，用于存放一个指针)
```
+ 字符串类型
+ 派生类型
	1. 指针类型（pointer）
	2. 数组类型
	3. 结构化类型
	4. channel类型
	5. 函数类型
	6. 切片类型
	7. 接口类型
	8. Map类型

## **go 语言变量**
### 变量声明
* 指定变量类型
* 自行判断变量类型
* 省略var，使用`:=`左侧没有声明新的变量，产生编译错误
	[!] `:=`用法只能用在函数中
### 多变量声明
```go
package main
import "fmt"

	
var j,k int
var (
	x int 
	y bool
)
var g,h int =1,2
var m,n =123,"hello"
func main(){
	var a string = "robot"
	fmt.Println(a)
	
	var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%d %v %v %q\n",i,f,b,s)
	//fmt.Println(i,f,b,s)
	//fmt.Print(i,f,b,s)
	
	var d=true
	fmt.Println(d)
	
	intvar :=10	//只能出现在函数体
	fmt.Println(intvar)
	fmt.Println(j,k,x,y,g,h,m,n)
}
```

### 注意事项

* 变量交换，要求两变量类型相同。`a,b=b,a`
* 空白标识符`_`用于被抛弃 如`_,b=5,7中5被抛弃`
* `_`只写变量不读
* 空白标识符在函数返回值是使用
```go
package main
import "fmt"

func main(){
	_,numb,strs :=numbers()
	fmt.Println(numb,strs)
}

func numbers()(int,int,string){
	a,b,c:=1,2,"str"
	return a,b,c
}
//结果
2 str //抛弃了a=1
```

## **go语言常量**
`const identifier [type] = value`
* 显式类型定义：`const b string="abc"`
* 隐式类型定义：`const b ="abc"`
* 多类型声明：`const name1,name2,name3 =value1,value2,value3`
```
package main

import "fmt"
const (
    Unknown = 0
    Female = 1
    Male = 2
)

func main() {
   const LENGTH int = 10
   const WIDTH int = 5  
   var area int
   const a, b, c = 1, false, "str" //多重赋值

   area = LENGTH * WIDTH
   fmt.Printf("面积为 : %d", area)
   println()
   println(a, b, c)  
   println(Unknown,Female,Male)
}
```
### iota
特殊常量
用法
```go
package main

import "fmt"
const (
    i=1<<iota
    j=3<<iota
    k
    l
)

func main() {
    fmt.Println("i=",i)//1
    fmt.Println("j=",j)//011左移1位110，换算为10进制：6
    fmt.Println("k=",k)//011左移2位1100，换算为10进制：12
    fmt.Println("l=",l)//011左移3位11000，换算为10进制：24
}
//结果
i= 1
j= 6
k= 12
l= 24
```
### 运算符
* 算术运算符
```
package main
import "fmt"

func main(){
	var a,b int =21,10
	var c int
	c=a-b
	fmt.Printf("第一行c值%d,over\n",c)
	c=a+b
	fmt.Printf("第二行c值%d,over\n",c)
	c=a*b
	fmt.Printf("第三行c值%d,over\n",c)
	c=a/b
	fmt.Printf("第四行c值%d,over\n",c)
	c=a%b
	fmt.Printf("第五行c值%d,over\n",c)
}
```

* 关系运算符
```
package main
import "fmt"

func main(){
	var a,b int =21,10
	if(a==b){
		fmt.Printf("a等于b\n")
	}else{
		fmt.Printf("a不等于b\n")
	}
	if(a>b){
		fmt.Printf("a大于b\n")
	}else{
		fmt.Printf("a不大于b\n")
	}
}
```
* 逻辑运算符
`&&`,`||`,`!`:与，或，非
```
package main
import "fmt"

func main(){
	var a,b bool =true,false
	if(a&&b){
		fmt.Printf("true\n")
	}
	if(a||b){
		fmt.Printf("true\n")
	}
   if ( !(a && b) ) {
      fmt.Printf("第四行 - 条件为 true\n" )
   }
}
```
* 位运算符
`&` `|` `^` `>>` `<<` 与、或、异或、右移、左移
```
package main

import "fmt"

func main(){
	var a uint =60	/*60=0011 1100*/
	var b uint =13	/*13=0000 1101*/
	var c uint =0
	
	c=a&b
	fmt.Printf("第一行%d\n",c)
	
	c=a|b
	fmt.Printf("第二行%d\n",c)
	
	c=a^b
	fmt.Printf("第三行%d\n",c)
	
	c=a<<2
	fmt.Printf("第四行%d\n",c)
	
	c=a>>2
	fmt.Printf("第五行%d\n",c)
}
```
* 赋值运算符
、、、
package main

import "fmt"

func main() {
   var a int = 21
   var c int

   c =  a
   fmt.Printf("第 1 行 - =  运算符实例，c 值为 = %d\n", c )

   c +=  a
   fmt.Printf("第 2 行 - += 运算符实例，c 值为 = %d\n", c )

   c -=  a
   fmt.Printf("第 3 行 - -= 运算符实例，c 值为 = %d\n", c )

   c *=  a
   fmt.Printf("第 4 行 - *= 运算符实例，c 值为 = %d\n", c )

   c /=  a
   fmt.Printf("第 5 行 - /= 运算符实例，c 值为 = %d\n", c )

   c  = 200;

   c <<=  2
   fmt.Printf("第 6行  - <<= 运算符实例，c 值为 = %d\n", c )

   c >>=  2
   fmt.Printf("第 7 行 - >>= 运算符实例，c 值为 = %d\n", c )

   c &=  2
   fmt.Printf("第 8 行 - &= 运算符实例，c 值为 = %d\n", c )

   c ^=  2
   fmt.Printf("第 9 行 - ^= 运算符实例，c 值为 = %d\n", c )

   c |=  2
   fmt.Printf("第 10 行 - |= 运算符实例，c 值为 = %d\n", c )

}
、、、
* 其他

## 条件语句
`if-else`语句
```go
package main
import "fmt"

func main(){
	var a int=30
	if a<20{
		fmt.Printf("a小于20\n")
	}else{
		fmt.Printf("a大于20\n")
		}
	fmt.Printf("a的值为%d\n",a)
}
```
`switch`语句
```go
package main

import "fmt"

func main(){
	var grade string="B"
	var marks int =90
	
	switch marks{
		case 90: grade="A"
		case 80: grade="B"
		case 50,60,70: grade="C"
		default: grade="D"
	}
	
	switch{
		case grade =="A":
			fmt.Printf("优秀\n")
		case grade =="B":
			fmt.Printf("良好\n")
		case grade=="D":
			fmt.Printf("及格\n")
		case grade =="F":
			fmt.Printf("不及格\n")
		default:
		fmt.Printf("差\n");
	}
	fmt.Printf("你的等级是%s\n",grade)
}
```
`type-switch`
```go
package main

import "fmt"

func main(){
	var x interface{}
	
	switch i :=x.(type){
		case nil:
			fmt.Printf("x类型%T",i)
		case int:
			fmt.Printf("x是int类型")
		case float64:
			fmt.Printf("x是float类型")
		case func(int) float64:
			fmt.Printf("x是func(int)型")
		case bool,string:
			fmt.Printf("x是bool类型")
		default:
			fmt.Printf("未知型")
	}
}
```
`fallthrough`
1. 
```go
package main

import "fmt"

func main() {

    switch {
    case false:
            fmt.Println("1、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("2、case 条件语句为 true")
            fallthrough
    case false:
            fmt.Println("3、case 条件语句为 false")
            fallthrough
    case true:
            fmt.Println("4、case 条件语句为 true")
    case false:
            fmt.Println("5、case 条件语句为 false")
            fallthrough
    default:
            fmt.Println("6、默认 case")
    }
}
```
` break`
```
//可以终止语句
switch{
    case 1:
    ...
    if(...){
        break
    }

    fallthrough // 此时switch(1)会执行case1和case2，但是如果满足if条件，则只执行case1

    case 2:
    ...
    case 3:
}

```
## 循环语句

## 函数
## 变量作用域
## 数组
## 指针
## 结构体
## 切片
## 范围