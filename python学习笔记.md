# python学习

## python标志符

- 下划线开头的类`_foo`，不能直接访问，需要通过类提供的接口，不能用`from xxx import *`
- python标识符，由字母、数字、下划线组成，数字不能开头
- 双下划线开头`__foo`代表私有成员，代表特殊方法专用的标识
- python 可以同一行线上多条语句，方法是用`;`分开，如：

```python
>>> print ('hello');print ('runoob');
hello
runoob
```

## python保留字符

| and      |  exec   |    not |
| :------- | :-----: | -----: |
| assert   | finally |     or |
| break    |   for   |   pass |
| class    |  from   |  print |
| continue | global  |  raise |
| def      |   if    | return |
| del      | import  |    try |
| elif     |   in    |  while |
| else     |   is    |   with |
| except   | lambda  |  yield |

python命令行参数
-------

python 提供了**getopt**模块来获取命令行参数

```python
python test.py arg1 arg2 arg3
```

也可以使用**sys**的**sys.argv**来获取命令行参数  

* sys.argv 是命令行参数列表
* len(sys.argv)是命令行参数个数  

**注：** sys.argv[0]表示脚本名
<font size=5> 实例 </font>
test.py文件代码如下：

```python
#!/user/bin/python
# _*_codind；UTF-8 _*_

import sys
print('参数个数为：',len(sys.argv),'个参数')
print('参数列表：',str(sys.argv))
```

执行以上代码，输出结果为：

```python
C:\Users\v_zhenlong>python E:\test3.py arg1 arg2 arg3
参数个数为： 4 个参数
参数列表： ['E:\\test3.py', 'arg1', 'arg2', 'arg3']
```

---

### getopt模块

getopt模块是专门处理命令行参数的模块，用于获取命令行选项和参数，也就是sys.argv。命令行选项使得程序的参数更加灵活。支持短选项`(-)`和长选项`(--)`。
该模块提供了两个方法以及一个异常处理来解析命令行参数。

#### getopt.getop 方法

getopt.getopt方法用于解析命令行参数列表，语法格式如下：

```python
getopt.getopt(args,option[,long_options])
```

方法参数说明：

+ **args**: 要解析的命令行参数列表。
+ **options**：以字符串的格式定义，**long_options**后的等号`=`表示该选项必须有附加的参数，不带冒号表示该选项不附加参数。
+ 该方法返回值由两个元素组成: 第一个是 **(option, value) **元组的列表。 第二个是参数列表，包含那些没有 - 或 -- 的参数。

#### Exception getopt.GetoptError

在没有找到参数列表，或选项需要的参数为空时会触发该异常。
异常的参数是一个字符串，表示错误的原因。属性**msg**和**opt**为相关的错误信息。

<font size=5> 实例</font>
假定我们创建这样一个脚本，可以通过命令行向脚本传递两个文件名，同时我们通过另外一个选项查看脚本的使用。脚本使用方法如下：

```python
usage:test.py -i <inputfile> -o <outputfile>
```

test.py文件代码如下所示：

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-

import sys, getopt

def main(argv):
   inputfile = ''
   outputfile = ''
   try:
      opts, args = getopt.getopt(argv,"hi:o:",["ifile=","ofile="])
   except getopt.GetoptError:
      print('test.py -i <inputfile> -o <outputfile>')
      sys.exit(2)
   for opt, arg in opts:
      if opt == '-h':
         print('test.py -i <inputfile> -o <outputfile>')
         sys.exit()
      elif opt in ("-i", "--ifile"):
         inputfile = arg
      elif opt in ("-o", "--ofile"):
         outputfile = arg
   print('输入的文件为：', inputfile)
   print('输出的文件为：', outputfile)

if __name__ == "__main__":
   main(sys.argv[1:])
```

执行以上代码，输出结果为：

```python
$ python test.py -h
usage: test.py -i <inputfile> -o <outputfile>

$ python test.py -i inputfile -o outputfile
输入的文件为： inputfile
输出的文件为： outputfile
```

#### getopt总结

`opts, args = getopt.getopt(sys.argv[1:], "ho:", ["help", "output="])`

+ `sys.argv[1:]`过滤点第一个参数，执行脚本的字符
+ 短格式分析串`ho:`。当一个选项标识开关，后面不带参数直接填入选项字符，当字符后带参数需要加`：`号。所以`ho:`就表示`h`是一个开关选项；`o:`表示后面还要参数
+ 长格式分析串列表`["help","output="]`。长格式串带`=`表示开关字符，不带`=`为参数字符.`"output="`表示后面应该还要带一个参数
+ 调用getopt返回一个两元组列表：opts和args。opts 为分析出的格式信息。args 为不属于格式信息的剩余的命令行参数。opts 是一个两元组的列表。每个元素为：( 选项串, 附加参数) 。如果没有附加参数则为空串'' 。
+ 一个命令行例子为： 
  `-h -o file --help --output=out file1 file2`
  在分析完成后，opts 应该是： 
  `[('-h', ''), ('-o', 'file'), ('--help', ''), ('--output', 'out')]`
  而args 则为： 
  `['file1', 'file2']`

```python
#代码文本内容test.py
import getopt
import sys

opts,args=getopt.getopt(sys.argv[1:],'hf:v',['help','filename=','version'])
print((opts,args))
for opt_name,opt_value in opts:
    if opt_name in ('-h','--help'):
        print("[*]Help info")
    if opt_name in ('-v','--version'):
        print("[*]Version is 0.01")
    if opt_name in ('-f','--filename'):
        fileName=opt_value
        print("[*]Filename is ",fileName)
        
exit()
```

命令行执行

```python
C:\Users\v_zhenlong>python E:\test.py --fi=test.txt
([('--filename', 'test.txt')], [])
[*]Filename is  test.txt

C:\Users\v_zhenlong>python E:\test.py -hv
([('-h', ''), ('-v', '')], [])
[*]Help info

C:\Users\v_zhenlong>python E:\test.py -hv
([('-h', ''), ('-v', '')], [])
[*]Help info

C:\Users\v_zhenlong>python E:\test.py -hv
([('-h', ''), ('-v', '')], [])
[*]Help info

C:\Users\v_zhenlong>python E:\test.py -v
([('-v', '')], [])

C:\Users\v_zhenlong>python E:\test.py -hv
([('-h', ''), ('-v', '')], [])
[*]Help info
[*]Version is 0.01
```

python 变量类型
------

### 变量赋值

***

`=`来赋值

```python
a=100	#整型
b=1000.0	#浮点型
c="honey"	#字符串
```

### 多变量赋值

***

```python
a=b=c=1
a,b,c=1,2,"john"
```

### 数据类型

***

1. numbers(数字)
2. string(字符串)
3. List(列表)
4. tuple(元组)
5. dictionary(字典)  

#### 数字

***

+ 创建
  `var=1`
+ 删除
  `del var`
+ 数字类型
  &emsp; 1. int（有符号整型）
  &emsp; 2. long（长整型）
  &emsp; 3. float（浮点数）
  &emsp; 4. complex(复数)

#### 字符串

***

字符串由数字、字母、下划线组成
`s="a1a2...an"`

+ 取值

1. 从左到右，0开始
2. 从右到左，-1开始

| R    | O    | U    | N    | D    |
| ---- | ---- | ---- | ---- | ---- |
| 0    | 1    | 2    | 3    | 4    |
| -5   | -4   | -3   | -2   | -1   |

+ 子字符串

```python
s='abcdefg'
s[1:5]
"bcde"
```

+ 加法
  ```'abc'+'def'='abcdef'```
+ 乘法
  ```'abc'*2='abcabc'```

#### 列表

***

![1](https://www.runoob.com/wp-content/uploads/2014/08/list_slicing1_new1.png)
<img src="https://www.runoob.com/wp-content/uploads/2014/08/list_slicing1_new1.png" width="50%">

+ 加号和星号

```python
list = ['runoob', 786, 2.23, 'john', 70.2]
tinylist = [123, 'john']

print(list)  # 输出完整列表
print(list[0])  # 输出列表的第一个元素
print(list[1:3])  # 输出第二个至第三个元素
print(list[2:] ) # 输出从第三个开始至列表末尾的所有元素
print(tinylist * 2)  # 输出列表两次
print(list + tinylist)  # 打印组合的列表

