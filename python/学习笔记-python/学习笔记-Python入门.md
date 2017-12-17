<!-- TOC -->

- [Python 教程](#python-教程)
    - [Python简介](#python简介)
    - [安装 Python](#安装-python)
    - [第一个Python程序](#第一个python程序)
        - [使用文本编辑器](#使用文本编辑器)
    - [Python 代码运行助手](#python-代码运行助手)
    - [输入和输出](#输入和输出)
    - [Python基础](#python基础)
        - [数据类型和变量](#数据类型和变量)
            - [数据类型](#数据类型)
            - [变量](#变量)
        - [字符串和编码](#字符串和编码)
        - [使用list和tuple](#使用list和tuple)
            - [list](#list)
            - [tuple](#tuple)
            - [小结](#小结)
        - [条件判断](#条件判断)
        - [循环](#循环)
        - [使用dict和set](#使用dict和set)
            - [dict](#dict)
            - [set](#set)
            - [小结](#小结-1)
    - [函数](#函数)
        - [调用函数](#调用函数)
        - [定义函数](#定义函数)
        - [函数的参数](#函数的参数)
            - [位置参数(必选参数)](#位置参数必选参数)
            - [默认参数](#默认参数)
            - [可变参数](#可变参数)
            - [关键字参数](#关键字参数)
            - [命名关键字参数](#命名关键字参数)
            - [参数组合](#参数组合)
            - [练习](#练习)
            - [小结](#小结-2)
        - [递归函数](#递归函数)
            - [练习](#练习-1)
    - [高级特性](#高级特性)
        - [切片](#切片)
        - [迭代](#迭代)
        - [列表生成式](#列表生成式)
        - [练习](#练习-2)
        - [小结](#小结-3)
        - [生成器](#生成器)
            - [小结](#小结-4)
        - [迭代器](#迭代器)
    - [函数式编程](#函数式编程)
        - [高阶函数](#高阶函数)
            - [Map/Reduce](#mapreduce)
            - [filter](#filter)
            - [sorted](#sorted)
        - [返回函数](#返回函数)
        - [匿名函数](#匿名函数)
            - [练习](#练习-3)
        - [装饰器](#装饰器)
        - [偏函数](#偏函数)
    - [模块](#模块)
        - [使用模块](#使用模块)
        - [安装第三方模块](#安装第三方模块)
    - [面向对象编程](#面向对象编程)
        - [类和实例](#类和实例)
        - [访问限制](#访问限制)
        - [继承和多态](#继承和多态)
        - [获取对象信息](#获取对象信息)
        - [实例属性和类属性](#实例属性和类属性)
    - [面向对象高级编程](#面向对象高级编程)
    - [使用`__slots__`](#使用__slots__)
        - [使用`@property`](#使用property)
            - [练习](#练习-4)
        - [多重继承](#多重继承)
        - [定制类](#定制类)
        - [使用枚举类](#使用枚举类)
    - [错误、调试和测试](#错误调试和测试)
        - [错误处理](#错误处理)
        - [调试](#调试)
        - [单元测试](#单元测试)
        - [文档测试](#文档测试)
    - [IO编程（同步）](#io编程同步)
        - [文件读写](#文件读写)
        - [`StringIO`和`BytesIO`](#stringio和bytesio)
        - [操作文件和目录](#操作文件和目录)
        - [序列化](#序列化)
    - [进程和线程](#进程和线程)
        - [多进程](#多进程)
        - [多线程](#多线程)
        - [ThreadLocal](#threadlocal)
        - [分布式进程](#分布式进程)
    - [正则表达式](#正则表达式)
    - [常用内置模块](#常用内置模块)
        - [`datetime`](#datetime)
        - [`collections`](#collections)
        - [base64](#base64)
        - [struct](#struct)
        - [hashlib](#hashlib)
            - [hmac](#hmac)
        - [itertools](#itertools)
        - [contextlib](#contextlib)
        - [urllib](#urllib)
        - [XML](#xml)
        - [HTMLParser](#htmlparser)
    - [常用第三方模块](#常用第三方模块)
    - [virtualenv](#virtualenv)
    - [图形界面](#图形界面)
    - [网络编程](#网络编程)
        - [TCP/IP简介](#tcpip简介)
        - [TCP编程](#tcp编程)
        - [UDP编程](#udp编程)

<!-- /TOC -->


* 学习来源：[Python教程](https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000) by廖雪峰

# Python 教程

## Python简介

许多大型网站就是用Python开发的，例如YouTube、Instagram，还有国内的豆瓣。很多大公司，包括Google、Yahoo等，甚至NASA（美国航空航天局）都大量地使用Python。

Python的缺点

* 第一个缺点就是运行速度慢，和C程序相比非常慢，因为Python是解释型语言，你的代码在执行时会一行一行地翻译成CPU能理解的机器码，这个翻译过程非常耗时，所以很慢。而C程序是运行前直接编译成CPU能执行的机器码，所以非常快。
* 第二个缺点就是代码不能加密。如果要发布你的Python程序，实际上就是发布源代码，这一点跟C语言不同，C语言不用发布源代码，只需要把编译后的机器码（也就是你在Windows上常见的xxx.exe文件）发布出去。要从机器码反推出C代码是不可能的，所以，凡是编译型的语言，都没有这个问题，而解释型的语言，则必须把源码发布出去。

## 安装 Python


当我们编写Python代码时，我们得到的是一个包含Python代码的以.py为扩展名的文本文件。要运行代码，就需要Python解释器去执行.py文件。

由于整个Python语言从规范到解释器都是开源的，所以理论上，只要水平够高，任何人都可以编写Python解释器来执行Python代码（当然难度很大）。事实上，确实存在多种Python解释器。

Python的解释器很多(有CPython、IPython
、PyPy、Jython、IronPython)，但使用最广泛的还是CPython。如果要和Java或.Net平台交互，最好的办法不是用Jython或IronPython，而是通过网络调用来交互，确保各程序之间的独立性。

## 第一个Python程序

在写代码之前，请**千万不要**用“复制”-“粘贴”把代码从页面粘贴到你自己的电脑上。写程序也讲究一个感觉，你需要一个字母一个字母地把代码自己敲进去，在敲代码的过程中，初学者经常会敲错代码：拼写不对，大小写不对，混用中英文标点，混用空格和`Tab`键，所以，你需要仔细地检查、对照，才能以最快的速度掌握如何写程序。

### 使用文本编辑器

用文本编辑器写Python程序，然后保存为后缀为.py的文件，就可以用Python直接运行这个程序了。

Python的交互模式和直接运行.py文件有什么区别呢？

直接输入python进入交互模式，相当于启动了Python解释器，但是等待你一行一行地输入源代码，每输入一行就执行一行。

直接运行.py文件相当于启动了Python解释器，然后一次性把.py文件的源代码给执行了，你是没有机会以交互的方式输入源代码的。

用Python开发程序，完全可以一边在文本编辑器里写代码，一边开一个交互式命令窗口，在写代码的过程中，把部分代码粘到命令行去验证，事半功倍！前提是得有个27'的超大显示器！

## Python 代码运行助手

一种可以在网页中运行Python代码的助手。

## 输入和输出
任何计算机程序都是为了执行一个特定的任务，有了输入，用户才能告诉计算机程序所需的信息，有了输出，程序运行后才能告诉用户任务的结果。

输入是Input，输出是Output，因此，我们把输入输出统称为Input/Output，或者简写为IO。

input()和print()是在命令行下面最基本的输入和输出，但是，用户也可以通过其他更高级的图形界面完成输入和输出，比如，在网页上的一个文本框输入自己的名字，点击“确定”后在网页上看到输出信息。

## Python基础

Python的语法比较简单，采用缩进方式，写出来的代码就像下面的样子：
```py
# print absolute value of an integer:
a=100
if(a>0):
    print(a)
else:
    print(-a)
```
以#开头的语句是注释。其他每一行都是一个语句，当语句以冒号:结尾时，缩进的语句视为代码块。缩进有利有弊。好处是强迫你写出格式化的代码，但没有规定缩进是几个空格还是Tab。按照约定俗成的管理，应该始终坚持使用**4个空格**的缩进。

Python程序是**大小写**敏感的，如果写错了大小写，程序会报错。

### 数据类型和变量

#### 数据类型

计算机顾名思义就是可以做数学计算的机器，因此，计算机程序理所当然地可以处理各种数值。但是，计算机能处理的远不止数值，还可以处理文本、图形、音频、视频、网页等各种各样的数据，不同的数据，需要定义不同的数据类型。在Python中，能够直接处理的数据类型有以下几种：

* 整数


* 浮点数

* 字符串
字符串是以单引号`'`或双引号`"`括起来的任意文本。特殊字符使用转义字符处理，转义字符`\`可以转义很多字符，比如`\n`表示换行，`\t`表示制表符，字符`\`本身也要转义，所以`\\`表示的字符就是`\`
* 布尔值
布尔值可以用`and`、`or`和`not`运算。

* 空值
空值是Python里一个特殊的值，用None表示。None不能理解为0，因为0是有意义的，而None是一个特殊的空值。

此外，Python还提供了列表、字典等多种数据类型，还允许创建自定义数据类型，我们后面会继续讲到。

#### 变量

### 字符串和编码

因为计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用8个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），如果要表示更大的整数，就必须用更多的字节。比如两个字节可以表示的最大整数是`65535`，4个字节可以表示的最大整数是`4294967295`。

由于计算机是美国人发明的，因此，最早只有127个字符被编码到计算机里，也就是大小写英文字母、数字和一些符号，这个编码表被称为`ASCII`编码，比如大写字母A的编码是`65`，小写字母z的编码是`122`。

但是要处理中文显然一个字节是不够的，至少需要两个字节，而且还不能和ASCII编码冲突，所以，中国制定了`GB2312`编码，用来把中文编进去。

你可以想得到的是，全世界有上百种语言，日本把日文编到`Shift_JIS`里，韩国把韩文编到`Euc-kr`里，各国有各国的标准，就会不可避免地出现冲突，结果就是，在多语言混合的文本中，显示出来会有乱码。

因此，Unicode应运而生。Unicode把所有语言都统一到一套编码里，这样就不会再有乱码问题了。

ASCII编码和Unicode编码的区别：ASCII编码是1个字节，而Unicode编码通常是2个字节

字母`A`用ASCII编码是十进制的`65`，二进制的`01000001`；

字符`0`用ASCII编码是十进制的`48`，二进制的`00110000`，注意字符`'0'`和整数`0`是不同的；

汉字`中`已经超出了ASCII编码的范围，用Unicode编码是十进制的`20013`，二进制的`01001110 00101101`。

你可以猜测，如果把ASCII编码的A用Unicode编码，只需要在前面补0就可以，因此，A的Unicode编码是00000000 01000001。

你可以猜测，如果把ASCII编码的`A`用Unicode编码，只需要在前面补0就可以，因此，`A`的Unicode编码是`00000000 01000001`。

字符串和编码

阅读: 895492
字符编码

我们已经讲过了，字符串也是一种数据类型，但是，字符串比较特殊的是还有一个编码问题。

因为计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用8个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），如果要表示更大的整数，就必须用更多的字节。比如两个字节可以表示的最大整数是65535，4个字节可以表示的最大整数是4294967295。

由于计算机是美国人发明的，因此，最早只有127个字符被编码到计算机里，也就是大小写英文字母、数字和一些符号，这个编码表被称为ASCII编码，比如大写字母A的编码是65，小写字母z的编码是122。

但是要处理中文显然一个字节是不够的，至少需要两个字节，而且还不能和ASCII编码冲突，所以，中国制定了GB2312编码，用来把中文编进去。

你可以想得到的是，全世界有上百种语言，日本把日文编到Shift_JIS里，韩国把韩文编到Euc-kr里，各国有各国的标准，就会不可避免地出现冲突，结果就是，在多语言混合的文本中，显示出来会有乱码。

char-encoding-problem

因此，Unicode应运而生。Unicode把所有语言都统一到一套编码里，这样就不会再有乱码问题了。

Unicode标准也在不断发展，但最常用的是用两个字节表示一个字符（如果要用到非常偏僻的字符，就需要4个字节）。现代操作系统和大多数编程语言都直接支持Unicode。

现在，捋一捋ASCII编码和Unicode编码的区别：ASCII编码是1个字节，而Unicode编码通常是2个字节。

字母A用ASCII编码是十进制的65，二进制的01000001；

字符0用ASCII编码是十进制的48，二进制的00110000，注意字符'0'和整数0是不同的；

汉字中已经超出了ASCII编码的范围，用Unicode编码是十进制的20013，二进制的01001110 00101101。

你可以猜测，如果把ASCII编码的A用Unicode编码，只需要在前面补0就可以，因此，A的Unicode编码是00000000 01000001。

新的问题又出现了：如果统一成Unicode编码，乱码问题从此消失了。但是，如果你写的文本基本上全部是英文的话，用Unicode编码比ASCII编码需要多一倍的存储空间，在存储和传输上就十分不划算。

所以，本着节约的精神，又出现了把Unicode编码转化为“可变长编码”的UTF-8编码。UTF-8编码把一个Unicode字符根据不同的数字大小编码成1-6个字节，常用的英文字母被编码成1个字节，汉字通常是3个字节，只有很生僻的字符才会被编码成4-6个字节。如果你要传输的文本包含大量英文字符，用UTF-8编码就能节省空间：

| 字符 |ASCII|	Unicode|	UTF-8|
|----:|-----:|-----:|-----:|
|A|01000001|00000000 01000001|01000001|
|中|x|01001110 00101101|11100100 10111000 10101101|

从上面的表格还可以发现，UTF-8编码有一个额外的好处，就是ASCII编码实际上可以被看成是UTF-8编码的一部分，所以，大量只支持ASCII编码的历史遗留软件可以在UTF-8编码下继续工作。

搞清楚了ASCII、Unicode和UTF-8的关系，我们就可以总结一下现在计算机系统通用的字符编码工作方式：

在计算机内存中，统一使用Unicode编码，当需要保存到硬盘或者需要传输的时候，就转换为UTF-8编码。

用记事本编辑的时候，从文件读取的UTF-8字符被转换为Unicode字符到内存里，编辑完成后，保存的时候再把Unicode转换为UTF-8保存到文件。

所以你看到很多网页的源码上会有类似`<meta charset="UTF-8" />`的信息，表示该网页正是用的UTF-8编码。

### 使用list和tuple

#### list

Python内置的一种数据类型是列表：list。list是一种有序的集合，可以随时添加和删除其中的元素。
> 相当于数组的概念
* len() 获取元素的个数
* 有append、insert、pop方法

#### tuple

另一种有序列表叫元组：tuple。tuple和list非常类似，但是tuple一旦初始化就不能修改，比如同样是列出同学的名字：
```py
classmates = ('Michael', 'Bob', 'Tracy')
```
现在，classmates这个tuple不能变了，它也没有append()，insert()这样的方法。其他获取元素的方法和list是一样的，你可以正常地使用classmates[0]，classmates[-1]，但不能赋值成另外的元素。

不可变的tuple有什么意义？因为tuple不可变，所以代码更安全。如果可能，能用tuple代替list就尽量用tuple。

#### 小结
list和tuple是Python内置的有序集合，一个可变，一个不可变。根据需要来选择使用它们。

### 条件判断

条件判断可以让计算机自己做选择，Python的if...elif...else很灵活。

条件判断从上向下匹配，当满足条件时执行对应的块内语句，后续的elif和else都不再执行。

> Python的elseif简写为elif，这是与其他语言不同之处

### 循环

Python的循环有两种，一种是for...in循环,一种是 while，依次把list或tuple中的每个元素迭代出来，跟其他语言相同。

### 使用dict和set

#### dict

Python内置了字典：dict的支持，dict全称dictionary，在其他语言中也称为map，使用键-值（key-value）存储，具有极快的查找速度。比如下面是一个字典`d`

```py
d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
```

和list比较，dict有以下几个特点：

* 查找和插入的速度极快，不会随着key的增加而变慢；
* 需要占用大量的内存，内存浪费多。

而list相反：

* 查找和插入的时间随着元素的增加而增加；
* 占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。

#### set
set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

要创建一个set，需要提供一个list作为输入集合：
```py
s = set([1, 2, 3])
s #{1,2,3}
```
注意，传入的参数[1, 2, 3]是一个list，而显示的{1, 2, 3}只是告诉你这个set内部有1，2，3这3个元素，显示的顺序也不表示set是有序的。重复元素在set中自动被过滤。可通过`add` 和`remove`方法增加和移除元素。

set和dict的唯一区别仅在于没有存储对应的value，但是，set的原理和dict一样，所以，同样不可以放入可变对象，因为无法判断两个可变对象是否相等，也就无法保证set内部“不会有重复元素”。试试把list放入set，看看是否会报错。

#### 小结
使用key-value存储结构的dict在Python中非常有用，选择不可变对象作为key很重要，最常用的key是字符串。

tuple虽然是不变对象，但试试把(1, 2, 3)和(1, [2, 3])放入dict或set中，并解释结果。

## 函数

### 调用函数

### 定义函数

定义函数时，需要确定函数名和参数个数；

如果有必要，可以先对参数的数据类型做检查；

函数体内部可以用`return`随时返回函数结果；

函数执行完毕也没有`return`语句时，自动`return None`。

函数可以同时返回多个值，但其实就是一个tuple。

### 函数的参数

Python的函数定义非常简单，但灵活度却非常大。除了正常定义的**必选参数**外，还可以使用**默认参数**、**可变参数**和**关键字参数**，使得函数定义出来的接口，不但能处理复杂的参数，还可以简化调用者的代码。

#### 位置参数(必选参数)

#### 默认参数
> 定义默认参数要牢记一点：**默认参数必须指向不变对象！**

```py
def power(x, n=2):
    s = 1
    while n > 0:
        n = n - 1
        s = s * x
    return s
```

#### 可变参数
可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple
```py
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```

#### 关键字参数
关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。

```py
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```

#### 命名关键字参数

如果要限制关键字参数的名字，就可以用命名关键字参数，例如，只接收`city`和`job`作为关键字参数。这种方式定义的函数如下：

```py
def person(name, age, *, city, job):
    print(name, age, city, job)
```
和关键字参数`**kw`不同，命名关键字参数需要一个特殊分隔符`*`，`*`后面的参数被视为命名关键字参数。

如果函数定义中已经有了一个可变参数，后面跟着的命名关键字参数就不再需要一个特殊分隔符`*`了：
```py
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
```

#### 参数组合

在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。

> 虽然可以组合多达5种参数，但不要同时使用太多的组合，否则函数接口的可理解性很差。

#### 练习
以下函数允许计算两个数的乘积，请稍加改造，变成可接收一个或多个数并计算乘积：
```py
# -*- coding: utf-8 -*-
def product(x, y):
    return x * y
```
my answer：
```py
# -*- coding: utf-8 -*-
def product(*numbers):
    # to do:检查是否为整数或浮点数
    sum=1
    for n in numbers:
        sum=sum*n
    return sum

a=product(5,6,7,9)
print(a)
```
#### 小结
Python的函数具有非常灵活的参数形态，既可以实现简单的调用，又可以传入非常复杂的参数。

默认参数一定要用不可变对象，如果是可变对象，程序运行时会有逻辑错误！

要注意定义可变参数和关键字参数的语法：

`*args`是可变参数，`args`接收的是一个tuple；

`**kw`是关键字参数，`kw`接收的是一个dict。

以及调用函数时如何传入可变参数和关键字参数的语法：

可变参数既可以直接传入：`func(1, 2, 3)`，又可以先组装list或tuple，再通过`*args`传入：`func(*(1, 2, 3))`；

关键字参数既可以直接传入：`func(a=1, b=2)`，又可以先组装dict，再通过`**kw`传入：`func(**{'a': 1, 'b': 2})`。

使用`*args`和`**kw`是Python的习惯写法，当然也可以用其他参数名，但最好使用习惯用法。

命名的关键字参数是为了限制调用者可以传入的参数名，同时可以提供默认值。

定义命名的关键字参数在没有可变参数的情况下不要忘了写分隔符`*`，否则定义的将是位置参数。

### 递归函数

递归函数的优点是定义简单，逻辑清晰。理论上，所有的递归函数都可以写成循环的方式，但循环的逻辑不如递归清晰。

使用递归函数的优点是逻辑简单清晰，缺点是过深的调用会导致栈溢出。

针对尾递归优化的语言可以通过尾递归防止栈溢出。尾递归事实上和循环是等价的，没有循环语句的编程语言只能通过尾递归实现循环。

Python标准的解释器没有针对尾递归做优化，任何递归函数都存在栈溢出的问题。

#### 练习

[汉诺塔](https://baike.baidu.com/item/%E6%B1%89%E8%AF%BA%E5%A1%94/3468295)的移动可以用递归函数非常简单地实现。

请编写move(n, a, b, c)函数，它接收参数n，表示3个柱子A、B、C中第1个柱子A的盘子数量，然后打印出把所有盘子从A借助B移动到C的方法，例如：
```py
# -*- coding: utf-8 -*-
def move(n, a, b, c):
    if n == 1:
        print(a, '-->', c)

```
my answer:
```py
# -*- coding: utf-8 -*-
# 暂时不做，后面先去研究什么是汉诺塔
```
## 高级特性

### 切片

对这种经常取指定索引范围的操作，用循环十分繁琐，因此，Python提供了切片（Slice）操作符`:`，能大大简化这种操作。可使用切片的对象有list、tuple、str。
```py
L1 = list(range(100)) # [0, 1, 2, 3, ..., 99]

# 取L1的前10个数
L1[:10]           # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] 
L1[0:10]          # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] 

# 取L1的前10个数
L1[-10:]          #[90, 91, 92, 93, 94, 95, 96, 97, 98, 99] 

# 前11-20个数
L1[10:20]         #[10, 11, 12, 13, 14, 15, 16, 17, 18, 19]

# 前10个数，每两个取一个
L1[:10:2]         # [0, 2, 4, 6, 8]

# 所有数，每5个取一个
L[::5] # [0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 60, 65, 70, 75, 80, 85, 90, 95]

(0, 1, 2, 3, 4, 5)[:3] # (0, 1, 2)
'ABCDEFG'[:3]     # 'ABC'
```
有了切片操作，很多地方循环就不再需要了。Python的切片非常灵活，一行代码就可以实现很多行循环才能完成的操作。

### 迭代
如果给定一个list或tuple，我们可以通过for循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。

可以看出，Python的for循环抽象程度要高于C的`for`循环，因为Python的`for`循环不仅可以用在list或tuple上，还可以作用在其他可迭代对象上。

list这种数据类型虽然有下标，但很多其他数据类型是没有下标的，但是，只要是可迭代对象，无论有无下标，都可以迭代，比如dict就可以迭代：

```py
d = {'a': 1, 'b': 2, 'c': 3}
for key in d
    print(key) 
    
# 输出：    
# a
# b
# c
```
默认情况下，dict迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。

如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断：
```py
from collections import Iterable
isinstance('abc', Iterable)   # True
isinstance([1,2,3], Iterable) # True
isinstance(123, Iterable)     # False
```
for循环里，同时引用了两个变量，在Python里是很常见的，比如下面的代码：
```py
for x, y in [(1, 1), (2, 4), (3, 9)]:
    print(x, y)
```
输出：
1 1
2 4
3 9

### 列表生成式

列表生成式即List Comprehensions，是Python内置的非常简单却强大的可以用来创建list的生成式。即可以在list中使用for来遍历,例如：
```py
[x * x for x in range(1, 11)] # [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

[x * x for x in range(1, 11) if x % 2 == 0] # [4, 16, 36, 64, 100]

[m + n for m in 'ABC' for n in 'XYZ'] # ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']

d = {'x': 'A', 'y': 'B', 'z': 'C' }
[k + '=' + v for k, v in d.items()] # ['y=B', 'x=A', 'z=C']

L = ['Hello', 'World', 'IBM', 'Apple']
[s.lower() for s in L] # ['hello', 'world', 'ibm', 'apple']
```

### 练习
```py
L = ['Hello', 'World', 18, 'Apple', None]
a= [s.lower() for s in L if isinstance(s,str)] 
print(a) # ['hello', 'world', 'apple']
```

### 小结
运用列表生成式，可以快速生成list，可以通过一个list推导出另一个list，而代码却十分简洁。

### 生成器

通过列表生成式，我们可以直接创建一个列表。但是，受到内存限制，列表容量肯定是有限的。而且，创建一个包含100万个元素的列表，不仅占用很大的存储空间，如果我们仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。

所以，如果列表元素可以按照某种算法推算出来，那我们是否可以在循环的过程中不断推算出后续的元素呢？这样就不必创建完整的list，从而节省大量的空间。在Python中，这种一边循环一边计算的机制，称为生成器：generator。

要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的[]改成()，就创建了一个generator：
```py
L = [x * x for x in range(10)]
L # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

g = (x * x for x in range(10))
g # generator object <genexpr> at 0x000001D58B221EB8>
```
创建`L`和`g`的区别仅在于最外层的`[]`和`()`，`L`是一个list，而`g`是一个generator。

我们可以直接打印出list的每一个元素，但我们怎么打印出generator的每一个元素呢？

如果要一个一个打印出来，可以通过next()函数获得generator的下一个返回值：
```py
next(g) # 0
next(g) # 1
next(g) # 4
next(g) # 6
next(g) # 16
next(g) # 25
next(g) # 36
...  #没有更多的元素时，抛出StopIteration的错误。
```

当然，上面这种不断调用next(g)实在是太变态了，正确的方法是使用for循环，因为generator也是可迭代对象

```py
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```
这就是定义generator的另一种方法。如果一个函数定义中包含yield关键字，那么这个函数就不再是一个普通函数，而是一个generator：
```py
f = fib(6)
f # <generator object fib at 0x104feaaa0>
```
这里，最难理解的就是generator和函数的执行流程不一样。函数是顺序执行，遇到return语句或者最后一行函数语句就返回。而变成generator的函数，在每次调用next()的时候执行，遇到yield语句返回，再次执行时从上次返回的yield语句处继续执行。

#### 小结

generator是非常强大的工具，在Python中，**可以简单地把列表生成式改成generator，也可以通过函数实现复杂逻辑的generator**。

要理解generator的工作原理，它是在`for`循环的过程中不断计算出下一个元素，并在适当的条件结束`for`循环。对于函数改成的generator来说，遇到return语句或者执行到函数体最后一行语句，就是结束generator的指令，`for`循环随之结束。

请注意区分普通函数和generator函数，普通函数调用直接返回结果：

```py
r = abs(6)
r # 6
```
generator函数的“调用”实际返回一个generator对象：

```py
g = fib(6)
g # <generator object fib at 0x1022ef948>
```

### 迭代器

我们已经知道，可以直接作用于for循环的数据类型有以下几种：一类是集合数据类型，如`list`、`tuple`、`dict`、`set`、`str`等；一类是`generator`，包括生成器和带`yield`的generator function。

凡是可作用于`for`循环的对象都是`Iterable`类型；

凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；

集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。**`Iterable`是可迭代对象，`Iterator`是迭代器**。

Python的`for`循环本质上就是通过不断调用`next()`函数实现的。

生成器不但可以作用于for循环，还可以被next()函数不断调用并返回下一个值，直到最后抛出StopIteration错误表示无法继续返回下一个值了。可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator

```py
from collections import Iterable
from collections import Iterator

isinstance([], Iterable) # True
isinstance([], Iterator) # False
isinstance(iter([]), Iterator) # True

isinstance({}, Iterable) # True
isinstance({}, Iterator) # False
isinstance(iter({}), Iterator) # True

isinstance('abc', Iterable) # True
isinstance('abc', Iterator) # False
isinstance(iter('abc'), Iterator) # True

isinstance((x for x in range(10)), Iterable) # True
isinstance((x for x in range(10)), Iterator) # True
```

## 函数式编程

函数是Python内建支持的一种封装，我们通过把大段代码拆成函数，通过一层一层的函数调用，就可以把复杂任务分解成简单的任务，这种分解可以称之为面向过程的程序设计。函数就是面向过程的程序设计的基本单元。

> 在项目管理中有WBS概念，也是把大的任务分解一个个小的任务，即也是把复杂的任务分解成更小的简单的任务。在生活中何尝不是一样，把大的目标分解很多个小目标，这样就不会产生畏惧，通过一步一步完成小目标，每天可以看到进步，还可以提升自信心，这样看似很难实现的大目标其实在慢慢靠近了。

而函数式编程（请注意多了一个“式”字）——Functional Programming，虽然也可以归结到面向过程的程序设计，但其思想更接近**数学计算**。

我们首先要搞明白计算机（Computer）和计算（Compute）的概念。

在计算机的层次上，CPU执行的是加减乘除的指令代码，以及各种条件判断和跳转指令，所以，**汇编语言是最贴近计算机的语言**。

而**计算则指数学意义上的计算，越是抽象的计算，离计算机硬件越远**。

**对应到编程语言，就是越低级的语言，越贴近计算机，抽象程度低，执行效率高，比如C语言；越高级的语言，越贴近计算，抽象程度高，执行效率低，比如Lisp语言**。

函数式编程就是一种抽象程度很高的编程范式，纯粹的函数式编程语言编写的函数没有变量，因此，任意一个函数，只要输入是确定的，输出就是确定的，这种纯函数我们称之为没有副作用。而允许使用变量的程序设计语言，由于函数内部的变量状态不确定，同样的输入，可能得到不同的输出，因此，这种函数是有副作用的。

函数式编程的一个特点就是，允许把函数本身作为参数传入另一个函数，还允许返回一个函数！

Python对函数式编程提供部分支持。由于Python允许使用变量，因此，Python不是纯函数式编程语言。

### 高阶函数

#### Map/Reduce

#### filter

#### sorted

### 返回函数

一个函数可以返回一个计算结果，也可以返回一个函数。返回一个函数时，牢记该函数并未执行，返回函数中不要引用任何可能会变化的变量。
> 既然函数里面可以定义函数，函数可以作为返回值返回，那么也就有闭包的概念，跟JS一样。

### 匿名函数

当我们在传入函数时，有些时候，不需要显式地定义函数，直接传入匿名函数更方便。在Python中，对匿名函数提供了有限支持。还是以`map()`函数为例，计算`f(x)=x2`时，除了定义一个`f(x)`的函数外，还可以直接传入匿名函数：
```py
 list(map(lambda x: x * x, [1, 2, 3, 4, 5, 6, 7, 8, 9])) #[1, 4, 9, 16, 25, 36, 49, 64, 81]
```
通过对比可以看出，匿名函数lambda x: x * x实际上就是：
```py
def f(x):
     return x * x
```
关键字`lambda`表示匿名函数，冒号前面的`x`表示函数参数。匿名函数有个限制，就是只能有一个表达式，不用写return，返回值就是该表达式的结果。用匿名函数有个好处，因为函数没有名字，不必担心函数名冲突。此外，匿名函数也是一个函数对象，也可以把匿名函数赋值给一个变量，再利用变量来调用该函数,也可以把匿名函数作为返回值返回。

Python对匿名函数的支持有限，只有一些简单的情况下可以使用匿名函数。

#### 练习
请用匿名函数改造下面的代码：
def is_odd(n):
    return n % 2 == 1

L = list(filter(is_odd, range(1, 20)))

my answer:
```py
L = list(filter(lambda x:x%2==1, range(1, 20)))
```

### 装饰器

> 没怎么看

### 偏函数
当函数的参数个数太多，需要简化时，使用`functools.partial`可以创建一个新的函数，这个新函数可以固定住原函数的部分参数，从而在调用时更简单。

## 模块

### 使用模块

### 安装第三方模块

## 面向对象编程

### 类和实例
> 概念和C#差不多，只是写法有点不同
定义一个学生类
```py
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
```

### 访问限制

如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线`__`，在Python中，实例的变量名如果以`__`开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问，所以，我们把Student类改一改：
```py
class Student(object):
    ...

    def get_name(self):
        return self.__name

    def get_score(self):
        return self.__score
```

### 继承和多态

### 获取对象信息

使用`type()`获取对象类型

使用`isinstance()`获取`class`类型

使用使用`dir()`获取对象的所有属性和方法，返回是一个包含字符串的list。仅仅把属性和方法列出来是不够的，配合`getattr()`、`setattr()`以及`hasattr()`，我们可以直接操作一个对象的状态

### 实例属性和类属性

由于Python是动态语言，根据类创建的实例可以任意绑定属性。所以在Python中
既可以在类上绑定属性，也可以在类的实例上绑定属性，在类的实例上绑定的属性不属于该类只属于该实例，在类上绑定的属性属于所有该类的实例。

同理，可以给类的某个实例绑定方法，该实例的属性和方法只属于该实例，不属于其他实例和该实例所属的类。

在编写程序的时候，千万不要对实例属性和类属性使用相同的名字，因为相同名称的实例属性将屏蔽掉类属性，但是当你删除实例属性后，再使用相同的名称，访问到的将是类属性。

实例属性属于各个实例所有，互不干扰；

类属性属于类所有，所有实例共享一个属性；

不要对实例属性和类属性使用相同的名字，否则将产生难以发现的错误。

## 面向对象高级编程

数据封装、继承和多态只是面向对象程序设计中最基础的3个概念。在Python中，面向对象还有很多高级特性，允许我们写出非常强大的功能。

我们会讨论多重继承、定制类、元类等概念。

## 使用`__slots__`

正常情况下，当我们定义了一个class，创建了一个class的实例后，我们可以给该实例绑定任何属性和方法，这就是**动态语言**的灵活性。

```py
class Student(object):
    pass
```
动态给Student绑定方法:

```py
def set_score(self, score):
    self.score = score
```
通常情况下，上面的`set_score`方法可以直接定义在class中，但动态绑定允许我们在程序运行的过程中动态给class加上功能，这在静态语言中很难实现。

Python允许在定义class的时候，定义一个特殊的`__slots__`变量，来限制该class实例能添加的属性,比如，只允许对Student实例添加name和age属性：

```py
class Student(object):
    __slots__ = ('name', 'age') # 用tuple定义允许绑定的属性名称
```
然后，我们试试：

```py
s=Student()
s.name='Lisa'
s.age=30
s.score=96 # 报错 AttributeError: 'Student' object has no attribute 'score'
```

由于`'score'`没有被放到`__slots__`中，所以不能绑定`score`属性，试图绑定`score`将得到AttributeError的错误。

使用`__slots__`要注意，`__slots__`定义的属性仅对当前类实例起作用，对继承的子类是不起作用的。除非在子类中也定义`__slots__`，这样，子类实例允许定义的属性就是自身的`__slots__`**加上父类的`__slots__`**。

### 使用`@property`

`@property`是一个装饰器，负责把一个方法变成属性。它广泛应用在类的定义中，可以让调用者写出简短的代码，同时保证对参数进行必要的检查，这样，程序运行时就减少了出错的可能性。

#### 练习

题目：请利用@property给一个Screen对象加上width和height属性，以及一个只读属性resolution：

```py
class Screen(object):
    
    @property
    def width(self):
        return self.__width

    @width.setter
    def width(self,value):
        self.__width=value

    @property
    def height(self):
        return self.__height

    @height.setter
    def height(self,value):
        self.__height=value

    @property
    def resolution(self):
        return self.__width*self.__height

s=Screen()
s.width=1024
s.height=768
print(s.resolution) # 320000
```

### 多重继承

由于Python允许使用多重继承，因此，MixIn就是一种常见的设计。

只允许单一继承的语言（如Java）不能使用MixIn的设计。但是C#也是支持多重继承的，这个跟Python应该一样。

### 定制类

下面是最常用的几个定制方法，还有很多可定制的方法，请参考[Python的官方文档](https://docs.python.org/3/reference/datamodel.html#special-method-names)。
`__str__`
`__repr__`
`__iter__`
`__getitem__`
`__getattr__`
`__call__`

### 使用枚举类

**`type()`**：动态创建类
```py
def fn(self, name='world'): # 先定义函数
    print('Hello, %s.' % name)
Hello = type('Hello', (object,), dict(hello=fn)) # 动态创建Hello class
```
要创建一个class对象，type()函数依次传入3个参数：

* class的名称；
* 继承的父类集合，注意Python支持多重继承，如果只有一个父类，别忘了tuple的单元素写法；
* class的方法名称与函数绑定，这里我们把函数fn绑定到方法名hello上。

正常情况下，我们都用`class Xxx...`来定义类，但是，`type()`函数也允许我们动态创建出类来，也就是说，动态语言本身支持运行期动态创建类，这和静态语言有非常大的不同，要在静态语言运行期创建类，必须构造源代码字符串再调用编译器，或者借助一些工具生成字节码实现，本质上都是动态编译，会非常复杂。

**`metaclass`**:
> todo:讲的有点复杂，没仔细看，回头再仔细研究下。

## 错误、调试和测试

### 错误处理

通过`try...except...finally...`的错误处理机制来处理程序错误，跟其他语言类似。

### 调试

### 单元测试

### 文档测试
> todo:只是大概秒了一眼，没细看

## IO编程（同步）

### 文件读写

文件读写是通过`open()`函数打开的文件对象完成的。使用`with`语句操作文件IO是个好习惯。

### `StringIO`和`BytesIO`

`StringIO`和`BytesIO`是在内存中操作`str`和`bytes`的方法，使得和读写文件具有一致的接口。

### 操作文件和目录

Python的`os`模块封装了操作系统的目录和文件操作，要注意这些函数有的在`os`模块中，有的在`os.path`模块中。

### 序列化

Python提供了`pickle`模块来实现序列化。我们把变量从内存中变成可存储或传输的过程称之为序列化，在Python中叫pickling，在其他语言中也被称之为serialization，marshalling，flattening等等，都是一个意思。序列化之后，就可以把序列化后的内容写入磁盘，或者通过网络传输到别的机器上。反过来，把变量内容从序列化的对象重新读到内存里称之为反序列化，即unpickling。

Python语言特定的序列化模块是pickle，但如果要把序列化搞得更通用、更符合Web标准，就可以使用`json`模块。如果我们要在不同的编程语言之间传递对象，就必须把对象序列化为标准格式，比如XML，但更好的方法是序列化为JSON，因为JSON表示出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输。JSON不仅是标准格式，并且比XML更快，而且可以直接在Web页面中读取，非常方便。

`json`模块的`dumps()`和`loads()`函数是定义得非常好的接口的典范。当我们使用时，只需要传入一个必须的参数。但是，当默认的序列化或反序列机制不满足我们的要求时，我们又可以传入更多的参数来定制序列化或反序列化的规则，既做到了接口简单易用，又做到了充分的扩展性和灵活性。

## 进程和线程

线程是最小的执行单元，而进程由至少一个线程组成。如何调度进程和线程，完全由操作系统决定，程序自己不能决定什么时候执行，执行多长时间。

多进程和多线程的程序涉及到同步、数据共享的问题，编写起来更复杂。

### 多进程

> todo:只是过了一遍，里面的代码没有自己敲，不过基本能看懂，后面还需要找时间详细了解。

在Unix/Linux下，可以使用`fork()`调用实现多进程。

要实现跨平台的多进程，可以使用`multiprocessing`模块。

进程间通信是通过`Queue`、`Pipes`等实现的。

### 多线程

多线程编程，模型复杂，容易发生冲突，必须用锁加以隔离，同时，又要小心死锁的发生。

Python解释器由于设计时有GIL全局锁，导致了多线程无法利用多核。多线程的并发在Python中就是一个美丽的梦。


### ThreadLocal

### 分布式进程
> todo:没看。

## 正则表达式
> todo:没看

## 常用内置模块

### `datetime`
`datetime`表示的时间需要时区信息才能确定一个特定的时间，否则只能视为本地时间。

如果要存储`datetime`，最佳方法是将其转换为`timestamp`再存储，因为`timestamp`的值与时区完全无关。

### `collections`

collections是Python内建的一个集合模块，提供了许多有用的集合类。

* `namedtuple`
* `deque`
* `defaultdict`
* `OrderedDict`
* `Counter`

### base64
Base64是一种用64个字符来表示任意二进制数据的方法。

### struct

> todo：大概过一遍，没仔细看

### hashlib

Python的`hashlib`提供了常见的摘要算法，如MD5，SHA1等等。

#### hmac

> todo:没仔细看

### itertools

> todo:没看

### contextlib

> todo:没看

### urllib

> todo:没看

### XML

> todo:没看

### HTMLParser

> todo:没看

## 常用第三方模块

> todo :没看

Pillow、requests、chardet

## virtualenv

> todo： 没看

virtualenv为应用提供了隔离的Python运行环境，解决了不同应用间多版本的冲突问题。

## 图形界面

Python支持多种图形界面的第三方库，包括：

* Tk
* wxWidgets
* Qt
* GTK
* ....

但是Python自带的库是支持Tk的Tkinter，使用Tkinter，无需安装任何包，就可以直接使用。

## 网络编程

由于你的电脑上可能不止浏览器，还有QQ、Skype、Dropbox、邮件客户端等，不同的程序连接的别的计算机也会不同，所以，更确切地说，网络通信是两台计算机上的两个进程之间的通信。比如，浏览器进程和新浪服务器上的某个Web服务进程在通信，而QQ进程是和腾讯的某个服务器上的某个进程在通信。

网络编程对所有开发语言都是一样的，Python也不例外。用Python进行网络编程，就是在Python程序本身这个进程内，连接别的服务器进程的通信端口进行通信。

### TCP/IP简介

### TCP编程

一个例子：
```py
# 服务器端：
# -*- coding: utf-8 -*-

import socket
import threading
import time

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.bind(('127.0.0.1',9988))

s.listen(5)
print('waiting fo connection....')

def tcplink(sock, addr):
    print('Accept new connection from %s:%s...' % addr)
    sock.send(b'Welcome!')
    while True:
        data = sock.recv(1024)
        time.sleep(1)
        if not data or data.decode('utf-8') == 'exit':
            break
        sock.send(('Hello, %s!' % data.decode('utf-8')).encode('utf-8'))
    sock.close()
    print('Connection from %s:%s closed.' % addr)

while True:
    # 接受客户端一个新连接
    sock,addr=s.accept()
    t = threading.Thread(target=tcplink, args=(sock, addr))
    t.start()
```
```py
# -*- coding: utf-8 -*-

import socket

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)

s.connect(('127.0.0.1',9988))

# 接收欢迎消息:
print(s.recv(1024).decode('utf-8'))
for data in [b'Michael', b'Tracy', b'Sarah']:
    # 发送数据:
    s.send(data)
    print(s.recv(1024).decode('utf-8'))
s.send(b'exit')
s.close()
```
运行结果：

### UDP编程