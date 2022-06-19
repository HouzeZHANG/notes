# C语言标准

- [C语言标准](#c语言标准)
- [第零章-学好C语言从会写指针开始](#第零章-学好c语言从会写指针开始)
- [第一章-导言](#第一章-导言)
  - [1.1 入门](#11-入门)
  - [1.2 变量与算数表达式](#12-变量与算数表达式)
    - [`while`语句](#while语句)
    - [标准化输入输出](#标准化输入输出)
    - [格式字符](#格式字符)
    - [除法](#除法)
    - [缩进](#缩进)
    - [数据类型的内存占用](#数据类型的内存占用)
    - [隐式转换](#隐式转换)
  - [1.3 `for`循环语句](#13-for循环语句)
  - [1.4 符号常量`#define`](#14-符号常量define)
  - [1.5 字符流与文本](#15-字符流与文本)
    - [关于bash终端](#关于bash终端)
    - [字符串常量](#字符串常量)
    - [字符常量](#字符常量)
    - [例程剖析：`getchar`与`putchar`实现文件复制](#例程剖析getchar与putchar实现文件复制)
    - [缓冲区](#缓冲区)
    - [全缓冲、行缓冲与不带缓冲](#全缓冲行缓冲与不带缓冲)
    - [`fflush()`清空缓冲区](#fflush清空缓冲区)
    - [C buffer - overflow](#c-buffer---overflow)
  - [连续赋值语句](#连续赋值语句)
  - [运算符优先级](#运算符优先级)
  - [1.7 函数](#17-函数)
    - [参数](#参数)
    - [原型](#原型)
    - [值传递](#值传递)
  - [1.9 字符数组](#19-字符数组)
  - [1.10 外部变量与作用域](#110-外部变量与作用域)
    - [`auto`自动变量](#auto自动变量)
    - [`extern`外部变量](#extern外部变量)
    - [过分依赖外部变量导致的问题](#过分依赖外部变量导致的问题)
    - [定义与声明的区别](#定义与声明的区别)
- [第二章 类型、运算符与表达式](#第二章-类型运算符与表达式)
  - [2.1 变量命名规则](#21-变量命名规则)
  - [2.2 基本数据类型](#22-基本数据类型)
  - [2.3常量](#23常量)
    - [枚举`enum`](#枚举enum)
  - [2.4声明](#24声明)
    - [初始化](#初始化)
  - [2.5算数运算符](#25算数运算符)
  - [2.6关系运算符](#26关系运算符)
  - [2.7类型转换](#27类型转换)
    - [类型转换规则](#类型转换规则)
    - [什么时候会发生类型转换？](#什么时候会发生类型转换)
    - [强制类型转换（一元运算符之一）](#强制类型转换一元运算符之一)
  - [2.8自增与自减运算符](#28自增与自减运算符)
  - [2.9位运算](#29位运算)
  - [2.10赋值运算符](#210赋值运算符)
  - [2.11条件表达式](#211条件表达式)
  - [2.12运算符优先级与求值次序](#212运算符优先级与求值次序)
- [第三章-控制流](#第三章-控制流)
  - [3.1语句与程序块](#31语句与程序块)
  - [3.2if-else语句](#32if-else语句)
  - [3.3else-if语句](#33else-if语句)
  - [3.4switch语句](#34switch语句)
  - [3.5while循环与for循环](#35while循环与for循环)
    - [逗号运算符](#逗号运算符)
  - [3.6 do-while循环](#36-do-while循环)
  - [3.7break与continue语句](#37break与continue语句)
- [第四章-函数与程序结构](#第四章-函数与程序结构)
  - [4.1函数的基本知识](#41函数的基本知识)
    - [最简单的函数](#最简单的函数)
    - [练习4-1 strrindex(s, t)](#练习4-1-strrindexs-t)
    - [函数原型和函数定义分别保存](#函数原型和函数定义分别保存)
    - [如果不写函数原型。。。](#如果不写函数原型)
    - [空参数表](#空参数表)
    - [返回值类型转换](#返回值类型转换)
    - [练习4-2 atof函数扩充](#练习4-2-atof函数扩充)
  - [4.3外部变量](#43外部变量)
    - [外部链接与外部变量](#外部链接与外部变量)
  - [4.4 作用域规则](#44-作用域规则)
  - [4.5 头文件](#45-头文件)
  - [4.6 静态变量](#46-静态变量)
  - [4.7 寄存器变量](#47-寄存器变量)
  - [4.8 程序块结构](#48-程序块结构)
  - [4.9 初始化](#49-初始化)
  - [4.10 递归](#410-递归)
    - [4.10.1 反序打印](#4101-反序打印)
    - [4.10.2 快排](#4102-快排)
    - [练习4-12](#练习4-12)
    - [练习4-13](#练习4-13)
  - [4.11 预处理器](#411-预处理器)
    - [4.11.1 文件包含#include](#4111-文件包含include)
    - [4.11.2 宏替换](#4112-宏替换)
    - [练习4-14](#练习4-14)
    - [4.11.3 条件包含](#4113-条件包含)
- [第五章-指针与数组](#第五章-指针与数组)
  - [5.1 指针与地址](#51-指针与地址)
  - [5.2 指针与函数参数](#52-指针与函数参数)
    - [补充：`getint`例子](#补充getint例子)
  - [5.3 指针与数组](#53-指针与数组)
  - [5.4 地址算术运算](#54-地址算术运算)
    - [指针之间的比较运算](#指针之间的比较运算)
  - [5.5 字符指针与函数](#55-字符指针与函数)
    - [研究：`strcpy`的不同实现](#研究strcpy的不同实现)
    - [研究：`strcmp`函数的实现](#研究strcmp函数的实现)
    - [`--`和`*`混合使用](#--和混合使用)
    - [练习5-3 用指针方式实现`strcat(s, t)`](#练习5-3-用指针方式实现strcats-t)
    - [练习5-4 编写函数`strend(s, t)`](#练习5-4-编写函数strends-t)
  - [5.6 指针数组](#56-指针数组)
    - [例程剖析：指针数组实现行排序](#例程剖析指针数组实现行排序)
    - [练习5-7 重写`readlines`](#练习5-7-重写readlines)
  - [5.7 多维数组](#57-多维数组)
    - [例程剖析：`day_of_year()`和`month_day()`](#例程剖析day_of_year和month_day)
  - [5.8 指针数组的初始化](#58-指针数组的初始化)
    - [例程剖析：`month_name`返回某月的字符串](#例程剖析month_name返回某月的字符串)
  - [5.9 二维数组VS指针数组](#59-二维数组vs指针数组)
  - [5.10 命令行参数`argc`和`argv`](#510-命令行参数argc和argv)
    - [例程剖析：实现`echo`](#例程剖析实现echo)
    - [例程剖析：实现`grep`](#例程剖析实现grep)
  - [5.11 函数指针](#511-函数指针)
    - [例程剖析：函数指针实现类型无关的`qsort`](#例程剖析函数指针实现类型无关的qsort)
  - [5.12 复杂声明](#512-复杂声明)
- [第六章-结构](#第六章-结构)
  - [6.1 结构的基本知识](#61-结构的基本知识)
  - [6.2 结构与函数](#62-结构与函数)
    - [例程剖析：使用`struct`对矩形进行操作](#例程剖析使用struct对矩形进行操作)
  - [6.3 结构数组](#63-结构数组)
    - [例程剖析：统计C语言关键字出现的次数](#例程剖析统计c语言关键字出现的次数)
  - [6.4 指向结构的指针](#64-指向结构的指针)
  - [6.7 类型定义`typedef`](#67-类型定义typedef)

未做但值得做的题目：
1. P25 C语言语法检查器
2. P28 编写程序确定类型变量的取值范围
3. [特想学编译原理](#43外部变量)
4. 练习5-1什么？
5. 练习5-2什么？

---

待解决的问题：
1. 库文件，源代码的链接步骤和方式
2. 浮点数，整数在计算机中是如何存储的？
3. [char转换为int会发生什么？](#27类型转换)
4. [为什么double双精度运算特别费时？](#类型转换规则)
5. [squeeze函数是否是库函数？](#27自增与自减运算符)
6. [bitcount](#210赋值运算符)
7. [对2做补码](#210赋值运算符)
8. [UNIX下grep函数的简单实现](#41函数的基本知识)


---
# 第零章-学好C语言从会写指针开始

这里记录了这本书中所有关于指针的奇技淫巧

>指针数组的连续打印//在指针数组中交换两位置的指针值
[`printf("%s\n", *lineptr++);`
`void swap(char *v[], int i, int j);`](#56-指针数组)

>指向长度为13的整型数组的指针
[`f(int (*daytab)[13]);`](#57-多维数组)
>声明一个长度为13的整型指针数组（注意辨析两者的差异）
`int *daytab[13]`

>argv先+1再取值
[`*++argv`](#510-命令行参数argc和argv)
[`printf((argc>1)?"%s ":"%s", *++argv);`](#510-命令行参数argc和argv)

>函数指针的运用
[`qsort((void **) lineptr, 0, nlines-1, (int (*)(void*, void*)) (numeric?numcmp:strcmp)));`](#511-函数指针)


# 第一章-导言

## 1.1 入门

略

## 1.2 变量与算数表达式

### `while`语句

进入`while`循环之前先检查条件是否满足

### 标准化输入输出

`scanf()`
`printf()`
这两个函数都**不是C语言的一部分**，但ANSI标准定义了他们  
对于符合标准的编译器和库，他们的行为是一致的。

### 格式字符

可以使用%xd来进行右对齐
`printf("%3d %6d\n", fahr, celsius);`

`%3.0f`
至少占3个字符宽，且不带小数点和小数部分
`%6.1f`
至少占6个字符宽，且小数点后面有1位数字

格式字符可以省略宽度与精度

| 符号 | 含义       |
| ---- | ---------- |
| `%o` | 八进制     |
| `%x` | 十六进制   |
| `%c` | 字符       |
| `%s` | 字符串     |
| `%%` | 百分号本身 |

| 符号  | 含义                     | 占用空间         |
| ----- | ------------------------ | ---------------- |
| `%ld` | 长整数                   | 32字节           |
| `%d`  | 整数                     | 16字节或者32字节 |
| `%f`  | 单精度浮点或者双精度浮点 | ？               |
| `%s`  | 字符串常量               | ？               |

### 除法

[整数除法会进行舍位，且具体取决于机器的实现](#25算数运算符)
与之相对应，**浮点数相除，无论操作数正负与否，都不会舍位**，所以如果明确想使用浮点数除法，可以显示地在整数后面加上小数点`celsius = 5.0*(fahr-32.0)/9.0;`这样就肯定是浮点数除法了

### 缩进

C编译器不关心缩进，但是正确的缩进和保留适当空格的程序设计风格十分重要

### 数据类型的内存占用

1. int 通常为16位，偶尔为32位
2. float通常为32位，至少有6位精度

结构，联合。。。

### 隐式转换

`fahr = lower;`
`while(fahr <= upper)`
这两个表达式，**算数运算符和逻辑运算符**两边的数据类型不一致。C语言在进行计算的时候会**将数据类型隐式转换为同类型数据**，Java类似

## 1.3 `for`循环语句

`for(fhar=0; fhar<=300; fhar=fhar+20)`
第二部分是循环的测试或者条件部分，for语句将对该条件求值，**如果为True，则执行循环体**（如果不满足要求，直接退出循环 ），随后执行第三部分

## 1.4 符号常量`#define`

`#define 名字 替换文本`
`define`将进行*文本替换操作*

替换文本不仅局限于数字，其可以是任意字符序列
`#define`指令行末尾没有分号

## 1.5 字符流与文本

>ANSI规定的文本流模型：

**文本流**是由多行字符构成的字符序列，每行字符由0个或者多个字符组成，**行末是一个换行符**，程序员不需要关心在程序之外这些行是如何表示的

### 关于bash终端

在bash终端下运行C语言程序，往往会给程序员带来困扰。

>我的问题是，在程序运行到`getchar()`等待用户输入的时候，我在终端输入了一串字符，随后按下`enter`，输入进缓冲区的字符是什么？

结论是会在行末加一个换行符

```bash
batman@LAPTOP-3KIH8KMK:/mnt/c/code/ANSIC_src/1/1.9$ ./a.out
kjsdf
kjsdf$ENTER$
askdf
askdf$ENTER$
```

>练习 1-17 编写一个程序，打印长度大于80 个字符的所有输入行。

这题要完美解决，需要创建二维数组以保存每一行

### 字符串常量

用双引号括起来的，以**空字符**结尾的字符数组，比如`"hello\n"`，其结尾还有一个`\0`

使用`printf("%s")`来打印字符串

### 字符常量

单引号括起来的字符，表示一个整型值，其对应在机器字符集中对应的数值，**小整数的一种写法**

### 例程剖析：`getchar`与`putchar`实现文件复制

`getchar()`返回输入流（文本流）中的下一个字符
`putchar(c)`打印一个字符变量

```c
int c;
c = getchar();
while(c != EOF){
	putchar(c);
	c = getchar();
}
```

>EOF
对于int来说，**EOF** (end of file char)类型的变量是存不下的。EOF在**stdio.h**头文件中被定义，他的大小并不重要，使用EOF确保程序不依赖特定的数值

>整型可以和字符常量混合运算
在统计数字出现个数的程序中，使用以下语句统计数字字符出现的个数
```c
int c;
a[c - '0']++;
```

>赋值可作为更大的表达式的一部分
`while((c=getchar()) != EOF)...`  
!=不等于的运算符优先级比赋值=运算符的优先级要高，所以要加括号
`c = getchar() != EOF;`等价于`c = (getchar() != EOF);`

### 缓冲区

**[CSDN论坛上关于缓冲区的论述](https://blog.csdn.net/qq_26768741/article/details/50933598#:~:text=fflush()%E5%87%BD%E6%95%B0%E5%86%B2%E6%B4%97%E6%B5%81,%E6%B8%85%E9%99%A4%E7%BC%93%E5%AD%98%E5%8C%BA%E7%9A%84%E6%96%87%E4%BB%B6%E3%80%82)**

在高速CPU与低速外部设备之间进行读写缓冲，提高CPU的工作效率

### 全缓冲、行缓冲与不带缓冲

| 缓冲类型 | 原理                                 | 适用范围         |
| -------- | ------------------------------------ | ---------------- |
| 全缓冲   | 填满标准IO缓存之后才进行实际IO操作   | 对磁盘文件的读写 |
| 行缓冲   | 当出现换行符的时候才进行实际的IO操作 | 标准输入输出     |
| 不带缓冲 | 直接显示                             | stderr标准出错   |

### `fflush()`清空缓冲区

`fflush()`刷新成功返回0，刷新失败返回EOF
`fflush(stdin)`
`fflush(stdout)`

### C buffer - overflow

缓冲区溢出 `char buffer[10];`

**[缓冲区溢出简介，以及黑客如何利用缓冲区攻击设计的不够合理的程序](https://www.thegeekstuff.com/2013/06/buffer-overflow/)**

A buffer is said to be overflown when the **data** (meant to be written into memory buffer) **gets written past the left or the right boundary of the buffer**. This way the **data** gets written to a portion of memory which does not belong to the program variable that references the buffer.  
简单讲，就是数据被写到buffer边界之外的时候，缓冲区溢出随即发生。危害：可能**导致关键内存区域被污染**

## 连续赋值语句

在兼有值与赋值的表达式中，执行顺序是从右到左的
`nl = nw = nc = 0;`
`nl = (nw = (nc = 0));` 

## 运算符优先级

`&&`比`||`仅仅高一个优先级，逻辑表达式**从左到右进行计算**

## 1.7 函数

1. **函数定义**可以以**任意次序**出现在一个源文件或者多个源文件中
2. 但**同一个函数**不能被拆分到多个文件中

### 参数

1. 参数列表中的变量称作**形式参数**  
2. 参数调用中和形式参数对应的值称作**实际参数**  
3. 主调函数可以忽略函数的返回值
4. 函数可以直接`return;`不加表达式  

### 原型

1. 函数原型中的**参数名是可选**的，甚至可以不同`int power(int, int);`
2. 但原型和函数的定义以及函数的调用**保持一致**

### 值传递

**C语言只有值传递**  
指针和数组指针例外

## 1.9 字符数组

略

## 1.10 外部变量与作用域

### `auto`自动变量

**局部变量**的别称，**在函数被调用时自动被创建，在返回时自动消失**，故称自动变量

### `extern`外部变量

`{ ... extern int max; ...}`
`int max;`

`extern`的注意事项：
1. 函数在使用外部变量之前，必须要知道外部变量的名字，使用`extern int a;`在函数体中重新声明（declaration）这个变量
2. `extern`关键字可以让**外部变量a**在**A文件中定义，在B文件C文件中使用**
3. 外部变量的定义（definition）只能在函数体外，且只能定义一次，定义的时候会给其分配存储单元
4. 习惯上将函数和变量的`extern`声明涵盖在头文件中

省略`extern`关键字的场合：
1. 外部变量在使用其的函数之前定义，函数体内就没有必要加`extern`关键字重新声明

### 过分依赖外部变量导致的问题

1. 模糊了数据之间的**依赖关系**
2. 失去了函数的**通用性**，函数的执行效果取决于外部变量而不是函数传入的参数

### 定义与声明的区别

定义：definition
[声明](#24声明)：declaration  

定义会给变量分配内存，而声明会描述变量的性质


# 第二章 类型、运算符与表达式

[第一章-格式字符](#格式字符)

1. 所有的整型变量都包括`signed`和`unsigned`两种
2. 字符串常量可以在编译的时候连接

## 2.1 变量命名规则

1. 下划线开头的是库例程，变量名不建议以下划线开头  
2. 变量名为小写，常量名全部大写

>对**内部名而言，至少前31个字符是有效的**，且区分大小写。函数名与外部变量名包含的字符数目可能小于31，这是因为汇编程序和加载程序可能会使用这些外部名，而语言本身是无法控制加载和汇编程序的。对于**外部名**，ANSI标准仅**保证前6个字符的唯一性，并且不区分大小写**

1. internal identifier
内部名指的是**只在某一文本中定义和使用的标识符**
2. external identifier
Ones **have to be visible outside the current source code file.**

## 2.2 基本数据类型

C语言四种基本数据类型：`short`,`long`,`float`,`double`。**具体实现依赖于平台**，这里不展开

`signed`,`unsigned`用于限定**char**和**整型**。`unsigned`遵循算数模2，不带限定符的char类型是否为正取决于编译器（参考CSAPP）

## 2.3常量

常量的声明

| 注脚             | 含义                                   |
| ---------------- | -------------------------------------- |
| u/U              | 无符号常量                             |
| l/L              | long                                   |
| ul/UL            | 无符号长整型                           |
| 没有后缀的浮点数 | double                                 |
| f                | float                                  |
| 0*               | 八进制                                 |
| 0x/0X            | 十六进制                               |
| ''               | 字符                                   |
| ""               | 字符串常量                             |
| \ooo             | 字节大小的位模式，ooo表示三个八进制位  |
| \xx              | 字节大小的位模式，xx表示两个十六进制位 |
| \0               | 空字符，值为0的字符                    |

**常量表达式**：只包含常量的表达式，只在编译时求值，运行时不求值。常量表达式可以出现在任何常量出现的地方

**字符串常量**：
1. 比如`"I am a string"`,`""`。字符串常量可以连接`"abnc" "Hello world!"`等价于`"abncHello world"`。串内部使用`\"`进行转义。字符串在内存中使用`\0`进行结尾。

2. `strlen()`返回字符串的长度，不包括结尾的空字符串，涵盖在string.h头文件中。  

3. **字符串常量**和**字符常量**，前者是一个字符型数组，后者是一个整数

### 枚举`enum`

常量整型值的列表

`enum boolean {NO, YES};`

默认第一个值为0，第二个值为1，以此类推，如果指定了部分枚举的值，则会将未指定的枚举名的值依照最后一个指定值向后递增  

不同枚举中的名字必须不同，同一枚举中的值可以相同

## 2.4声明

变量**先声明再使用**

### 初始化

1. 初始化表达式`int a=1;`
2. 如果变量不是自动变量，则只能进行一次初始化操作
3. 非自动变量的初始化表达式必须为常量表达式，而自动变量的初始化表达式可以是任何表达式
4. 每次进入函数的时候，都会对自动变量进行初始化
5. **外部变量与静态变量的初始化值为0，自动变量的初始化值为无效值**

**const关键字**
1. 变量声明的时候使用const
任何变量的声明都可以使用const限定符修饰，指定变量的值不能被修改
`const char msg[] = "warning: ";`
该数组内所有元素的值都不能被修改
2. 在函数参数表中使用const
`int strlen(const char[]);`
表明函数内部无权修改该数组

```bash
#gcc const_test.c
const_test.c: In function ‘main’:
const_test.c:3:7: error: assignment of read-only variable ‘a’
    3 |     a = 2;
      |       ^
```

## 2.5算数运算符

1. 五种算数运算符 +-*/%
2. 取模不能用于浮点数（float, double）
在有**负操作数**的情况下，**整数除法**和**取模**的结果的符号取决于机器的实现

## 2.6关系运算符

关系运算符的优先级比相等性运算符高

关系运算符优先级比算术运算符低

&& || 是一组
== != 是一组
&& || 优先级比 ==!=低

== != 优先级比赋值运算符高
`i<lim - 1 && (c=getchar()) != '\n' && c != EOF`

关系运算符表达式为真，为1；若为假，为0

`!`非运算符将非0转化为0，将0转化为1
判断某一变量的值是否为0的时候，往往使用`if(!vali)`而不是`if(vali == 0)`

## 2.7类型转换

`ctype.h`

当把char类型的值转换为整型的时候，可能为正数也可能为负数，所以[最好指定signed/unsigned限定符](#22基本数据类型)以确保程序的可移植性

反之，如果将较长的整数转化为较短的整数，信息也有可能会丢失

`int i;`
`char c;`
`i = c;`
`c = i;`

此时c的信息一定不会丢失，但如果颠倒赋值语句的顺序，i可能会丢失信息

### 类型转换规则

1. 不为long,double的转换为long,double
2. 如果一个为double，另一个也转换成double
3. float同理
4. char，short转换为int（自动）
5. 一个为long，另一个也转化成long

float不会主动转化为double，一来为了**节约时间**，二来为了**节约内存**

### 什么时候会发生类型转换？

赋值运算的时候往往也需要进行类型转换，赋值运算**右边**的类型转换为**左边**的类型

[函数传参的时候也会发生类型转换，函数原型中如果有声明参数类型，会在函数调用的时候自动进行强制类型转换](#4函数与程序结构)

### 强制类型转换（一元运算符之一）

`(type_name) expr;`
`sqrt((double) n);`

强制类型转换不会改变expr本身的值

## 2.8自增与自减运算符

既可以用作前缀运算符，也可以用作后缀运算符

`++n;`
先将n的值加1，再使用n

`n++;`
先使用n的值，再将n的值加1

自增自减运算符只能用于变量，**表达式禁止使用**
`(n+1)++l`

## 2.9位运算

6种位运算，且**只能运用于整型**
带符号或者无符号的char，int，short，long

| 符号 | 功能                         |
| ---- | ---------------------------- |
| &    | AND                          |
| \|   | OR                           |
| ^    | XOR                          |
| <<   | 左移                         |
| >>   | 右移（右操作数的值必须非负） |
| ~    | 求反                         |

## 2.10赋值运算符

`op=`针对的是二元运算符，取反不支持此语法

`expr1 op= expr2;`
等价于
`expr1 = (expr1) op (expr2);`
在还原的时候，自动加上括号

`x *= y + 1;`
等价于
`x = x * (y + 1);`

[同样地，赋值运算符自己也会返回一个值](#字符流与文本)
返回的类型是左边的变量的类型，值是赋值之后的类型（潜台词是有可能数据会做类型转换）

赋值运算符有助于编译器产生高效的程序

## 2.11条件表达式

`expr1 ? expr2 : expr3`
expr1不等于0即返回expr2，否则返回expr3

## 2.12运算符优先级与求值次序

位运算符的优先级比运算符`==，!=`低，所以在做条件判断的时候，需要将位运算括起来

C语言**没有指定**同一运算符中不同操作数的运算次序。`x = f() + g()`。如果f函数和g函数都是用了同一个全局变量，就要小心了！

C语言同样没有指定各个函数参数的求值顺序！`printf("...", ++n, power(2, n));`这么写在不同的编译器上会有不同的表现。`a[i] = i++;`不是好的实现。

# 第三章-控制流

## 3.1语句与程序块

在表达式之后加上`;`就变成了**语句**

在`{}`之间的语句与声明构成**复合语句（程序块）**

## 3.2if-else语句

事实上if语句只会判断数值是否为0，所以可以大肆简化判断条件
`if(expr)`代替`if(expr != 0)`

else在没有限制的情况下会**匹配最近的一条if语句**，需要注意的是，编译器并不会获取缩进信息

## 3.3else-if语句

`if-else if ...else`
最后的else语句可以不加，最后的else语句视为对例外情况进行处理

## 3.4switch语句

`switch(表达式){`
`case 常量表达式:语句`
`case 常量表达式:语句`
`case 常量表达式:语句`
`case 常量表达式:语句`
`...`
`}`

case的作用只是一个**标号**，某个分支中的代码执行完毕之后，程序将进入下一个分支继续执行。常用的退出方法是使用**break&return**

良好的编程风格是在default语句之后再加break

## 3.5while循环与for循环
**在循环体执行之前**，对循环条件做判断的两个循环语句

while循环和for循环在大多数情形下是等价的
`for(expr1;expr2;expr3)`
`...`
等价于
`expr1`
`while(exp2)`
`...`
`expr3`

for语句省略`expr1`，`expr3`则退化成`while`语句，省略`expr2`则表示永远运行

### 逗号运算符

逗号分隔符`,`在`for`循环语句中可以实现同时多个语句一起执行`for(i=0, j=...;...;i++,j--)`

并不是所有的逗号都是逗号运算符，比如声明语句，比如函数参数，在这两种情况下，不能保证从左到右运行

`for(i=0, j=strlen(s)-1; i<j; i++, j--)`
`c=s[i], s[i]=s[j], s[j]=c`

## 3.6 do-while循环
**在循环体执行之后**对循环条件做判断的循环语句

## 3.7break与continue语句

`continue`语句使`for`,`while`,`do-while`语句立即开始下一次循环，对于`for`语句，会直接更新循环变量，`while`和`do-while`则直接判定循环条件

说了等于没说哈哈

# 第四章-函数与程序结构

如果参数声明得当，程序可以自动进行适当的强制类型转换

每个外部对象只能有一个定义

自动数组与结构都可以初始化

## 4.1函数的基本知识

利用C语言实现模式匹配
`strstr`库函数

[初始化](#49-初始化)模式：
`char pattern[] = "ould";`

C语言实现grep
```c
//pattern
char pattern[] = "ould";
int strindex(char source[], char searchfor[]);
int strindex(char s[], char t[]){
    //返回字符串t在字符串s出现的起始位置，当不包含t的时候，返回-1
    int i, j, k;
    for(i=0; s[i]!='\0'; i++){
        for(j=i, k=0; t[k]!='\0' && s[j] == t[k]; j++, k++)
            ;
        //k_index指向t数组，j_index指向s数组
        if(t[k] == '\0'){
            return i;
        }
    }
    return -1;
}
```

### 最简单的函数

`dummy() {}`
如果函数中省略了返回值类型，则**默认为返回int**

函数在源文件中的**顺序可以是任意的**
`return (expr);`

函数的返回语句如果是一个表达式，**习惯添加括号**  

在模式匹配这个例子中，main函数返回了`found`参数，调用这个**程序**的环境可以使用这个值

```c
main(){
  ...
  return found;
}
```

在UNIX环境下，`cc`指令先生成`.o`文件，再将`.o`文件加载到可执行文件`a.out`中

1. 一个外部变量只能有一个定义
2. 函数在源文件中出现的次序可以是任意的，但同一个函数不能被分离到多个文件中
3. 调用函数可以忽略返回值

### 练习4-1 strrindex(s, t)

编写函数strrindex(s, t)返回字符串t在s中出现的最右边的位置，如果不存在，返回-1

```c
int strrindex(char s[], char t[]){
    int j, k;
    for(int i = 0; s[i] != '\0'; i++){
        for (j = i, k = 0; s[j] == t[k] && t[k] != '\0';j++, k++){
            ;
        }
        if(t[k] == '\0'){
            return s[j] == '\0'? j-2:j-1;
        }
    }
    return -1;
}
```

函数声明语句**可以和变量声明放在一起**
`double sum, atof(char []);`

### 函数原型和函数定义分别保存

>若函数声明和函数定义放在一个源文件中，编译器会主动检查类型是否匹配，但如果定义和声明放在不同源文件中，编译器无法检测（因为分别编译！）

### 如果不写函数原型。。。

如果在使用一个函数之前，**没有函数原型**，则函数将在第一次出现的**表达式**中**隐式声明**。这会导致函数的返回值被自动设定为int
`sum += atof(line)`

### 空参数表

此外，使用空参数表进行函数声明`double atof()`在**语法上是正确的**，新版编译器允许这么操作的原因是为了向后兼容，但这么做会让编译器**对函数参数表不做任何假设**，会关闭所有的参数检查，所以如果想声明空参数的函数，尽量使用`void`关键字

### 返回值类型转换

在函数传参返回的时候，如果使用隐式类型转换，可能会丢失信息，有些编译器会给警告信息。建议在return返回之前使用强制类型转换

### 练习4-2 atof函数扩充

略

## 4.3外部变量

`external` & `internal`是一对相对的词

C语言不允许在函数内部定义函数，故函数是外部的，于是internal用于描述定义在**函数内部**的**函数参数**和**变量**

### 外部链接与外部变量

通过同一个名字**对外部变量的引用**（即使这些引用来自于单独编译的不同函数），也都**引用同一个对象**

外部变量的生命周期最长？

作者举了一个逆波兰表达式的例子，栈这一个数据结构作为外部变量供全部函数访问。

`push(pop() - pop())`错误写法，因为无法确认哪个pop()调用先执行

## 4.4 作用域规则

1. 函数与外部变量可以分开编译
2. 一个程序可以放在几个文件中
3. 原先已经编译过的函数可以从库中加载（库函数？）

几个问题：
1. 如何进行声明才能确保变量在编译的时候正确声明？
2. 如何安排声明的位置才能确保程序在加载的时候各部分正确连接？
3. 如何组织程序中的声明才能确保只有一份副本？
4. 如何初始化外部变量？

**作用域**：程序中可以使用该名字的部分
1. 各个函数中声明的具有相同名字的各个局部变量之间没有任何关系，**函数的参数看作是局部变量**
2. 外部变量或者函数的作用域从声明它的地方开始，到其所在的（待编译的）文件的末尾结束

```c
#include<stdio.h>

int a = 10;
int main(void){
    printf("%d", a);
    return 0;
}
```
允许将a这个外部变量在main函数之前**定义**，随后在main函数中调用，但如果在main函数之后定义a这个外部变量，必须在main函数中使用extern关键字重新声明（变量的定义和使用在不同的文件中也要重新用extern声明）

```c
#include<stdio.h>

int main(void){
    extern int a;
    printf("%d", a);
    return 0;
}

int a = 10;
```

变量的**声明**用于说明变量的属性（尤其是他的类型）
变量的**定义**促使**存储器内存的分配**

试比较：
```c
int sp;
double val[MAXVAL];
```

```c
extern int sp;
extern double val[];
```
前者是**定义+声明**，在该文件剩余的地方都可以直接使用sp和val（当然这两句话写在所有函数的外部）
后者**只是声明**，可以看见val数组的长度甚至都不需要给出（它的长度在被定义的时候给出），这两句声明语句不会建立变量或者为他们分配存储单元。在该文件中，这两句声明之后，就可以使用这两个外部变量了
外部变量的初始化只能出现在定义中（言下之意不能在声明中初始化）

## 4.5 头文件

**calc.h**
```c
#define NUMBER '0'
void push(double);
double pop(void);
int getop(char []);
int getch(void);
void ungetch(int);
```

**main.c**
```c
#include<stdio.h>
#include<stdlib.h>
#include"calc.h"
#define MAXOP 100

main(void){
  ...
}
```

**getop.c**
```c
//头文件中不建议添加标准库
#include<stdio.h>
#include<ctype.h>
#include"calc.h"

getop(){
  ...
}
```

**stack.c**
```c
#include<stdio.h>
#include"calc.h"
#define MAXVAL 100

//外部变量定义
int sp = 0;
double val[MAXVAL];
void push(double){
  ...
}
double pop(void){
  ...
}
```

**getch.c**
```c
#include<stdio.h>

//外部变量的声明
#define BUFSIZE 100
char buf[BUFSIZE];
int bufp = 0;

int getch(void) {
  ...
}

void ungetch(int){
  ...
}
```

>自己的项目头文件中，往往是宏定义+函数签名的组合。中等规模的程序最好只用一个头文件来共享对象，较大的程序使用更多的头文件，需要组织他们。

## 4.6 静态变量

1. `static`是声明的一种方式
2. `static`主要用于限制**外部变量**的访问权限，让其作用域只限于该源文件的**后半部分**（在`static`声明之前用`extern`重新声明该变量，会报错：Static declaration of 'a' follows non-static declaration）就算是同文件，也不行！
3. `static`也可以用来**修饰函数**。一般来说函数名字**全局可见**。
4. `static`也可以用来声明**内部变量**（函数体中声明），和自动变量一样都无法从外部访问，但其一直占据内存，不管函数是否被调用，它一直存在，其**初始化时间是在第一次进入函数内部的时候**

**getch.c**
```c
#include<stdio.h>

#define BUFSIZE 100
char buf[BUFSIZE];
int bufp = 0;

int getch(void) {
  ...
}

void ungetch(int){
  ...
}
```
观察该文件，`getch`和`ungetch`共享`bufp`和`buf`，所以使用外部变量进行声明，但是这两个对象不该被`getch`和`ungetch`的**调用者**所访问，在这种情况下，使用`static`关键字将很好地对**外部变量的访问权限**进行隔离，该程序其他文件中可以使用与其同名的变量而不冲突

**getch.c**
```c
#include<stdio.h>

#define BUFSIZE 100
static char buf[BUFSIZE];
static int bufp = 0;
int getch(void) {
  ...
}

void ungetch(int){
  ...
}
```

## 4.7 寄存器变量

1. `register`声明，将程序占用内存空间更小，编译器将倾向于将该变量放在寄存器中
2. 只适用于**自动变量**和**函数参数**
3. 可以选择声明过量的寄存器变量，编译器最终只会选择很小一部分的变量放进寄存器，取决于机器实现
4. 寄存器变量的**地址无法访问**（无论其是否被存放在寄存器中）

```c
register int x;
register char c;

f(register unsigned m, register long n)
{
  register int i;
  ...
}
```

## 4.8 程序块结构

1. 在函数中以程序块的形式定义变量
2. 变量的声明可以跟在（函数开始的花括号后||其他标识复合语句开始的左花括号后）

```c
if(n>0){
  int i;
  for(i=0;i<n;i++){
    ...
  }
}
```

3. 自动变量（包括形式参数）可以隐藏同名的外部变量与函数

```c
int x;
int y;

f(double x){
  double y;
}
```
在`f`内部，`x`和`y`都是`double`且和外部的同名变量无关（这不是一个好的程序设计）

## 4.9 初始化

1. 不进行显示初始化的时候，外部变量和静态变量为0，自动变量和寄存器变量为未知
2. 外部变量和静态变量的初始化必须是**常量表达式**，且**只初始化一次**（程序开始执行之前就已经初始化完毕）
3. 自动变量和寄存器变量在每次进入函数的时候都将初始化，可以为任意表达式，以下两种声明都允许
```c
int binsearch(int x, int v[], int n){
  int low, high, mid;

  low = 0;
  high = n - 1;
  ...
}

int binsearch(int x, int v[], int n){
  int low = 0;
  int high = n - 1;
  int mid;
  ...
}
```
4. 数组的初始化，数组长度可以省略

```c
int days[] = {31, 28, 31, 30, 31, 30, 31, 31, 30, ...};
```

如果初始化元素的个数比数组长度小，对于外部变量，静态变量和自动变量来说，没有初始化的元素将自动赋值为0，（和外部变量默认为0保持一致）
```c
char pattern[] = "ould";
char pattern[] = {'o', 'u', 'l', 'd', '\0'};
```
字符数组的初始化有两种方法，效果相同

## 4.10 递归

### 4.10.1 反序打印
```c
#include<stdio.h>
//打印十进制数n，这里编写的函数无法处理最大的负数，为什么？
void printd(int n){
  if (n<0){
    putchar('-');
    n = -n;
  }
  if (n/10){
    printd(n/10);
  }
  putchar(n%10 + '0');
}
```
函数在进行递归调用的时候，每次都会得到一个与以前的自动变量集合不同的新的自动变量集合

### 4.10.2 快排
对于给定的数组，将集合中的元素分为两个子集，其一全部小于该元素，其二全部大于或者等于该元素，再对这两个子集分别执行该过程，直到子集元素小于2
标准库中提供了qsort函数，适用于任何对象类型

```c
void qsort(int arr[], int l, int r){
  if (r - l + 1 < 2){
    return;
  }

  //将划分元素和第一个元素交换
  swap(v, l, l+((r - l)>>1));

  last = l;
  //i指针始终指向比较元素，该for循环的意义在于遍历比较[1,:]位置的全部元素
  for(i = left + 1; i<= right; i++)
    if(v[i] < v[left])
      //last始终指针指向比target小的元素的尾巴（这也是为什么使用++last的原因）
      //在循环结束之后，交换l和target位置的元素，完成荷兰国旗
      swap(v, ++last, i);
  swap(v, left, last);
  
  //交换完成之后，last指向target
  qsort(v, left, last-1);
  qsort(v, last+1, right);
}

void swap(int arr[], int i, int j){
  int temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
```

递归并不节省存储器开销

### 练习4-12

### 练习4-13

## 4.11 预处理器

预处理是编译过程中执行的第一个步骤
```c
//两个常用的预处理指令
//---
//用任意字符序列替换一个标记
#define
//用于在编译阶段将指定文件的内容包含进当前文件
#include
```

### 4.11.1 文件包含#include

```c
//在源文件位置查找
#include ""
//如果源文件目录没有找到，或者使用尖括号括起来，则按照具体实现
#include <>
```

在大程序中如果某个包含文件中的内容发生了变化，则所有依赖该包含文件的源文件都必须重新编译

### 4.11.2 宏替换

```c
#define 名字 替换文本
```
1. 后续所有出现名字记号的地方都会被替换成替换文本，通常情况下`#define ...`自成一行，替换文本为`#define`**指令的尾部剩余的所有部分**，替换文本可以是任意字符串  

2. 如果想要换行，使用`\`来换行

3. 宏替换对括在引号中的字符串不起作用。`YES`被宏定义之后，`printf("YES");`不会起作用
4. 宏定义的作用范围从当前定义点开始，一直到源文件的结束
5. **带参数的宏定义**：`#define max(A, B) ((A) > (B) ? (A):(B))`

语句`x = max(p+q, r+s)`将被替换成`x = ((p+q) > (r+s)?(p+q):(r+s));`

缺点1：作为参数的表达式被重复计算两次，如果表达式有副作用，比如含有自增自减运算，则会出现不正确的情况，比如：
`max(i++, j++)`

缺点2：计算次序`#define square(x) x * x`定义后，如果调用`square(z+1)`，结果错误

适当地使用宏定义将**减少函数调用的开销**

`getchar`等字符串处理函数就是用宏定义实现的，这样会减少函数调用的开销，如果想取消宏定义，可以使用`#undef getchar`

形式参数不能用带引号的字符串替换，但却可以使用`#`来使用字符串连接运算，下面是一个调试打印宏的应用：
`#define dprint(expr) printf(#expr "=%g\n", expr)`

`##`宏运算符：略
`#define paste(front, back) front ## back`

### 练习4-14
定义宏swap(t, x, y)以交换t类型的两个参数
`#define swap(t, x, y) {t temp = x; x = y; y = temp;}`

### 4.11.3 条件包含

使用条件语句对预处理本身进行控制，其值在预处理阶段进行计算

```c
#if 常量整型表达式
//若不等于0，包含其后的各行，直到#endif，#elif，#else语句为止
#endif
```

下面这个函数和`#if`一起使用
```c
defined(name)
```
为了保证hdr.h头文件的内容只被`#include`一次，可以这么写：
```c
#if !defined(HDR)
#define HDR
//hdr.h的头文件内容被放在这里
#endif
```
下面是Clion自动生成的条件包含文本：
```c
#ifndef CTEST_ABC_H
#define CTEST_ABC_H
...
#endif //CTEST_ABC_H
```
```c
#ifndef如果没有！
#ifdef如果有！
```

# 第五章-指针与数组

指针：保存变量地址的变量

C语言的指针能让程序员写出非常紧凑与高效的代码

ANSI C之前，使用`char *`来作为通用类型指针，在ANSI C及之后，使用`void *`作为通用类型指针，其可以存放指向任何数据类型的指针（`void *`的前身是`char *`）

## 5.1 指针与地址

指针是能够存放地址的一组存储单元

一元运算符`&`取一个变量的地址`p = &c;`将c变量的地址给p，地址运算符**只能运用于存储在内存中的变量**，**无法作用于表达式，常量或者register类型的变量**

一元运算符`*`是间接寻址或间接引用运算符，当其作用于指针的时候，将访问指针所指向的对象

```c
int x = 1, y = 2, z[10];

//表达式*ip的结果是int类型，这么写方便记忆
int *ip;

ip = &x;
y = *ip;
*ip = 0;
ip = &z[0];

//atof的参数是一个指向char类型变量的指针
double atof(char *);
```

如果`ip`指针指向`x`，那么在x可以出现的任何上下文中都可用`*ip`来指代`x`

```c
*ip = *ip + 1;
y = *ip + 1;
*ip += 1;

//遵循从右至左的结合顺序，右结合
++*ip;
(*ip)++;
```

## 5.2 指针与函数参数

C语言函数传参使用[值传递](#值传递)，若要在函数中修改主调函数中的值，只能使用指针
```c
//swap函数的指针实现
void swap(int *a, int *b){
    int temp = *a;
    *a = *b;
    *b = temp;
}

//函数调用
swap(&int_a, &int_b);
```
### 补充：`getint`例子

`getint`接受自由格式的输入，将输入的字符流分解成整数，每次调用得到一个整数，返回得到的整数，到达输入结尾的时候返回`EOF`

```c
#include<stdio.h>

int getch(void);
void ungetch(int);

//将输入中的下一个整型赋值给*pn
int getint(int *pn)
{
    int c, sign;

    while(isspace(c=getch()))
        ;
    if(!isdigit(c) && c!=EOF && c!='+' && c!='-'){
        ungetch(c);
        return 0;
    }
}

```

## 5.3 指针与数组

一般来说用指针编写的程序速度比用数组下标编写的要快

如果pa指向数组中的某个特定元素，根据指针运算的定义，`pa+k`将指向下`k`个元素
```c
pa = &a[0];
int res = *(pa+1);

//下面这两个表达式效果相同
a[i];
*(a+i);
```

数组名所代表的就是该数组最开始的第一个元素的地址
```c
//下面两句话效果相等
pa = &a[0];
pa = a;
```

如果`pa`是一个指针，`pa[k]`与`*(pa+k)`是等价的

指针和数组名之间的区别：**指针是一个变量，而数组名不是**，指针可以自增自减，可以被赋值，但是数组名不可

```c
strlen(char *);
int strlen(char *arr){
    int i;
    for(i=0;*(arr+i)!='\0';i++)
        ;
    return i;
}

int main(void){
    char my_arr[] = "my love!";
    int len = strlen(my_arr);
    ...

    return 0;
}
```

需要注意，虽然函数参数传入的是数组名，但是函数将自动创建指针变量，执行该函数并不会影响`main`函数中的`my_arr`字符串

```c
//参数表中以下两种语法等价
char a[]
char *a
```

可以给函数传递数组的子数组，函数不关心传入的数组是不是只是某数组的一部分`f(&a[2])`，甚至可以用数组头引用头元素之前的元素`f(&a[-1])`

## 5.4 地址算术运算

C语言将指针，数组和地址的算术运算集成在一起

```c
//最大栈空间
#define MAX_LEN_STACK 10000

//指向下一个空闲存储单元的指针
static char *allocp;

//大字符数组作为栈空间
static char allocbuf[MAX_LEN_STACK];
allocp = allocbuf;

char *alloc(int n);
char *alloc(int n){
    if(allocp - allocbuf + n <= MAX_LEN_STACK){
        //存储空间足够
        allocp += n;
        return allocp - n;
    }
    else{
        return 0;
    }
}

void afree(char *p);
void afree(char *p){
    //释放p指向的存储区域
    if (p>=allocbuf && p < allocbuf + MAX_LEN_STACK)
        allocp = p;
}
```

C语言保证0永远不是有效的地址，但**0可以赋值给指针**，用以表示异常。整数和指针之间永远不可以互相转换，但0是唯一例外的；常量0可以赋值给指针，指针也可以和0进行比较，**程序中经常使用`NULL`来代替常量0。**
```c
int main(void){
    printf("%d", 0 == NULL);
    return 0;
}
```
返回1

### 指针之间的比较运算

我们知道指针一般不能和整数比较，但是指针之间可以比较

```c
if (p >= allocbuf && p < allocbuf + MAX_LEN_STACK)
```
1. 如果两个指针都指向同一个数组，那么就可以比较
2. 如果指向不同的数组，那么比较没有定义
3. 和0，NULL进行相等或不相等的比较是有意义的

如果`p`是一个指针，`p+n`到底向后移动了几个存储单元取决于`p`指针的类型，所有指针运算都会**自动考虑它所指向的对象的长度**

```c
int strlen(char *s){
    char *p = s;
    while(*p != '\0'){
        p++;
    }
    return p - s;
}
```

两指针之间的加法、乘法、除法、移位或者屏蔽运算都是非法的；指针同浮点数之间的运算；将不同类型的指针做赋值运算（其中一个是`void *`的情况除外）

## 5.5 字符指针与函数

1. 作为函数参数
字符串常量最常见的用法或许是作为函数参数`printf("hello, world!\n");`。我们的`printf()`函数接受的是字符串的第一个**字符**的指针，这是一般的字符串常量访问方法
2. 用字符指针存储字符串常量
```c
char *pmessage;
pmessage = "now is the time";

//创建一个数组
char amessage[] = "now is the time";
//创建一个字符型指针，指向一片内存（pmessage可以指向其他内存）
char *pmessage = "now is the time";

//前者可以修改字符串的内容，修改后者字符串的内容没有意义，修改完之后printf不出来了，蛮怪的
*(pmessage+1) = 'f';
for(int i = 0; *(pmessage+i)!='\0';i++){
    //啥都没有
    printf("%c", *(pmessage+i));
}
```

### 研究：`strcpy`的不同实现
`strcpy(s, t)`将`t`指向的字符串拷贝到`s`指针处
```c
//数组下标实现
void strcpy(char *s, char *t){
    int i = 0;
    while((s[i] = t[i])!='\0'){
        i++;
    }
}

//指针实现，得益于C语言的值传递，我们在函数中可以肆意使用s和t而不用担心对主调函数中s和t的影响
void strcpy(char *s, char *t){
    while((*s=*t)!='\0'){
        s++;
        t++;
    }
}

//经验丰富的程序员
void strcpy(char *s, char *t){
    //表达式*t++的值是执行自增运算之前t所指向的字符
    while((*s++ = *t++) != '\0')
        ;
}

void strcpy(char *s, char *t){
    //printf("%d", '\0' == 0); 显示为1，空字符值=0
    while(*s++ = *t++)
        ;
}
```

### 研究：`strcmp`函数的实现

该函数比较字符串`s`和`t`，根据`s`按照字典顺序小于、等于或者大于`t`的结果分别返回负整数，0或正整数，该返回值是逐字符比较之后`s[j]-t[j]`的差

```c
int strcmp(char *s, char *t){
    int i;
    for(i=0;s[i] == t[i];i++){
        if(s[i] == '\0'){
            return 0;
        }
    }
    return s[i] - j[i];
}

int strcmp(char *s, char *t){
    for(;*s == *t;s++, t++){
        if(*s == '\0'){
            return 0;
        }
    }
    return *s - *t;
}
```

### `--`和`*`混合使用

压栈`*p++=val;`事实上这俩是同级别优先级的运算符
出栈`val=*--p;`

### 练习5-3 用指针方式实现`strcat(s, t)`

将`t`指向的字符串复制到`s`指向的字符串的尾部

```c
void strcat(char *s, char *t){
    while(*s!='\0'){
        s++;
    }
    for(;*t!='\0';s++, t++){
        *s = *t;
    }
    *s = '\0';
}
```

### 练习5-4 编写函数`strend(s, t)`

如果t出现在s的尾部，返回1， 否则返回0

```c
int strend(char *s, char *t){
    char *h1 = s;
    char *h2 = t;
    while(*s!='\0'){
        s++;
    }
    while(*t!='\0'){
        t++;
    }
    for(; *s==*t && s>=h1 && t >= h2; s--, t--){
        ;
    }
    if(t<h2 || s<h1){
        return 1;
    }
    return 0;
}
```

## 5.6 指针数组

### 例程剖析：指针数组实现行排序

用指针数组实现不同长度字符串的排序问题

在分析该问题时，最好将问题划分为不同部分，**分而治之**

```c
#include<stdio.h>
#include<string.h>

//规定最大行数
#define MAXLINES 5000
//指向文本行的指针数组
char *lineptr[MAXLINES];
//规定每个输入行的最大字符数
#define MAXLEN 1000

//返回文本的行数int，如果超行，返回-1
int readlines(char *lineptr[], int nlines);
//打印各个字符串的函数
void writelines(char *lineptr[], int nlines);
//对指针数组进行排序
void qsort(char *lineptr[], int left, int right);

int main(){
    //文本的行数
    int nlines;

    if((nlines = readlines(lineptr, MAXLIENS))>=0){
        qsort(lineptr, 0, nlines-1);
        writelines(lineptr, nlines);
        return 0;
    }
    else{
        printf("error : input too big to sort\n");
        return 1;
    }
}

int getline(char *, int);
char *alloc(int);

//readlines:读取输入行
int readlines(char *lineptr[], int maxlines){
    int len, nlines;
    //用于临时存放最大单行字符数的数组line
    char *p, line[MAXLEN];

    nlines = 0
    while((len = getline(line, MAXLEN))>0){
        if(nlines >= maxlines || (p=alloc(len)) == NULL){
            //当alloc分配不出内存 或者超过最大行数的时候返回 -1
            return -1;
        }
        else{
            //将换行符替换为空字符
            line[line-1] = '\0';
            strcpy(p, line);
            //将copy出来的p指针给lineptr指针数组
            lineptr[nline++] = p;
        }
    }
    return nlines;
}

void writelines(char *lineptr[], int nlines){
    int i;
    for(i=0;i<nlines;i++){
        printf("%s\n", lineptr[i]);
    }
}
```
**重要概念：指针数组**
```c
//指向文本行的指针数组
char *lineptr[MAXLINES];
```
**writelines用指针数组的另一种写法**
```c
void writelines(char *lineptr[], int nlines){
    int i;
    while(nlines-- >0){
        printf("%s\n", *lineptr++);
    }
}
```
**对快排的一些小改动。。。以满足行排序**
```c
void swap(char *v[], int i, int j);

void qsort(char *v[], int left, int right){
    //为什么这里swap函数要在qsort里做签名？
    void swap(char *v[], int i, int j);

    if(left >= right){
        return;
    }
    swap(v, left, (right+left)/2);
    last = left;
    for(i=left+1;i<=right;i++){
        if(strcmp(v[i], v[left])<0){
            swap(v, ++last, i);
        }
    }
    swap(v, left, last);
    qsort(v, left, last-1);
    qsort(v, last+1, right);
}

void swap(char *v[], int i, int j){
    //需要将swap函数修改成交换char指针
    char *temp;
    temp = v[i];
    v[i] = v[j];
    v[j] = temp;
}
```

### 练习5-7 重写`readlines`
```c
int readlines(char *lineptr[], int maxlines){
    int len, nlines;
    //用于临时存放最大单行字符数的数组line
    char *p, line[MAXLEN];

    nlines = 0
    while((len = getline(line, MAXLEN))>0){
        if(nlines >= maxlines || (p=alloc(len)) == NULL){
            //当alloc分配不出内存 或者超过最大行数的时候返回 -1
            return -1;
        }
        else{
            //将换行符替换为空字符
            line[line-1] = '\0';
            strcpy(p, line);
            //将copy出来的p指针给lineptr指针数组
            lineptr[nline++] = p;
        }
    }
    return nlines;
}
```

## 5.7 多维数组

### 例程剖析：`day_of_year()`和`month_day()`

`month_day()`将某一年的第一天转换成相应的日和月，需要返回两个值，所以使用指针参数

为了简化函数的实现，将每月有多少天记录在数组（矩阵）中
```c
//二维数组的初始化
static char daytab[2][13] = {
    {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
    {0, 31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}
}

int day_of_year(int year, int month, int day){
    int i, leap;
    //判断闰年的公式
    leap = year%4 == 0 && year%100 !=0 || year%400 == 0;
    for(i=0;i<month; i++){
        //精彩。。直接在day这个临时变量上加
        //逻辑表达式的值只可能是0或1，所以可以用来当作下标
        day += daytab[leap][i];
    }
    return day;
}

void month_day(int year, int yearday, int *pmonth, int *pday){
    int i, leap;
    leap = year%4 == 0 && year%100 !=0 || year%400 == 0;
    //作者把二维数组每行的第一个元素都设置为0，随后在本函数中直接返回i即可
    for(i=1;yearday>daytab[leap][i];i++){
        yearday -= daytab[leap][i];
    }
    *pmonth = i;
    *pday = yearday;
}
```
**如果我想将二维数组作为函数参数。。。**
切记，一般来说数组除了第一维，*其余各维度都必须声明长度*
```c
f(int daytab[2][13]);
f(int daytab[][13]);
//一个指向长度为13的整型数组的指针，因为方括号的运算优先级大于*运算符，所以必须打括号
f(int (*daytab)[13]);
```

## 5.8 指针数组的初始化

### 例程剖析：`month_name`返回某月的字符串

如何初始化字符串数组？第一个维度存储一个指向字符串首的指针
```c
char *month_name(int n){
    //这么写初始化是不需要填入数组长度的，编译器会自动检测
    static char *name[] = {
        "illegal month",
        "Jan", "Feb", "Mar", "April", "...",
        "December"
    }
    return (n<1 || n>12) ? name[0]:name[n];
}
```

## 5.9 二维数组VS指针数组

```c
int a[10][20];
int *b[10];
```

事实上，`a[3][4]`和`b[3][4]`都是合法的，区别在于，二维数组**在初始化的时候程序就已经为它分配好了内存**，而指针数组是**高度动态**的

指针数组的最大用途是拿来存[**字符串列表**](#58-指针数组的初始化)
```c
//事实上这样写也可以。。。但会浪费内存，或存不下大于15个字符长度的字符串
//二维数组写法
char aname[][15] = {"illegal month", "Jan"};

//指针数组写法
char *aname[] = {"illegal month", "Jan"};
```

## 5.10 命令行参数`argc`和`argv`

`argv`是一个数组（第二参数，vector意味着参数向量），`argc`是一个整型（第一参数，用于计算有多少个参数），`argc`的值至少大于等于1，如果为1，则表明程序之后没有任何参数

`echo Hello, world`的效果：
| 表达式    | 值         |
| --------- | ---------- |
| `argv[0]` | `"echo"`   |
| `argv[1]` | `"Hello,"` |
| `argv[2]` | `"world"`  |

其中`argv`的每一个参数都是一个**指向字符串的指针**

所以可选参数为`argv[k]`，其中$k \in [1, argc-1]$  
ANSI要求`argv[argc] = NULL`，在这种情况下，`argc`的值顺理成章地等于传进来的`参数值+1`这个1是程序名字，这算是ANSI对C语言数组索引从0开始的一个修正

```bash
batman@LAPTOP-3KIH8KMK:/mnt/c/code/ANSIC_src/echo_$ ./echo_
1
batman@LAPTOP-3KIH8KMK:/mnt/c/code/ANSIC_src/echo_$ ./echo_ 1
2
batman@LAPTOP-3KIH8KMK:/mnt/c/code/ANSIC_src/echo_$ ./echo_ 1 2
3
batman@LAPTOP-3KIH8KMK:/mnt/c/code/ANSIC_src/echo_$ ./echo_ 1 2 1
4
```

### 例程剖析：实现`echo`

```c
#include<stdio.h>
int main(int argc, char *argv[]){
    int i;
    for(i=1;i<argc;i++){
        printf("%s%s", argv[i], (i==argc-1?(""):(" ")));
    }
    printf("\n");
    return 0;
}

#include<stdio.h>
int main(int argc, char *argv[]){
    while(--argc>0){
        //这里没问题，因为argc=1意味着没有任何参数传进来
        printf("%s%s", *++argv, (argc > 1)?" ":"");
        //第二种写法，让printf()函数的格式化参数变成表达式
        printf((argc>1)?"%s ":"%s", *++argv);
    }
    printf("\n");
    return 0;
}
```

### 例程剖析：实现`grep`

通过命令行的第一个参数指定模式

## 5.11 函数指针

函数不是变量，但可以定义指向函数的指针，这种指针可以被赋值，被存放在数组中，传递给函数以及作为返回值

### 例程剖析：函数指针实现类型无关的`qsort`

排序过程往往包含三部分：
1. 判断两个对象之间的比较操作
2. 颠倒对象次序的交换操作
3. 用于比较和交换的排序算法

通常来说想要让第一和第二步骤和对象的类型无关，可以使用函数指针（感觉像Java里的比较器）

```c
#include<stdio.h>
#include<string.h>

//待排序的最大行数
#define MAXLINES 5000
char *lineptr[MAXLINES] /*指向文本行的指针*/

int readlines(char *lineptr[], int nlines);
void writelines(char *lineptr[], int nlines);

//类型无关的快排
void qsort(void *lineptr, int left, int right, int (*comp)(void *, void *));

//比较函数
int numcmp(char *, char*);

int main(int argc, char *argv[])
{
    int nlines;
    int numeric = 0;

    if(argc>1 && strcmp(argv[1], "-n") == 0)
    //第一个参数为n，则进行数值比较
        numeric = 1;
    if((nlines = readlines(lineptr, MAXLINES)) >= 0){
        //把numcmp和strcmp函数强制转换了
        qsort((void **) lineptr, 0, nlines-1, 
            (int (*)(void*, void*)) (numeric?numcmp:strcmp)));
        
        writelines(lineptr, nlines);
        return 0;
    }
    else{
        printf("input too big to sort\n");
        return 1;
    }
}
```

>为什么使用`void *`作为数组的类型？

因为任何类型的指针转化为`void *`再转换回来不会丢失任何信息

>qsort核心代码段的重构，仔细观察如何使用函数指针

```c
void qsort(void *v[], int left, int right, int (*)(comp)(void *, void *)){
    int i, last;
    void swap(void *v[], int, int);

    if(left >= right){
        return;
    }

    swap(v, left, left+(right-left)/2);
    last = left;
    for(i=left+1;i<=right;i++){
        //重点，高度类似数组名*arr
        if((*comp)(v[left], v[i])>0){
            swap(v, ++last, i);
        }
    }
    swap(v, left, last);
    qsort(v, 0, last-1, comp);
    qsort(v, last+1, right, comp);
}
```

在参数表中的指针数组VS在函数返回值中的指针数组
`void *v[]`或`void**`

注意，strcmp和numcmp都是函数的**地址**，类似数组名（数组名前面也不需要加&来进行取地址运算）

## 5.12 复杂声明

`*`运算优先级低于`()`
```c
//函数声明，这个函数返回int指针
int *f();
//函数指针声明，这个函数返回int对象
int (*f)();
```

# 第六章-结构

## 6.1 结构的基本知识

关键字`struct`引入结构声明
`point`作为`结构标记`其实可以省略，`结构标记`有助于省略声明
注意在结构声明的结尾需要加上`;`
```c
struct point{
    int x;
    int y;
};
```

结构中定义的变量称为`成员变量`，`成员变量`，`结构标记`和`普通变量`可以采用相同的名字，不同结构中的成员可以使用相同的名字（显然地）

>如何声明结构变量

类似于普通变量的声明：
```c
struct {...} x, y, z...;
int x, y, z...;

//使用前述的结构标记进行变量声明
struct point x, y, z;

//结构体的初始化
struct point x = {100, 200};
```

>结构成员运算符

通过`.`运算符访问结构成员

>结构嵌套

```c
struct rect{
    struct point pt1;
    struct point pt2;
}
//初始化嵌套结构成员
struct rect screen;
//访问嵌套结构成员
screen.pt1.x = 3;
```

## 6.2 结构与函数

### 例程剖析：使用`struct`对矩形进行操作

如果结构比较大，使用指针的开销会小很多`struct point *pp;`

```c
struct point *pp;
(*pp).x = 1;

struct point *pp, origin;
pp = &origin;
```

为了简化结构指针的使用，C语言推出了`->`运算符
运算符`.`和`->`都是从左到右结合，所以以下这些表达式效果一致
```c
struct rect r, *rp = &r;

r.pt1.x;
rp->pt1.x;
(r.pt1).x;
(rp->pt1).x;
```

在所有的运算符之间，`.`,`->`,`()`,`[]`运算优先级最高
```c
//以下语句将会增加len的长度
*p->len;
//以下语句将会先对len执行操作，再对p++，此处可以省略括号
(p++)->len
//先读取str指针所指向的值，再对str++
*p->str++
//先读取str指向的值，再对p++
*p++->str
```

## 6.3 结构数组

### 例程剖析：统计C语言关键字出现的次数

```c
//用于记录关键字出现次数的结构数组
struct key{
    char *word;
    int count;
} keytab[NKEYS];

//或者这样分步声明
struct key{char *word; int count;};
struct key keytab[NKEY];

//结构数组的初始化
struct key{
    char *word;
    int count;
} keytab[] = {
    "auto", 0, 
    "break", 0, 
    "while", 0
};

//更为精确的是加上花括号
struct key{
    char *word;
    int count;
} keytab[] = {
    {"auto", 0}, 
    {"break", 0}, 
    {"while", 0}
};
```

`sizeof`运算符是C语言的**编译时**一元运算符（终于等到你哈哈）`sizeof(type_name)`或者`sizeof(object)`将返回一个整型`size_t`，等于传入的类型或者对象所占字节长度，强调是编译时的一元运算符，意味着sizeof函数不能在条件编译`#if`中使用，预处理器不会对类型名进行分析，但预处理器不会计算`#define`语句中的表达式，所以在`#define`语句中可以写

之前我们使用`#define`宏定义将`NKEYS`常量写死了，这样的程序不具备好的鲁棒性，现在通过`sizeof`动态分配结构数组的长度：我们有两种写法
`#define NKEYS (sizeof(keytab)/sizeof(struct key))`
`#define NKEYS (sizeof(keytab)/sizeof(keytab[0]))`

另一种不是那么优雅的解决方法是在结构数组初始化的时候，在数组的尾巴上插入一个空指针，在初始化完毕后遍历数组，随后计算出结构数组的长度，这两种方法的效率有待考虑（目前不清楚`sizeof`的实现机制，但直接告诉我前者效率更高），除了效率方面的考量，这种写法使**程序和结构体定义无关**

## 6.4 指向结构的指针

如何优雅地给函数签名
```c
struct key *
binsearch(char *word, struct key *tab, int n);
```

## 6.7 类型定义`typedef`

用于建立新的数据类型名

```c
typedef int length;
length len, maxlen;
typedef char *String;

String p, lineptr[MSXLINES];
p = (String) malloc(100);
```