#结果
['runoob', 786, 2.23, 'john', 70.2]
runoob
[786, 2.23]
[2.23, 'john', 70.2]
[123, 'john', 123, 'john']
['runoob', 786, 2.23, 'john', 70.2, 123, 'john']
```


#### 元组

***

元组不能二次赋值，相当于只读列表

```python
tuple = ( 'runoob', 786 , 2.23, 'john', 70.2 )
tuple[2]=1000	#非法应用
```

#### 字典

***

列表是有序的对象集合，字典是无序的对象集合；字典是通过键来存取而非偏移

```python
dict={}
dict['one']="This is one"
dict[2]="This is two"
tinydict={'name':'ruound','code':'325','dept':'sales'}

print(dict['one'])
print(dict[2])
print(tinydict)
print(tinydict.keys())
print(tinydict.values())

#结果
This is one
This is two
{'name': 'ruound', 'code': '325', 'dept': 'sales'}
dict_keys(['name', 'code', 'dept'])
dict_values(['ruound', '325', 'sales'])
```

#### 数据类型转换

***

```python
print(int('1000',2))
print(float(20))
print(complex(1,2))
print((str(213)))   

a=repr(['sdfds',12,[78,'dfd','er']])
print(a,type(a))

b=eval('12+30')
print(b,type(b))

print(tuple('dfdsfs'))

print(list('sfdsadgf'))

print(set('abcde'))

print(dict([(1,'one'),(2,'two'),(3,'three')]))
print(dict(a='a',b='b',c='c'))
print(dict(zip(['one','two','three'],[1,2,3])))

print(frozenset(range(10))) #参数是可迭代对象列表、字典、元组等

print(chr(12300))

print(ord('^'))

print(hex(16))

print(oct(16))

#结果
8
20.0
(1+2j)
213
['sdfds', 12, [78, 'dfd', 'er']] <class 'str'>
42 <class 'int'>
('d', 'f', 'd', 's', 'f', 's')
['s', 'f', 'd', 's', 'a', 'd', 'g', 'f']
{'c', 'e', 'a', 'b', 'd'}
{1: 'one', 2: 'two', 3: 'three'}
{'a': 'a', 'b': 'b', 'c': 'c'}
{'one': 1, 'two': 2, 'three': 3}
frozenset({0, 1, 2, 3, 4, 5, 6, 7, 8, 9})
「
94
0x10
0o20
```

## python运算符

### 算术运算符

***

```python
a=21
b=10
c=0

c=a+b
print('1->',c)

c=a-b
print('2->',c)

c=a*b
print('3->',c)

c=a/b
print('4->',c)

c=a%b
print('5->',c)

a,b=2,3
c=a**b
print('6->',c)

a,b=10,4
c=a//b
print('7->',c)

#结果
1-> 31
2-> 11
3-> 210
4-> 2.1
5-> 1
6-> 8
7-> 2
```

### 比较运算符

***

`==`,`>`,`<`,`>=`,`<=`,`!=`

```python
a,b=10,20
print(a==b)
print(a>=b)
print(a<=b)
print(a!=b)
print(a>b)
print(a<b)
#结果
False
False
True
True
False
True
```

### 赋值运算符

***

`=`,`+=`,`-=`,`*=`,`/=`,`%=`,`**=`,`//=`

| 运算符 |       描述       |                 实例                  |
| ------ | :--------------: | :-----------------------------------: |
| =      | 简单的赋值运算符 | c = a + b 将 a + b 的运算结果赋值为 c |
| +=     |  加法赋值运算符  |        c += a 等效于 c = c + a        |
| -=     |  减法赋值运算符  |        c -= a 等效于 c = c - a        |
| \*=    |  乘法赋值运算符  |       c \*= a 等效于 c = c \* a       |
| /=     |  除法赋值运算符  |        c /= a 等效于 c = c / a        |
| %=     |  取模赋值运算符  |        c %= a 等效于 c = c % a        |
| \*\*=  |   幂赋值运算符   |     c \*\*= a 等效于 c = c \*\* a     |
| //=    | 取整除赋值运算符 |       c //= a 等效于 c = c // a       |

### 逻辑运算符

***

`and`,`or`,`not`

<table class="reference">
<tbody><tr>
<th>运算符</th><th>逻辑表达式</th><th>描述</th><th>实例</th>
</tr>
<tr>
<td>and</td><td>x and y</td><td> 布尔"与" - 如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值。	</td><td> (a and b) 返回 20。</td>
</tr>
<tr>
<td>or</td><td>x or y</td><td>布尔"或"	- 如果 x 是非 0，它返回 x 的计算值，否则它返回 y 的计算值。</td><td> (a or b) 返回 10。</td>
</tr>
<tr><td>not</td><td>not x</td><td>布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。</td><td> not(a and b) 返回 False </td>
</tr>
</tbody></table>

### 位运算符

***

```python
a=60,b=13a = 0011 1100b = 0000 1101-----------------a&b = 0000 1100a|b = 0011 1101a^b = 0011 0001~a  = 1100 0011
```

<table class="reference">
<tbody><tr>
<th>运算符</th><th>描述</th><th>实例</th>
</tr>
<tr>
<td>&amp;</td><td>按位与运算符：参与运算的两个值,如果两个相应位都为1,则该位的结果为1,否则为0</td><td> (a &amp; b) 输出结果 12 ，二进制解释： 0000 1100</td>
</tr>
<tr>
<td>|</td><td> 按位或运算符：只要对应的二个二进位有一个为1时，结果位就为1。</td><td> (a | b) 输出结果 61 ，二进制解释： 0011 1101</td>
</tr>
<tr>
<td>^</td><td>按位异或运算符：当两对应的二进位相异时，结果为1 </td><td> (a ^ b) 输出结果 49 ，二进制解释： 0011 0001</td>
</tr>
<tr>
<td>~</td><td> 按位取反运算符：对数据的每个二进制位取反,即把1变为0,把0变为1 。<span class="marked">~x</span> 类似于 <span class="marked">-x-1</span></td><td> (~a ) 输出结果 -61 ，二进制解释： 1100 0011，在一个有符号二进制数的补码形式。</td>
</tr>
<tr>
<td>&lt;&lt;</td><td>左移动运算符：运算数的各二进位全部左移若干位，由 <span class="marked">&lt;&lt;</span> 右边的数字指定了移动的位数，高位丢弃，低位补0。</td><td> a &lt;&lt; 2 输出结果 240 ，二进制解释： 1111 0000</td>
</tr>
<tr>
<td>&gt;&gt;</td><td>右移动运算符：把"&gt;&gt;"左边的运算数的各二进位全部右移若干位，<span class="marked">&gt;&gt;</span> 右边的数字指定了移动的位数 </td><td> a &gt;&gt; 2 输出结果 15 ，二进制解释： 0000 1111</td>
</tr>
</tbody></table>

### 成员运算符

***

<table class="reference">
<tbody><tr>
<th>运算符</th><th>逻辑表达式</th><th align='center'>描述</th><th>实例</th>
</tr>
<tr>
<td>and</td><td>x and y</td><td> 布尔"与" - 如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值。	</td><td> (a and b) 返回 20。</td>
</tr>
<tr>
<td>or</td><td>x or y</td><td>布尔"或"	- 如果 x 是非 0，它返回 x 的计算值，否则它返回 y 的计算值。</td><td> (a or b) 返回 10。</td>
</tr>
<tr><td>not</td><td>not x</td><td>布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。</td><td> not(a and b) 返回 False </td>
</tr>
</tbody></table>


```python
a = 10
list = [1, 2, 3, 4, 5 ]

print(a in list)
print(a not in list)
```

### 身份运算符

***

```python
a = 10
b=10

print(a is b)
print(a is not b)
```

<table class="reference">
<tbody><tr>
<th width="10%">运算符</th><th>描述</th><th>实例</th>
</tr>
<tr>
<td>is</td><td>
is 是判断两个标识符是不是引用自一个对象</td><td> <strong>x is y</strong>, 类似 <strong>id(x) == id(y)</strong> , 如果引用的是同一个对象则返回 True，否则返回 False</td>
</tr>
<tr>
<td>is not</td><td>is not 是判断两个标识符是不是引用自不同对象</td><td><strong> x is not y</strong> ， 类似 <strong>id(a) != id(b)</strong>。如果引用的不是同一个对象则返回结果 True，否则返回 False。 </td>
</tr>
</tbody></table>

