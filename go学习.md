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

