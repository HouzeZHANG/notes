# C++ primer 中文版
# Content
- [C++ primer 中文版](#c-primer-中文版)
- [Content](#content)
- [第1章-开始](#第1章-开始)
  - [1.1 编写一个简单的程序](#11-编写一个简单的程序)
  - [1.2 初识输入输出](#12-初识输入输出)
    - [标准输入输出对象](#标准输入输出对象)
      - [向流写入数据](#向流写入数据)
      - [`std::`](#std)
      - [向流读取数据](#向流读取数据)
  - [1.3 注释简介](#13-注释简介)
  - [1.4 控制流](#14-控制流)
    - [1.4.1 while语句](#141-while语句)
    - [1.4.2 for语句](#142-for语句)
    - [1.4.3 读取数量不确定的输入数据](#143-读取数量不确定的输入数据)
    - [1.4.4 if语句](#144-if语句)
  - [1.5 类简介](#15-类简介)
- [第一部分 C++基础](#第一部分-c基础)
  - [第二章 变量和基本类型](#第二章-变量和基本类型)

# 第1章-开始

## 1.1 编写一个简单的程序

1. return type 返回类型
2. function name 函数名
3. parameter list 参数列表
4. function body函数体
5. built-in type 内置类型
6. curly brace 左花括号
7. block of statement 语句块
8. Integrated developed environment IDE
9. source file 源文件

>一种类型不仅定义了数据元素的内容，还**定义了数据上可以进行的运算**

>在windows下运行可执行文件不需要添加扩展名

查看程序返回值
```bash
// Linux
echo $?

//Windows
echo %ERRORLEVEL%
```

**调用编译器**，生成**windows平台下的可执行文件**.exe
```bash
g++ -o prog1 prog1.cc
```

>GCC支援的语言大多在MinGW也受支援，其中涵盖C、C++、Objective-C、Fortran及Ada。**对于C语言之外的语言，MinGW使用标准的GNU运行时库，如C++使用GNU libstdc++。**但是MinGW使用Windows中的C运行时库。因此用MinGW开发的程序不需要额外的第三方DLL支持就可以直接在Windows下运行，而且也不一定必须遵从GPL许可证。这同时造成了MinGW开发的程序只能使用Win32API和跨平台的第三方库，而缺少POSIX支持[4]，大多数GNU软件无法在不修改源代码的情况下用MinGW编译。

>作为编译系统，Mingw32可以用来做Unix平台到windows平台的跨平台软件移植工作

>Cygwin 与 MinGW 皆可用来移植 Unix 软件到 Windows，但它们**采用截然不同的实作**。Cygwin 旨在提供一个完整的 POSIX 层，包括主流 Unix 的系统呼叫及函式库实作；其重视兼容性优先于性能。相对的，MinGW 则着重简化与性能。因此，它并不提供某些难以用 Windows API 实现的 POSIX API，例如 fork()，mmap() 和 ioctl()。使用跨平台函式库写成的应用程式，若函式库本身已移植到了 MinGW（例如 SDL、wxWidgets、Qt 或 GTK+），则那些应用程式通常也容易用 MinGW 编译。
用 Cygwin 写成的 Windows 程序，因为是执行在公共版权的兼容 DLL 上，所以 DLL 必须随著程序源代码一起发布。MinGW 则不需要兼容层，因为基于 MinGW 的程序是直接调用 Windows API 编译的。
MinGW 搭配 MSYS 可以产生一个小却完整的执行环境，让程式可以载入随身装置当中，却不动到注册表或产生额外档案。
在 POSIX 系统下，用 MinGW-GCC 交叉编译 Windows 应用程式也是可行的。这意味著开发者不需要安装 Windows 与 MSYS 才能编译 Windows 软件，或 Windows+Cygwin 软件。

## 1.2 初识输入输出

1. stream 流
2. standard input 标准输入
3. standard output 标准输出
4. standard error 标准错误
5. string literal 字符串字面值常量
6. manipulator 操纵符
7. namespace 命名空间
8. condition 条件

C++**没有定义任何输入输出语句**（和C语言一样）我们使用`iostream`库）

两种类型：`istream`和`ostream`分别代表输入流和输出流，是`iostream`标准库中定义的两个类型，流（stream）表达的是，随着时间的推移，字符**顺序产生&消耗**

### 标准输入输出对象

`cin`和`cout`分别是`istream`和`ostream`类型的对象
`cerr`和`clog`分别输出标准错误和日志

```cpp
#include<iostream>

int main(){
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The sum of " << v1 << " and " << v2 
            << " is " << v1 + v2 << std::endl;
    return 0;
}
```

#### 向流写入数据
C++的输出运算符：`<<`
1. 左侧运算对象必须是一个ostream类型对象
2. 右侧对象是要打印的值
3. 运算结果为左侧的运算对象
4. `std::endl`是一个**操纵符**特殊值，对标准输出对象输入该操纵符将结束当前行，将设备关联的**缓冲区内容刷新到页面上**，所以`cout`使用的是行缓冲
5. 标准库中定义了不同版本的输入输出运算符，故如下代码可以正常运转

```cpp
    std::cout << "The sum of " << v1 << " and " << v2 
            << " is " << v1 + v2 << std::endl;
```

>在调试的阶段如果需要使用`cout`来打印信息，记得使用`std::endl`来刷新缓冲区，这样就算程序崩溃，留在缓冲区的内容也会被及时打印到设备上

#### `std::`
1. `std::`指出，`cout`和`cin`是定义在名为`std`的命名空间中的
2. 命名空间的设定是为了防止名字冲突
3. `std`是标准库的命名空间
4. `::`作用域运算符

#### 向流读取数据
C++的输入运算符`>>`，返回左侧对象作为计算结果

## 1.3 注释简介

`/*...*/`注释**界定符**
1. 注释界定符不能嵌套
2. 单行注释将会把改行中的所有内容都忽略
3. `""`双引号之间的注释界定符没有注释的效果
4. 编译器遇到左界定符时，会注释掉所有的字符，直到右界定符

## 1.4 控制流

### 1.4.1 while语句

### 1.4.2 for语句

### 1.4.3 读取数量不确定的输入数据
```c++
while(std::cin>>x){
  ...
}
```
>原理：输入运算符返回左侧的对象，当使用`istream`对象作为条件时，可以起到检测流的状态，如果输入无效，比如类型不匹配，或是遇到EOF，则为`False`

故该循环停止的条件有二，其一为当遇到EOF时，其二为输入错误时

### 1.4.4 if语句

## 1.5 类简介

>C++中我们通过定义类来定义自己的数据结构
C++设计之初的焦点就是能够定义使用上像内置类型一样自然的**类类型**（class type）

1. 习惯上头文件通过其中定义的类的名字命名
2. 标准库头文件通常不带后缀
3. 标准库头文件使用`<>`，不属于标准库的头文件，使用`""`

>为了使用一个类，我们不需要知道其如何实现，只需要知道类对象可以执行什么操作
类也定义了类对象的行为

1. 成员函数（member function）是定义为类的一部分的函数，也被称为方法（methode）
2. 点运算符`.`返回指定的成员

# 第一部分 C++基础

和Python语言不同，C++的类型检查发生在编译阶段（静态类型语言）

## 第二章 变量和基本类型

>数据类型是程序的基础

字符，整数，浮点数