### 运算符优先级

***

<table class="reference">
<tbody><tr><th>运算符</th><th>描述</th></tr>
<tr>
<td>**</td>
<td>指数 (最高优先级)</td>
</tr><tr>
<td>~ + -</td>
<td>按位翻转, 一元加号和减号 (最后两个的方法名为 +@ 和 -@)</td>
</tr><tr>
<td>* / % //</td>
<td>乘，除，取模和取整除</td>
</tr><tr>
<td>+ -</td>
<td>加法减法</td>
</tr><tr>
<td>&gt;&gt; &lt;&lt;</td>
<td>右移，左移运算符</td>
</tr><tr>
<td>&amp;</td>
<td>位 'AND'</td>
</tr><tr>
<td>^ |</td>
<td>位运算符</td>
</tr><tr>
<td>&lt;= &lt; &gt; &gt;=</td>
<td>比较运算符</td>
</tr><tr>
<td>&lt;&gt; == !=</td>
<td>等于运算符</td>
</tr>
<tr>
<td>= %= /= //= -= += *= **=</td>
<td>赋值运算符</td>
</tr>
<tr>
<td>is is not</td>
<td>身份运算符</td>
</tr>
<tr>
<td>in not in</td>
<td>成员运算符</td>
</tr><tr>
<td>not and or</td>
<td>逻辑运算符</td>
</tr>
</tbody></table>



## python字符串

### 转义字符

<table class="reference">
<thead>
<tr>
<th>转义字符</th><th>描述</th>
</tr>
</thead>
<tbody>
<tr>
<td>\(在行尾时)</td>
<td>续行符</td>
</tr>
<tr>
<td>\\</td>
<td>反斜杠符号</td>
</tr>
<tr>
<td>\'</td>
<td>单引号</td>
</tr>
<tr>
<td>\"</td>
<td>双引号</td>
</tr>
<tr>
<td>\a</td>
<td>响铃</td>
</tr>
<tr>
<td>\b</td>
<td>退格(Backspace)</td>
</tr>
<tr>
<td>\e</td>
<td>转义</td>
</tr>
<tr>
<td>\000</td>
<td>空</td>
</tr>
<tr>
<td>\n</td>
<td>换行</td>
</tr>
<tr>
<td>\v</td>
<td>纵向制表符</td>
</tr>
<tr>
<td>\t</td>
<td>横向制表符</td>
</tr>
<tr>
<td>\r</td>
<td>回车</td>
</tr>
<tr>
<td>\f</td>
<td>换页</td>
</tr>
<tr>
<td>\oyy</td>
<td>八进制数，y 代表 0~7 的字符，例如：\012 代表换行。</td>
</tr>
<tr>
<td>\xyy</td>
<td>十六进制数，以 \x 开头，yy代表的字符，例如：\x0a代表换行</td>
</tr>
<tr>
<td>\other</td>
<td>其它的字符以普通格式输出</td>
</tr>
</tbody>
</table>


### 字符串运算符

<table class="reference">
<tbody><tr>
<th width="10%">操作符</th><th>描述</th><th width="20%">实例</th>
</tr>
<tr>
<td>+</td><td>字符串连接</td><td> a + b 输出结果： HelloPython</td>
</tr>
<tr>
<td>*</td><td>重复输出字符串</td><td> a*2 输出结果：HelloHello</td>
</tr>
<tr>
<td>[]</td><td>通过索引获取字符串中字符</td><td> a[1] 输出结果 <b>e</b></td>
</tr>
<tr>
<td>[ : ]</td><td>截取字符串中的一部分，遵循<strong>左闭右开</strong>原则，str[0:2] 是不包含第 3 个字符的。</td><td> a[1:4] 输出结果 <b>ell</b></td>
</tr>
<tr>
<td>in</td><td>成员运算符 - 如果字符串中包含给定的字符返回 True </td><td> <b>'H' in a</b> 输出结果 True</td>
</tr>
<tr>
<td>not in </td><td>成员运算符 - 如果字符串中不包含给定的字符返回 True </td><td> <b>'M' not in a</b> 输出结果 True</td>
</tr>
<tr>
<td>r/R</td><td>原始字符串 - 原始字符串：所有的字符串都是直接按照字面的意思来使用，没有转义特殊或不能打印的字符。原始字符串除在字符串的第一个引号前加上字母 <span class="marked">r</span>（可以大小写）以外，与普通字符串有着几乎完全相同的语法。</td><td><pre>
print( r'\n' )
print( R'\n' )
</pre></td>
</tr>
<tr>
<td>%</td><td>格式字符串</td><td>请看下一节内容。</td>
</tr>
</tbody></table>


### 字符串格式化

<table class="reference">
<tbody<tr><th>
&nbsp;&nbsp;&nbsp; 符&nbsp;&nbsp; 号</th>
<th>描述</th></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %c</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化字符及其ASCII码</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %s</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化字符串</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %d</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化整数</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %u</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化无符号整型</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %o</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化无符号八进制数</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %x</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化无符号十六进制数</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %X</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化无符号十六进制数（大写）</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %f</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;格式化浮点数字，可指定小数点后的精度</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %e</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;用科学计数法格式化浮点数</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %E</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;作用同%e，用科学计数法格式化浮点数</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %g</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;%f和%e的简写</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %G</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;%F 和 %E 的简写</font></td></tr><tr><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; %p</font></td><td><font face="宋体" size="2" style="line-height: 23px; ">&nbsp;用十六进制数格式化变量的地址</font></td></tr></tbody></table>
<p>格式化操作符辅助指令:</p>
<table class="reference">
<tbody><tr>
<th>符号</th><th>功能</th>
</tr>
<tr><td>*</td><td>定义宽度或者小数点精度 </td></tr>
<tr><td>-</td><td>用做左对齐 </td></tr>
<tr><td>+</td><td>在正数前面显示加号( + ) </td></tr>
<tr><td>&lt;sp&gt;</td><td>在正数前面显示空格 </td></tr>
<tr><td>#</td><td> 在八进制数前面显示零('0')，在十六进制前面显示'0x'或者'0X'(取决于用的是'x'还是'X')</td></tr>
<tr><td>0</td><td> 显示的数字前面填充'0'而不是默认的空格 </td></tr>
<tr><td>%</td><td> '%%'输出一个单一的'%' </td></tr>
<tr><td>(var)</td><td>映射变量(字典参数) </td></tr>
<tr><td>m.n.</td><td>  m 是显示的最小总宽度,n 是小数点后的位数(如果可用的话)</td></tr>
</tbody></table>


### 三引号

1. 三引号可以将复杂的字符串进行赋值
2. 三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。
3. 三引号的语法是一对连续的单引号或者双引号
4. 多行注释

### Unicode 字符串

```python
>>> u'Hello\u0020World !'u'Hello World !'
```

### f-string

格式化字符串

```python
name='robot'print(f'hello{name}')   #hellorobotprint(f'{1+2}') #3
```

### 内建函数

