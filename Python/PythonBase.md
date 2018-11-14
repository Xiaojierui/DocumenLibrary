# Python基础
---
## 快速上手：基础知识

#### 1.1 交互式解释器

如果你熟悉其他计算机语言，可能习惯了在每行末尾都加上分号。在Python中无需这样做，
因为在Python中，一行就是一行。如果你愿意，也可加上分号，但不会有任何影响（除非后面还
有其他代码），况且大家通常都不这样做。

<pre>
>>> print("Hello, world!")
等你按下回车键后，将出现如下输出：
Hello, world!
>>>
>>>>是提示符，可在它后面输入一些内容。 例如， 如果你输入print("Hello,
world!")并按回车键， Python解释器将打印字符串"Hello, world!"，然后再次显示提示符
</pre>

解释器还指出了问题出在什么地方：使用红色背景色（在命令行解释器中，使用的
是脱字符号^）突出单词。help()

#### 1.2 算法是什么
算法都由对象和语句组成
#### 1.3 数和表达式
<pre>
整数运算：
>>> 2 + 2
结果应该为4
>>> 53672 + 235253
288925
小数运算
>>> 1 / 2
0.5
>>> 1 / 1
1.0

如果你想丢弃小数部分，即执行整除运算，可使用双斜杠。
>>> 1 // 2
0
>>> 1 // 1
1
>>> 5.0 // 2.4
2.0
求余
>>> 10 % -3
-2
>>> -10 % 3 
2
>>> 9 % 3 
0
>>> 2.75 % 0.5
0.25

乘法
>>> 2 ** 3
8
>>> -3 ** 2
>-9
</pre>
<pre>
十六进制
>>> 0xAF
175
八进制
>>> 010
8
二进制
>>> 0b1011010010
722
</pre>

#### 1.4 变量

<pre>
>>> x = 3
>>> x * 2
6
</pre>
**在Python中，名称（标识符）只能由字母、数字和下划线（_）构成，且不能以数字打头。**

**使用Python变量前必须给它赋值，因为Python变量没有默认值。**

#### 1.5 语句
<pre>
>>> 2 * 2
4
>>> print(2 * 2)
4

>>> if 1 == 2: print('One equals two')
>>> if 1 == 1: print('One equals one')
One equals one
>>>
</pre>

#### 1.6 获取用户输入
<pre>
>>> input("The meaning of life: ")
The meaning of life: 42
'42

>>> x = input("x: ")
x: 34
>>> y = input("y: ")
y: 42
>>> print(int(x) * int(y))
1428
</pre>

#### 1.7 函数
**round()  接近的数**
<pre>
>>> 2 ** 3
8
>>> pow(2, 3)
8

>>> abs(-10)
10
>>> 2 // 3
0
>>> round(2 / 3)
1.0
</pre>

#### 1.8 模块
 **ceil与floor相反，返回大于或等于给定数
的最小整数。**
<pre>
>>> import math
>>> math.floor(32.9)
32

>>> int(32.9)
32

>>> math.ceil(32.3)
33
>>> math.ceil(32)
32

>>> from math import sqrt
>>> sqrt(9)
3.0

>>> from math import sqrt
>>> sqrt(9)
3.0
通过使用命令import的变种from module import function，可在调用函数时不指定模块前缀。

</pre>
事实上，可使用变量来引用函数（以及其他大部分Python元素）。执行赋值语句foo =math.sqrt后，就可使用foo来计算平方根。例如， foo(4)的结果为2.0。

#### 1.8.1 cmath 和复数
<pre>
>>> import cmath
>>> cmath.sqrt(-1)
1j
</pre>
1j是个虚数，虚数都以j（或J）结尾。复数算术运算都基于如下定义： -1的平方根为1j。
<pre>
>>> (1 + 3j) * (9 + 4j)
(-3 + 31j)
从这个示例可知， Python本身提供了对复数的支持。
</pre>
注意 Python没有专门表示虚数的类型，而将虚数视为实部为零的复数

(1)运行 Python 脚本    
在Windows中使用如下命令来执行这个脚本：   
C:\>python hello.py    
在UNIX系统中，可使用如下命令：  
$ python hello.py   

(2)注释    
`#`表示

#### 1.10 字符串
<pre>
>>> "Hello, world!"
'Hello, world!
</pre>

单引号字符串以及对引号转义
<pre>
>>> 'Let's go!
SyntaxError: invalid syntax

>>> 'Let\'s go!'
"Let's go!"

>>> "\"Hello, world!\" she said"
'"Hello, world!" she said'
</pre>

拼接字符串
<pre>
>>> "Hello, " + "world!"
'Hello, world!'
>>> x = "Hello, "
>>> y = "world!"
>>> x + y
'Hello, world!'
</pre>

字符串表示 str 和 repr
<pre>
>>> "Hello, world!"
'Hello, world!'
>>> print("Hello, world!")
Hello, world!
如果再加上表示换行符的编码\n，差别将更明显。
>>> "Hello,\nworld!"
'Hello,\nworld!'
>>> print("Hello,\nworld!")
Hello,
world!

>>> print(repr("Hello,\nworld!"))
'Hello,\nworld!'
>>> print(str("Hello,\nworld!"))
Hello,
world!
</pre>
长字符串、原始字符串和字节
<pre>
要表示很长的字符串（跨越多行的字符串），可使用三引号（而不是普通引号）。
print('''This is a very long string. It continues here.
And it's not over yet. "Hello, world!"
Still here.''')
还可使用三个双引号，如"""like this"""。请注意，这让解释器能够识别表示字符串开始
和结束位置的引号，因此字符串本身可包含单引号和双引号，无需使用反斜杠进行转义

常规字符串也可横跨多行。只要在行尾加上反斜杠，反斜杠和换行符将被转义，即被忽
略。例如，如果编写如下代码：
print("Hello, \ world!")
它将打印Hello, world!。这种处理手法也适用于表达式和语句。
>>> 1 + 2 + \
4 + 5
12
>>> print \
('Hello, world')
Hello, world


>>> print(r'C:\nowhere')
C:\nowhere
>>> print(r'C:\Program Files\fnord\foo\bar\baz\frozz\bozz')
C:\Program Files\fnord\foo\bar\baz\frozz\bozz


>>> "\u00C6"
'Æ'
>>> "\U0001F60A"
'☺ '
>>> "This is a cat: \N{Cat}"
'This is a cat: '
要获悉字符的Unicode码点和名称，可在网上使用有关该字符的描述进行搜索，也可参阅特
定的网站，如http://unicode-table.com。
</pre>

#### 涉及函数

<pre>
abs(number) 返回指定数的绝对值
bytes(string, encoding[, errors]) 对指定的字符串进行编码，并以指定的方式处理错误
cmath.sqrt(number) 返回平方根；可用于负数
float(object) 将字符串或数字转换为浮点数
help([object]) 提供交互式帮助
input(prompt) 以字符串的方式获取用户输入
int(object) 将字符串或数转换为整数
math.ceil(number) 以浮点数的方式返回向上圆整的结果
math.floor(number) 以浮点数的方式返回向下圆整的结果
math.sqrt(number) 返回平方根；不能用于负数
pow(x, y[, z]) 返回x的y次方对z求模的结果
print(object, ...) 将提供的实参打印出来，并用空格分隔
vrepr(object) 返回指定值的字符串表示
round(number[, ndigits]) 四舍五入为指定的精度，正好为5时舍入到偶数
str(object) 将指定的值转换为字符串。用于转换bytes时，可指定编码和错误处理方式
</pre>
---