<table class="reference">
<tbody><tr>
<th style="width:5%">序号</th><th>方法及描述</th></tr>
<tr><td>1</td><td><p><a href="/python3/python3-string-capitalize.html">capitalize()</a><br>将字符串的第一个字符转换为大写</p></td></tr>
<tr><td>2</td><td><p><a href="/python3/python3-string-center.html">center(width, fillchar)</a></p><br>
返回一个指定的宽度 width 居中的字符串，fillchar 为填充的字符，默认为空格。</td>
</tr>
<tr><td>3</td><td><p><a href="/python3/python3-string-count.html">count(str, beg= 0,end=len(string))</a></p><br>返回 str 在 string 里面出现的次数，如果 beg 或者 end 指定则返回指定范围内 str 出现的次数</td></tr>
<tr><td>4</td><td><p><a href="/python3/python3-string-decode.html">bytes.decode(encoding="utf-8", errors="strict")</a></p><br>Python3 中没有 decode 方法，但我们可以使用 bytes 对象的 decode() 方法来解码给定的 bytes 对象，这个 bytes 对象可以由 str.encode() 来编码返回。</td></tr>
<tr><td>5</td><td><p><a href="/python3/python3-string-encode.html">encode(encoding='UTF-8',errors='strict')</a></p><br>以 encoding 指定的编码格式编码字符串，如果出错默认报一个ValueError 的异常，除非 errors 指定的是'ignore'或者'replace'</td></tr>
<tr><td>6</td><td><p><a href="/python3/python3-string-endswith.html">endswith(suffix, beg=0, end=len(string))</a><br>检查字符串是否以 obj 结束，如果beg 或者 end 指定则检查指定的范围内是否以 obj 结束，如果是，返回 True,否则返回 False.</p></td></tr>
<tr><td>7</td><td><p><a href="/python3/python3-string-expandtabs.html">expandtabs(tabsize=8)</a></p><br>把字符串 string 中的 tab 符号转为空格，tab 符号默认的空格数是 8 。</td></tr>
<tr><td>8</td><td><p><a href="/python3/python3-string-find.html">find(str, beg=0, end=len(string))</a></p><br>检测 str 是否包含在字符串中，如果指定范围 beg 和 end ，则检查是否包含在指定范围内，如果包含返回开始的索引值，否则返回-1</td></tr>
<tr><td>9</td><td><p><a href="/python3/python3-string-index.html">index(str, beg=0, end=len(string))</a></p><br>跟find()方法一样，只不过如果str不在字符串中会报一个异常。</td></tr>
<tr><td>10</td><td><p><a href="/python3/python3-string-isalnum.html">isalnum()</a></p><br>如果字符串至少有一个字符并且所有字符都是字母或数字则返
回 True，否则返回 False</td></tr>
<tr><td>11</td><td><p><a href="/python3/python3-string-isalpha.html">isalpha()</a></p><br>如果字符串至少有一个字符并且所有字符都是字母或中文字则返回 True,
否则返回 False</td></tr>
<tr><td>12</td><td><p><a href="/python3/python3-string-isdigit.html">isdigit()</a></p><br>如果字符串只包含数字则返回 True 否则返回 False..</td></tr>
<tr><td>13</td><td><p><a href="/python3/python3-string-islower.html">islower()</a></p><br>如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是小写，则返回 True，否则返回 False</td></tr>
<tr><td>14</td><td><p><a href="/python3/python3-string-isnumeric.html">isnumeric()</a></p><br>如果字符串中只包含数字字符，则返回 True，否则返回 False</td></tr>
<tr><td>15</td><td><p><a href="/python3/python3-string-isspace.html">isspace()</a></p><br>如果字符串中只包含空白，则返回 True，否则返回 False.</td></tr>
<tr><td>16</td><td><p><a href="/python3/python3-string-istitle.html">istitle()</a></p><br>	
如果字符串是标题化的(见 title())则返回 True，否则返回 False</td></tr>
<tr><td>17</td><td><p><a href="/python3/python3-string-isupper.html">isupper()</a></p><br>如果字符串中包含至少一个区分大小写的字符，并且所有这些(区分大小写的)字符都是大写，则返回 True，否则返回 False</td></tr>
<tr><td>18</td><td><p><a href="/python3/python3-string-join.html">join(seq)</a></p><br>以指定字符串作为分隔符，将 seq 中所有的元素(的字符串表示)合并为一个新的字符串</td></tr>
<tr><td>19</td><td><p><a href="/python3/python3-string-len.html">len(string)</a></p><br>返回字符串长度</td></tr>
<tr><td>20</td><td><p><a href="/python3/python3-string-ljust.html">ljust(width[, fillchar])</a></p><br>返回一个原字符串左对齐,并使用 fillchar 填充至长度 width 的新字符串，fillchar 默认为空格。</td></tr>
<tr><td>21</td><td><p><a href="/python3/python3-string-lower.html">lower()</a></p><br>转换字符串中所有大写字符为小写.</td></tr>
<tr><td>22</td><td><p><a href="/python3/python3-string-lstrip.html">lstrip()</a></p><br>截掉字符串左边的空格或指定字符。</td></tr>
<tr><td>23</td><td><p><a href="/python3/python3-string-maketrans.html">maketrans()</a></p><br>创建字符映射的转换表，对于接受两个参数的最简单的调用方式，第一个参数是字符串，表示需要转换的字符，第二个参数也是字符串表示转换的目标。</td></tr>
<tr><td>24</td><td><p><a href="/python3/python3-string-max.html">max(str)</a></p><br>返回字符串 str 中最大的字母。</td></tr>
<tr><td>25</td><td><p><a href="/python3/python3-string-min.html">min(str)</a></p><br>返回字符串 str 中最小的字母。</td></tr>
<tr><td>26</td><td><p><a href="/python3/python3-string-replace.html">replace(old, new [, max])</a></p><br>把 将字符串中的 old 替换成 new,如果 max 指定，则替换不超过 max 次。</td></tr>
<tr><td>27</td><td><p><a href="/python3/python3-string-rfind.html">rfind(str, beg=0,end=len(string))</a></p><br>类似于 find()函数，不过是从右边开始查找.</td></tr>
<tr><td>28</td><td><p><a href="/python3/python3-string-rindex.html">rindex( str, beg=0, end=len(string))</a></p><br>类似于 index()，不过是从右边开始.</td></tr>
<tr><td>29</td><td><p><a href="/python3/python3-string-rjust.html">rjust(width,[, fillchar])</a></p><br>返回一个原字符串右对齐,并使用fillchar(默认空格）填充至长度 width 的新字符串</td></tr>
<tr><td>30</td><td><p><a href="/python3/python3-string-rstrip.html">rstrip()</a></p><br>删除字符串末尾的空格或指定字符。</td></tr>
<tr><td>31</td><td><p><a href="/python3/python3-string-split.html">split(str="", num=string.count(str))</a></p><br>
以 str 为分隔符截取字符串，如果 num 有指定值，则仅截取 num+1 个子字符串</td></tr>
<tr><td>32</td><td><p><a href="/python3/python3-string-splitlines.html">splitlines([keepends])</a></p><br>按照行('\r', '\r\n', \n')分隔，返回一个包含各行作为元素的列表，如果参数 keepends 为 False，不包含换行符，如果为 True，则保留换行符。</td></tr>
<tr><td>33</td><td><p><a href="/python3/python3-string-startswith.html">startswith(substr, beg=0,end=len(string))</a></p><br>检查字符串是否是以指定子字符串 substr 开头，是则返回 True，否则返回 False。如果beg 和 end 指定值，则在指定范围内检查。</td></tr>
<tr><td>34</td><td><p><a href="/python3/python3-string-strip.html">strip([chars])</a></p><br>在字符串上执行 lstrip()和 rstrip()</td></tr>
<tr><td>35</td><td><p><a href="/python3/python3-string-swapcase.html">swapcase()</a></p><br>将字符串中大写转换为小写，小写转换为大写</td></tr>
<tr><td>36</td><td><p><a href="/python3/python3-string-title.html">title()</a></p><br>返回"标题化"的字符串,就是说所有单词都是以大写开始，其余字母均为小写(见 istitle())</td></tr>
<tr><td>37</td><td><p><a href="/python3/python3-string-translate.html">translate(table, deletechars="")</a></p><br>根据 str 给出的表(包含 256 个字符)转换 string 的字符,
要过滤掉的字符放到 deletechars 参数中</td></tr>
<tr><td>38</td><td><p><a href="/python3/python3-string-upper.html">upper()</a></p><br>	
转换字符串中的小写字母为大写</td></tr>
<tr><td>39</td><td><p><a href="/python3/python3-string-zfill.html">zfill (width)</a></p><br>返回长度为 width 的字符串，原字符串右对齐，前面填充0</td></tr>
<tr><td>40</td><td><p><a href="/python3/python3-string-isdecimal.html">isdecimal()</a></p><br>
检查字符串是否只包含十进制字符，如果是返回 true，否则返回 false。</td></tr>
</tbody></table>


## python列表函数及方法

### 函数

<table class="reference">
<tbody><tr>
<th style="width:5%">序号</th><th style="width:95%">函数</th></tr>
<tr><td>1</td><td><a href="python3-att-list-len.html">len(list)</a><br>列表元素个数</td></tr>
<tr><td>2</td><td><a href="python3-att-list-max.html">max(list)</a><br>返回列表元素最大值</td></tr>
<tr><td>3</td><td><a href="python3-att-list-min.html">min(list)</a><br>返回列表元素最小值</td></tr>
<tr><td>4</td><td><a href="python3-att-list-list.html">list(seq)</a><br>将元组转换为列表</td></tr>
</tbody></table>

### 方法

<table class="reference">
<tbody><tr>
<th style="width:5%">序号</th><th style="width:95%">方法</th></tr>
<tr><td>1</td><td><a href="python3-att-list-append.html">list.append(obj)</a><br>在列表末尾添加新的对象</td></tr>
<tr><td>2</td><td><a href="python3-att-list-count.html">list.count(obj)</a><br>统计某个元素在列表中出现的次数</td></tr>
<tr><td>3</td><td><a href="python3-att-list-extend.html">list.extend(seq)</a><br>在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）</td></tr>
<tr><td>4</td><td><a href="python3-att-list-index.html">list.index(obj)</a><br>从列表中找出某个值第一个匹配项的索引位置</td></tr>
<tr><td>5</td><td><a href="python3-att-list-insert.html">list.insert(index, obj)</a><br>将对象插入列表</td></tr>
<tr><td>6</td><td><a href="python3-att-list-pop.html">list.pop([index=-1])</a><br>移除列表中的一个元素（默认最后一个元素），并且返回该元素的值</td></tr>
<tr><td>7</td><td><a href="python3-att-list-remove.html">list.remove(obj)</a><br>移除列表中某个值的第一个匹配项</td></tr>
<tr><td>8</td><td><a href="python3-att-list-reverse.html">list.reverse()</a><br>反向列表中元素</td></tr>
<tr><td>9</td><td><a href="python3-att-list-sort.html">	list.sort( key=None, reverse=False)</a><br>对原列表进行排序</td></tr>
<tr><td>10</td><td><a href="python3-att-list-clear.html">list.clear()</a><br>清空列表</td></tr>
<tr><td>11</td><td><a href="python3-att-list-copy.html">list.copy()</a><br>复制列表</td></tr>
</tbody></table>


## python元组

### 内置函数

<table class="reference">
<tbody><tr>
<th style="width:5%">序号</th><th style="width:25%">方法及描述</th><th style="width:45%">实例</th></tr><tr><td>1</td><td>len(tuple)<br>计算元组元素个数。</td><td><pre>&gt;&gt;&gt; tuple1 = ('Google', 'Runoob', 'Taobao')&gt;&gt;&gt; len(tuple1)3&gt;&gt;&gt; </pre></td></tr><tr><td>2</td><td>max(tuple)<br>返回元组中元素最大值。</td><td><pre>>>> tuple2 = ('5', '4', '8')>>> max(tuple2)'8'>>> </td></tr>
<tr><td>3</td><td>min(tuple)<br>返回元组中元素最小值。</td>
<td>
<pre>
>>> tuple2 = ('5', '4', '8')
>>> min(tuple2)
'4'
>>> 
</td>
</tr>
<tr><td>4</td><td>tuple(iterable)<br>将可迭代系列转换为元组。</td>
<td>
<pre>
>>> list1= ['Google', 'Taobao', 'Runoob', 'Baidu']
>>> tuple1=tuple(list1)
>>> tuple1
('Google', 'Taobao', 'Runoob', 'Baidu')
</td>
</tr>
</tbody></table>

### 元组不可变与列表可变

```python
//元组
>>>tup=('r','u','n','o','f','d')
>>>tup[0]
'r'
>>>tup[0]='g'	#不能修改
Traceback (most recent call last):
  File "<input>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
>>>id(tup)		#内存地址
236697728
>>>tup=(1,2,3)	#重新赋值为重新创建
>>>id(tup)		#内存地址变了
237324728
```

```python
//列表
>>>list=['e','r','t','y']
>>>list[0]='g'		#可修改
>>>id(list)
237334320
>>>list=[1,2,3]
>>>id(list)		#重新赋值，内存地址也变了
237340312
```

## 字典

### 创建

```python
d = {key1 : value1, key2 : value2, key3 : value3 }
a=dict({1:1,2:2})
b=dict(c=1,d=4)
print(a,b,type(b),type(b))
# {1: 1, 2: 2} {'c': 1, 'd': 4} <class 'dict'> <class 'dict'>
a.clear()
print(a)
del a	#删除字典
print(a)
#	{}
Traceback (most recent call last):
  File "F:/机器学习+深度学习/tensorflow/test3.py", line 22, in <module>
    print(a)
NameError: name 'a' is not defined
```

### 内置函数

<table class="reference">
<tbody><tr><th width="5%">序号</th><th width="25%">函数及描述</th><th>实例</th></tr>
<tr><td>1</td><td>len(dict)<br>计算字典元素个数，即键的总数。</td><td><pre>&gt;&gt;&gt;dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}&gt;&gt;&gt; len(dict)3</pre>
</td>
</tr>
<tr><td>2</td><td>str(dict)<br>输出字典，以可打印的字符串表示。</td>
<td>
<pre>
&gt;&gt;&gt; dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
&gt;&gt;&gt; str(dict)
"{'Name': 'Runoob', 'Class': 'First', 'Age': 7}"
</pre>
</td>
</tr>
<tr><td>3</td><td>type(variable)<br>返回输入的变量类型，如果变量是字典就返回字典类型。</td>
<td>
<pre>&gt;&gt;&gt; dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}&gt;&gt;&gt; type(dict)&lt;class 'dict'&gt;</pre>
</td>
</tr>
</tbody></table>

### 内置方法

<table class="reference">
<tbody><tr>
<th style="width:5%">序号</th><th style="width:95%">方法及描述</th></tr>
<tr><td>1</td><td><a href="python3-att-dictionary-clear.html">radiansdict.clear()</a><br>删除字典内所有元素 </td></tr>
<tr><td>2</td><td><a href="python3-att-dictionary-copy.html">radiansdict.copy()</a><br>返回一个字典的浅复制</td></tr>
<tr><td>3</td><td><a href="python3-att-dictionary-fromkeys.html">radiansdict.fromkeys()</a><br> 创建一个新字典，以序列seq中元素做字典的键，val为字典所有键对应的初始值</td></tr>
<tr><td>4</td><td><a href="python3-att-dictionary-get.html">radiansdict.get(key, default=None)</a><br>返回指定键的值，如果键不在字典中返回 default 设置的默认值</td></tr>
<tr><td>5</td><td><a href="python3-att-dictionary-in.html">key in dict</a><br>如果键在字典dict里返回true，否则返回false</td></tr>
<tr><td>6</td><td><a href="python3-att-dictionary-items.html">radiansdict.items()</a><br>以列表返回一个视图对象</td></tr>
<tr><td>7</td><td><a href="python3-att-dictionary-keys.html">radiansdict.keys()</a><br>返回一个视图对象</td></tr>
<tr><td>8</td><td><a href="python3-att-dictionary-setdefault.html">radiansdict.setdefault(key, default=None)</a><br>   
和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default</td></tr>
<tr><td>9</td><td><a href="python3-att-dictionary-update.html">radiansdict.update(dict2)</a><br>把字典dict2的键/值对更新到dict里</td></tr>
<tr><td>10</td><td><a href="python3-att-dictionary-values.html">radiansdict.values()</a><br>返回一个视图对象</td></tr>
<tr><td>11</td><td><a href="python3-att-dictionary-pop.html">pop(key[,default])</a><br>删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。
否则，返回default值。</td></tr>
<tr><td>12</td><td><a href="python3-att-dictionary-popitem.html"> popitem()</a><br>随机返回并删除字典中的最后一对键和值。</td></tr>
</tbody></table>



## 集合

### 创建

```python
parame={value,value2}# orb=set(value)
```

### 操作

```python
s = set(("Google", "Runoob", "Taobao"))s.add('facebook')   #新增s.update({1,3})s.update([1,4],[5,6])print(s)s.remove(1)     #删除s.discard(4)print(s)x=s.pop()print(s,x)l=len(s)    #长度print(l)s.clear()   #清空print(s)
```

```python
basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']c=set(basket)print(basket)print(c)print('apple' in c)print(1 in c)a= set('abcdabcd')b=set('fcbacba')print(a)print(b)print(a-b)  #在a不在bprint(a|b)  #在a或者b中print(a&b)  #a,b中都有print(a^b)  #a或b中字母，不同时存在
```

### 内置方法

<table class="reference">
<tbody><tr>
<th>方法</th>
<th>描述</th>
</tr>
<tr><td><a href="ref-set-add.html" target="_blank" rel="noopener noreferrer">add()</a></td><td>为集合添加元素</td></tr>
<tr><td><a href="ref-set-clear.html" target="_blank" rel="noopener noreferrer">clear()</a></td><td>移除集合中的所有元素</td></tr>
<tr><td><a href="ref-set-copy.html" target="_blank" rel="noopener noreferrer">copy()</a></td><td>拷贝一个集合</td></tr>
  <tr>
    <td><a href="ref-set-difference.html" target="_blank" rel="noopener noreferrer">difference()</a></td><td>返回多个集合的差集</td>
  </tr>
  <tr>
    <td><a href="ref-set-difference_update.html" target="_blank" rel="noopener noreferrer">difference_update()</a></td><td>移除集合中的元素，该元素在指定的集合也存在。</td>
  </tr>
<tr><td><a href="ref-set-discard.html" target="_blank" rel="noopener noreferrer">discard()</a></td><td>删除集合中指定的元素</td></tr>
  <tr>
    <td><a href="ref-set-intersection.html" target="_blank" rel="noopener noreferrer">intersection()</a></td><td>返回集合的交集</td>
  </tr>
<tr><td><a href="ref-set-intersection_update.html" target="_blank" rel="noopener noreferrer">intersection_update()</a></td><td>
  返回集合的交集。</td></tr>
  <tr>
    <td><a href="ref-set-isdisjoint.html" target="_blank" rel="noopener noreferrer">isdisjoint()</a></td><td>判断两个集合是否包含相同的元素，如果没有返回 True，否则返回 False。</td>
  </tr>
  <tr>
    <td><a href="ref-set-issubset.html" target="_blank" rel="noopener noreferrer">issubset()</a></td><td>判断指定集合是否为该方法参数集合的子集。</td>
  </tr>
<tr><td><a href="ref-set-issuperset.html" target="_blank" rel="noopener noreferrer">issuperset()</a></td><td>判断该方法的参数集合是否为指定集合的子集</td></tr>
<tr><td><a href="ref-set-pop.html" target="_blank" rel="noopener noreferrer">pop()</a></td><td>随机移除元素</td></tr>
<tr><td><a href="ref-set-remove.html" target="_blank" rel="noopener noreferrer">remove()</a></td><td>移除指定元素</td></tr>
  <tr>
    <td><a href="ref-set-symmetric_difference.html" target="_blank" rel="noopener noreferrer">symmetric_difference()</a></td><td>返回两个集合中不重复的元素集合。</td>
  </tr>
<tr><td><a href="ref-set-symmetric_difference_update.html" target="_blank" rel="noopener noreferrer">symmetric_difference_update()</a></td><td>
  移除当前集合中在另外一个指定集合相同的元素，并将另外一个指定集合中不同的元素插入到当前集合中。 </td></tr>
  <tr>
    <td><a href="ref-set-union.html" target="_blank" rel="noopener noreferrer">union()</a></td><td>返回两个集合的并集</td>
  </tr>
<tr><td><a href="ref-set-update.html" target="_blank" rel="noopener noreferrer">update()</a></td><td>给集合添加元素</td></tr>
</tbody></table>


## 迭代器和生成器

### 迭代器

#### for循环

```python
list=[1,2,3,4]
it=iter(list)
print(next(it)) #1
print(next(it)) #2

# 迭代器for循环
list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象
for x in it:
    print (x, end=" ")
print(' ')
```

#### while循环

```python
# 迭代器while循环
import sys  # 引入 sys 模块
list = [1, 2, 3, 4]
it = iter(list)  # 创建迭代器对象
while True:
    try:
        print(next(it))
    except StopIteration:
        sys.exit()
```

#### 创建迭代器

```python
class mynumber():
    def __iter__(self):
        self.a=1
        return self

    def __next__(self):
        x=self.a
        self.a +=1
        return x

myclass = mynumber()
myiter = iter(myclass)

print(next(myiter))
print(next(myiter))
print(next(myiter))
```

#### stopiteration

```python
class MyNumbers:  def __iter__(self):    self.a = 1    return self   def __next__(self):    if self.a <= 20:      x = self.a      self.a += 1      return x    else:      raise StopIteration myclass = MyNumbers()myiter = iter(myclass) for x in myiter:  print(x)
```

### 生成器

```python
import sysdef fibonacci(n): # 生成器函数 - 斐波那契    a, b, counter = 0, 1, 0    while True:        if (counter > n):             return        yield a        a, b = b, a + b        counter += 1f = fibonacci(10) # f 是一个迭代器，由生成器返回生成while True:    try:        print (next(f), end=" ")    except StopIteration:        sys.exit()        # 结果0 1 1 2 3 5 8 13 21 34 55
```

## python函数

### 参数

#### 必需参数

```python
def func(str):
	print(str)
	return 
```

#### 关键字参数

```
def func(str,str1):
    print(str)
    print(str1)
    return 
func(str=1,str1=3)
```

#### 默认参数

```
def func(str=5,str1=10):
    print(str)
    print(str1)
    return
func(str=1,str1=3)
```

#### 不定长参数

```
def func(*args):
    print(*args)
    return
func(1,2,3)
def func(**args):
    print(args) #键值对
    print(*args)    #键
    return
func(a=1,b=2,c=3)
```

### 匿名函数

```
sum=lambda a,b:a+b
print(sum(3,4))
```

### return

```
def func(s):
    return s+5
a=func(5)
print(a)    #10
```

## python模块

### import

```python
import sysfrom sys import exit,stdinfrom sys import *from ..filters import equalizer
```

### 模块属性

```
# 可以判断是被调用还是自己运行if __name__ == '__main__':   print('程序自身在运行')else:   print('我来自另一模块')   # dir()函数可以找到模块内定义的所有名称
```

### 包

```
sound/                          顶层包      __init__.py               初始化 sound 包      formats/                  文件格式转换子包              __init__.py              wavread.py              wavwrite.py              aiffread.py              aiffwrite.py              auread.py              auwrite.py              ...      effects/                  声音效果子包              __init__.py              echo.py              surround.py              reverse.py              ...      filters/                  filters 子包              __init__.py              equalizer.py              vocoder.py              karaoke.py              ...
```

## 输入和输出

### format格式化

```
for x in range(1,10):    print('{0:2d} {1:3d} {2:4d}'.format(x, x*x, x*x*x))
```

### %格式化

```
import mathprint('pi的值为：%5.3f'%math.pi)
```

### 读写文件

`open(file, mode='r')
`
`open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)
`

```
f=open('file.txt','w+',encoding="utf-8")f.write('testing great')f.read(size)	#读取一点数目数据，不填参数读所有f.readline()	#只读一行，空格算一行f.readlines()	#读所有，返回一个列表，每行+\n是一个值f.tell()	#返回光标所在位置f.seek(offset,from_what)seek(x,0)	#起始位置往后移动xseek(x,1)	#当前位置往后移动x字符seek(-x,2)	#从结尾往前移动x字符f.close()	#释放系统资源
```

```
with open('file.txt','w+',encoding="utf-8") as f:	data=f.read()
```

<table class="reference">
<tbody><tr><th style="width:10%">模式</th><th>描述</th></tr>
<tr><td>t</td><td>文本模式 (默认)。</td></tr>
<tr><td>x</td><td>写模式，新建一个文件，如果该文件已存在则会报错。</td></tr>
<tr><td>b</td><td>二进制模式。</td></tr>
<tr><td>+</td><td>打开一个文件进行更新(可读可写)。</td></tr>
<tr><td>U</td><td>通用换行模式（<strong style="color:red;">Python 3 不支持</strong>）。</td></tr>
<tr><td>r</td><td>以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。</td></tr>
<tr><td>rb</td><td>以二进制格式打开一个文件用于只读。文件指针将会放在文件的开头。这是默认模式。一般用于非文本文件如图片等。</td></tr>
<tr><td>r+</td><td>打开一个文件用于读写。文件指针将会放在文件的开头。</td></tr>
<tr><td>rb+</td><td>以二进制格式打开一个文件用于读写。文件指针将会放在文件的开头。一般用于非文本文件如图片等。</td></tr>
<tr><td>w</td><td>打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。</td></tr>
<tr><td>wb</td><td>以二进制格式打开一个文件只用于写入。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。</td></tr>
<tr><td>w+</td><td>打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。</td></tr> 
<tr><td>wb+</td><td>以二进制格式打开一个文件用于读写。如果该文件已存在则打开文件，并从开头开始编辑，即原有内容会被删除。如果该文件不存在，创建新文件。一般用于非文本文件如图片等。</td></tr>
<tr><td>a</td><td>打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。</td></tr> <tr><td>ab</td><td>以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。也就是说，新的内容将会被写入到已有内容之后。如果该文件不存在，创建新文件进行写入。</td></tr> <tr><td>a+</td><td>打开一个文件用于读写。如果该文件已存在，文件指针将会放在文件的结尾。文件打开时会是追加模式。如果该文件不存在，创建新文件用于读写。</td></tr> <tr><td>ab+</td><td>以二进制格式打开一个文件用于追加。如果该文件已存在，文件指针将会放在文件的结尾。如果该文件不存在，创建新文件用于读写。</td></tr></tbody></table>


### json模块

### csv模块

## OS

<table class="reference">
<tbody><tr>
<th style="width:5%">序号</th><th>方法及描述</th></tr>
<tr><td>1</td><td><p><a href="/python3/python3-os-access.html">os.access(path, mode)</a></p><br>检验权限模式  </td></tr>
<tr><td>2</td><td><p><a href="/python3/python3-os-chdir.html">os.chdir(path)</a></p><br>改变当前工作目录</td></tr>
<tr><td>3</td><td><p><a href="/python3/python3-os-chflags.html">os.chflags(path, flags)</a></p><br>设置路径的标记为数字标记。</td></tr>
<tr><td>4</td><td><p><a href="/python3/python3-os-chmod.html">os.chmod(path, mode)</a></p><br>更改权限 </td></tr>
<tr><td>5</td><td><p><a href="/python3/python3-os-chown.html">os.chown(path, uid, gid)</a></p><br>更改文件所有者</td></tr>
<tr><td>6</td><td><p><a href="/python3/python3-os-chroot.html">os.chroot(path)</a></p><br>改变当前进程的根目录  </td></tr>
<tr><td>7</td><td><p><a href="/python3/python3-os-close.html">os.close(fd)</a></p><br>关闭文件描述符 fd</td></tr>
<tr><td>8</td><td><p><a href="/python3/python3-os-closerange.html">os.closerange(fd_low, fd_high)</a></p><br>关闭所有文件描述符，从 fd_low (包含) 到 fd_high (不包含), 错误会忽略</td></tr>
<tr><td>9</td><td><p><a href="/python3/python3-os-dup.html">os.dup(fd)</a></p><br>复制文件描述符 fd</td></tr>
<tr><td>10</td><td><p><a href="/python3/python3-os-dup2.html">os.dup2(fd, fd2)</a></p><br>将一个文件描述符 fd 复制到另一个 fd2</td></tr>
<tr><td>11</td><td><p><a href="/python3/python3-os-fchdir.html">os.fchdir(fd)</a></p><br>通过文件描述符改变当前工作目录</td></tr>
<tr><td>12</td><td><p><a href="/python3/python3-os-fchmod.html">os.fchmod(fd, mode)</a></p><br>改变一个文件的访问权限，该文件由参数fd指定，参数mode是Unix下的文件访问权限。</td></tr>
<tr><td>13</td><td><p><a href="/python3/python3-os-fchown.html">os.fchown(fd, uid, gid)</a></p><br>修改一个文件的所有权，这个函数修改一个文件的用户ID和用户组ID，该文件由文件描述符fd指定。 </td></tr>
<tr><td>14</td><td><p><a href="/python3/python3-os-fdatasync.html">os.fdatasync(fd)</a></p><br>强制将文件写入磁盘，该文件由文件描述符fd指定，但是不强制更新文件的状态信息。</td></tr>
<tr><td>15</td><td><p><a href="/python3/python3-os-fdopen.html">os.fdopen(fd[, mode[, bufsize]])</a></p><br>通过文件描述符 fd 创建一个文件对象，并返回这个文件对象 </td></tr>
<tr><td>16</td><td><p><a href="/python3/python3-os-fpathconf.html">os.fpathconf(fd, name)</a></p><br>返回一个打开的文件的系统配置信息。name为检索的系统配置的值，它也许是一个定义系统值的字符串，这些名字在很多标准中指定（POSIX.1, Unix 95, Unix 98, 和其它）。</td></tr>
<tr><td>17</td><td><p><a href="/python3/python3-os-fstat.html">os.fstat(fd)</a></p><br>返回文件描述符fd的状态，像stat()。 </td></tr>
<tr><td>18</td><td><p><a href="/python3/python3-os-fstatvfs.html">os.fstatvfs(fd)</a></p><br>返回包含文件描述符fd的文件的文件系统的信息，Python 3.3 相等于 statvfs()。</td></tr><tr><td>19</td><td><p><a href="/python3/python3-os-fsync.html">os.fsync(fd)</a></p><br>强制将文件描述符为fd的文件写入硬盘。</td></tr><tr><td>20</td><td><p><a href="/python3/python3-os-ftruncate.html">os.ftruncate(fd, length)</a></p><br>裁剪文件描述符fd对应的文件, 所以它最大不能超过文件大小。</td></tr>
<tr><td>21</td><td><p><a href="/python3/python3-os-getcwd.html">os.getcwd()</a></p><br>返回当前工作目录 </td></tr><tr><td>22</td><td><p><a href="/python3/python3-os-getcwdb.html">os.getcwdb()</a></p><br>返回一个当前工作目录的Unicode对象</td></tr>
<tr><td>23</td><td><p><a href="/python3/python3-os-isatty.html">os.isatty(fd)</a></p><br>如果文件描述符fd是打开的，同时与tty(-like)设备相连，则返回true, 否则False。</td></tr><tr><td>24</td><td><p><a href="/python3/python3-os-lchflags.html">os.lchflags(path, flags)</a></p><br>设置路径的标记为数字标记，类似 chflags()，但是没有软链接</td></tr>
<tr><td>25</td><td><p><a href="/python3/python3-os-lchmod.html">os.lchmod(path, mode)</a></p><br>修改连接文件权限</td></tr><tr><td>26</td><td><p><a href="/python3/python3-os-lchown.html">os.lchown(path, uid, gid)</a></p><br>更改文件所有者，类似 chown，但是不追踪链接。 </td></tr><tr><td>27</td><td><p><a href="/python3/python3-os-link.html">os.link(src, dst)</a></p><br>创建硬链接，名为参数 dst，指向参数 src</td></tr><tr><td>28</td><td><p><a href="/python3/python3-os-listdir.html">os.listdir(path)</a></p><br>返回path指定的文件夹包含的文件或文件夹的名字的列表。 </td></tr><tr><td>29</td><td><p><a href="/python3/python3-os-lseek.html">os.lseek(fd, pos, how)</a></p><br>设置文件描述符 fd当前位置为pos, how方式修改: SEEK_SET 或者 0 设置从文件开始的计算的pos; SEEK_CUR或者 1 则从当前位置计算; os.SEEK_END或者2则从文件尾部开始. 在unix，Windows中有效</td></tr><tr><td>30</td><td><p><a href="/python3/python3-os-lstat.html">os.lstat(path)</a></p><br>像stat(),但是没有软链接 </td></tr><tr><td>31</td><td><p><a href="/python3/python3-os-major.html">os.major(device)</a></p><br>从原始的设备号中提取设备major号码 (使用stat中的st_dev或者st_rdev field)。</td></tr><tr><td>32</td><td><p><a href="/python3/python3-os-makedev.html">os.makedev(major, minor)</a></p><br>以major和minor设备号组成一个原始设备号</td></tr><tr><td>33</td><td><p><a href="/python3/python3-os-makedirs.html">os.makedirs(path[, mode])</a></p><br>递归文件夹创建函数。像mkdir(), 但创建的所有intermediate-level文件夹需要包含子文件夹。</td></tr><tr><td>34</td><td><p><a href="/python3/python3-os-minor.html">os.minor(device)</a></p><br>从原始的设备号中提取设备minor号码 (使用stat中的st_dev或者st_rdev field )。</td></tr><tr><td>35</td><td><p><a href="/python3/python3-os-mkdir.html">os.mkdir(path[, mode])</a></p><br>以数字mode的mode创建一个名为path的文件夹.默认的 mode 是 0777 (八进制)。 </td></tr><tr><td>36</td><td><p><a href="/python3/python3-os-mkfifo.html">os.mkfifo(path[, mode])</a></p><br>创建命名管道，mode 为数字，默认为 0666 (八进制) </td></tr>
<tr><td>37</td><td><p><a href="/python3/python3-os-mknod.html">os.mknod(filename[, mode=0600, device])</a><br>创建一个名为filename文件系统节点（文件，设备特别文件或者命名pipe）。</p></td></tr><tr><td>38</td><td><p><a href="/python3/python3-os-open.html">os.open(file, flags[, mode])</a></p><br>打开一个文件，并且设置需要的打开选项，mode参数是可选的</td></tr>
<tr><td>39</td><td><p><a href="/python3/python3-os-openpty.html">os.openpty()</a></p><br>打开一个新的伪终端对。返回 pty 和 tty的文件描述符。</td></tr>
<tr><td>40</td><td><p><a href="/python3/python3-os-pathconf.html">os.pathconf(path, name)</a></p><br>
返回相关文件的系统配置信息。 </td></tr>
<tr><td>41</td><td><p><a href="/python3/python3-os-pipe.html">os.pipe()</a></p><br>创建一个管道. 返回一对文件描述符(r, w) 分别为读和写</td></tr>
<tr><td>42</td><td><p><a href="/python3/python3-os-popen.html">os.popen(command[, mode[, bufsize]])</a></p><br>从一个 command 打开一个管道</td></tr>
<tr><td>43</td><td><p><a href="/python3/python3-os-read.html">os.read(fd, n)</a></p><br>从文件描述符 fd 中读取最多 n 个字节，返回包含读取字节的字符串，文件描述符 fd对应文件已达到结尾, 返回一个空字符串。</td></tr>
<tr><td>44</td><td><p><a href="/python3/python3-os-readlink.html">os.readlink(path)</a></p><br>返回软链接所指向的文件 </td></tr>
<tr><td>45</td><td><p><a href="/python3/python3-os-remove.html">os.remove(path)</a></p><br>删除路径为path的文件。如果path 是一个文件夹，将抛出OSError; 查看下面的rmdir()删除一个 directory。 </td></tr>
<tr><td>46</td><td><p><a href="/python3/python3-os-removedirs.html">os.removedirs(path)</a></p><br>递归删除目录。</td></tr>
<tr><td>47</td><td><p><a href="/python3/python3-os-rename.html">os.rename(src, dst)</a></p><br>重命名文件或目录，从 src 到 dst</td></tr>
<tr><td>48</td><td><p><a href="/python3/python3-os-renames.html">os.renames(old, new)</a></p><br>递归地对目录进行更名，也可以对文件进行更名。</td></tr>
<tr><td>49</td><td><p><a href="/python3/python3-os-rmdir.html">os.rmdir(path)</a></p><br>删除path指定的空目录，如果目录非空，则抛出一个OSError异常。</td></tr>
<tr><td>50</td><td><p><a href="/python3/python3-os-stat.html">os.stat(path)</a></p><br>获取path指定的路径的信息，功能等同于C API中的stat()系统调用。</td></tr>
<tr><td>51</td><td><p><a href="/python3/python3-os-stat_float_times.html">os.stat_float_times([newvalue])</a><br>决定stat_result是否以float对象显示时间戳</p></td></tr>
<tr><td>52</td><td><p><a href="/python3/python3-os-statvfs.html">os.statvfs(path)</a></p><br>获取指定路径的文件系统统计信息</td></tr>
<tr><td>53</td><td><p><a href="/python3/python3-os-symlink.html">os.symlink(src, dst)</a></p><br>创建一个软链接</td></tr>
<tr><td>54</td><td><p><a href="/python3/python3-os-tcgetpgrp.html">os.tcgetpgrp(fd)</a></p><br>返回与终端fd（一个由os.open()返回的打开的文件描述符）关联的进程组 </td></tr>
<tr><td>55</td><td><p><a href="/python3/python3-os-tcsetpgrp.html">os.tcsetpgrp(fd, pg)</a></p><br>设置与终端fd（一个由os.open()返回的打开的文件描述符）关联的进程组为pg。</td></tr>
<tr><td>56</td><td><p>os.tempnam([dir[, prefix]])</p><br><strong style="color:red">Python3 中已删除。</strong>返回唯一的路径名用于创建临时文件。 </td></tr>
<tr><td>57</td><td><p>os.tmpfile()</p><br><strong  style="color:red">Python3 中已删除。</strong>返回一个打开的模式为(w+b)的文件对象 .这文件对象没有文件夹入口，没有文件描述符，将会自动删除。 </td></tr>
<tr><td>58</td><td><p>os.tmpnam()</p><br><strong  style="color:red">Python3 中已删除。</strong>为创建一个临时文件返回一个唯一的路径</td></tr>
<tr><td>59</td><td><p><a href="/python3/python3-os-ttyname.html">os.ttyname(fd)</a></p><br>返回一个字符串，它表示与文件描述符fd 关联的终端设备。如果fd 没有与终端设备关联，则引发一个异常。</td></tr>
<tr><td>60</td><td><p><a href="/python3/python3-os-unlink.html">os.unlink(path)</a></p><br>删除文件路径 </td></tr>
<tr><td>61</td><td><p><a href="/python3/python3-os-utime.html">os.utime(path, times)</a></p><br>返回指定的path文件的访问和修改的时间。 </td></tr>
<tr><td>62</td><td><p><a href="/python3/python3-os-walk.html">os.walk(top[, topdown=True[, onerror=None[, followlinks=False]]])</a></p><br>输出在文件夹中的文件名通过在树中游走，向上或者向下。</td></tr>
<tr><td>63</td><td><p><a href="/python3/python3-os-write.html">os.write(fd, str)</a></p><br>写入字符串到文件描述符 fd中. 返回实际写入的字符串长度</td></tr>
<tr><td>64</td><td><p><a href="/python/os-write.html"><a href="/python3/python3-os-path.html" rel="noopener noreferrer" target="_blank">os.path 模块</a></a></p><br>获取文件的属性信息。</td></tr>
<tr><td>65</td><td><p><a href="/python/os-write.html"><a href="/python3/python3-os-pardir.html" rel="noopener noreferrer" target="_blank">os.pardir()</a></a></p><br>获取当前目录的父目录，以字符串形式显示目录名。</td></tr>
</tbody></table>


## 异常处理

### try/except

### try/except...else

### try-finally

```
try:
    runoob()
except AssertionError as error:
    print(error)
else:
    try:
        with open('file.log') as file:
            read_data = file.read()
    except FileNotFoundError as fnf_error:
        print(fnf_error)
finally:
    print('这句话，无论异常是否发生都会执行。')
```

### raise

`raise [Exception [, args [, traceback]]]`

```
a=100
if a>10:
    raise Exception('山中无甲子')
#结果
Traceback (most recent call last):
  File "F:/test/list/test.py", line 3, in <module>
    raise Exception('山中无甲子')
Exception: 山中无甲子
```

### 自定义异常

## 作用域

### 全局变量和局部变量

定义在函数内部的变量拥有一个局部作用域，定义在函数外的拥有全局作用域。
局部变量只能在其被声明的函数内部访问，而全局变量可以在整个程序范围内访问。调用函数时，所有在函数内声明的变量名称都将被加入到作用域中

```
total = 0 # 这是一个全局变量
# 可写函数说明
def sum( arg1, arg2 ):
    #返回2个参数的和."
    total = arg1 + arg2 # total在这里是局部变量.
    print ("函数内是局部变量 : ", total)
    return total
 
#调用sum函数
sum( 10, 20 )
print ("函数外是全局变量 : ", total)
# 结果
函数内是局部变量 :  30
函数外是全局变量 :  0
```

### global和nonlocal关键字

```
num = 1
def fun1():
    global num  # 需要使用 global 关键字声明
    print(num) 
    num = 123
    print(num)
fun1()
print(num)
# 结果
1
123
123
```

```
def outer():
    num = 10
    def inner():
        nonlocal num   # nonlocal关键字声明
        num = 100
        print(num)
    inner()
    print(num)
outer()
# 结果
100
100
```

