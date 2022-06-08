# 2022-02-21-PythonConcept-Chapter6-Modules : The Dynamic Typing Interlude

## 摘要

本章介绍了Python的动态类型特性，介绍了variable和object之间的关系，介绍了shared object和python对象垃圾回收的机制，同时还介绍了可变类型的in-place change特性，如何拷贝object，如何进行equality判定以及如何获取某一object被引用的次数，同时还提及了弱引用。。。

python中只存在这唯一的一个assignment model

## Dynamic typing is the root of the flexibility

statically typed language 静态语言类型

python中变量的类型在运行阶段自动分配

### 变量创建

Python在代码运行前就会检测names，但理解为一旦被赋值变量就被创建，这也是一样的

### 变量variable类型

变量没有类型type，只有对象object有类型，类型type这个概念和names无关，只和对象object有关

在同一时刻，一个变量只能指向一个对象

> The notion of type lives with objects, not names.

### 变量使用

当变量出现在表达式中，会被替换为相应的对象以进行计算

变量必须先被assigned，才能被使用，否则会报错！

> Variable creation
> A variable (i.e., name), like a, is created when your code first assigns it a value. Future assignments change the value of the already created name. Technically, Python detects some names before your code runs, but you can think of it as though initial assignments make variables.
>
> Variable types
> A variable never has any type information or constraints associated with it. The notion of type lives with objects, not names. Variables are generic in nature; they always simply refer to a particular object at a particular point in time.
>
> Variable use
> When a variable appears in an expression, it is immediately replaced with the object that it currently refers to, whatever that may be. Further, all variables must be explicitly assigned before they can be used; referencing unassigned variables results in errors.

举例来说，counters必须在counter+1之前被assigned

### 例子

a = 3

> 1. Create an object to represent the value 3.
> 2. Create the variable a, if it does not yet exist.
> 3. Link the variable a to the new object 3.

### 内存视图

一般来说，variable和object存储在不同的内存分区，他们通过**reference**进行连接，variable只能指向object，而object可以指向其他object，比如list

![image-20220222102241912](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222102241912.png)

> Internally, the variable is really a pointer to the object’s memory space created by running the literal expression 3
>
> a reference is a kind of association, implemented as a pointer in memory

从某种意义上来讲，variable都是指针，并且是没有类型的指针！在内存实现上用指针完成！

> • Variables are **entries** in a system table, with spaces for links to objects.
> • Objects are pieces of allocated memory, with enough space to represent the values for which they stand.
> • References are automatically followed pointers from variables to objects.

## python会重用不变的对象

python will reuse certain kinds of unchangeable objects, such as small integer and string

每一个object都有两个标志域，**type designator**用于显示什么时候该对象能够被回收，另一个标志域**reference counter**用于显示该对象的类型

## Garbage-collected

### reference counter

> whenever a name is assigned to a new object, the space held by the prior object is reclaimed if it is not referenced by any other name or object.

当一个name被赋予新的对象的时候，如果先前绑定的对象没有被其他name所引用，那么该对象就会被回收，如果是小整数，或是小字符串，则会被扔到free space pool中

通过引用计数，也就是前面提到的reference counter实现

python的垃圾回收的好处是，python能够自动地申请释放内存，相较于更为低级的语言，能省去相当数量的语句

### cyclic reference, cycle detector

L.append(L)?

当出现循环引用的时候，reference counter永远不会降低到0，所以这种特殊的情况需要使用cyclic reference来跟踪变量

以上的垃圾回收机制只适用于CPython，它不适用于Jython,IronPython

## Shared reference,shared object

a = 3

b = a

这么写会让a，b这两个变量指向同一片内存，并不会将b和a这两个变量连接！

![image-20220222113807040](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222113807040.png)

a = 3

b = a

a = 'spam'

![image-20220222113844587](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222113844587.png)

对于同类型的对象，这种现象依然存在

a = 3

b = a

a = a+2



==>a = 5

==>b = 3

## In-place changes, mutable types

python中存在对象的原地改动！列表，字典和集合！

> there are objects and operations that perform in-place object changes—**Python’s mutable types**, including lists, dictionaries, and sets

![image-20220222120916470](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222120916470.png)

python将L1指向的这个list所指向的第一个object修改了！list本身没有修改！

所以像这样修改list，会在程序其他地方出现副作用！有点像静态变量

这种现象只会在支持in-place change 的mutable objects身上出现

### 如何copy对象？

L2 = L1[:]

创建L1的副本，而不是将L2指向L1所指向的list

或者使用copy函数，或者使用内建的list函数，dict函数或者set函数

**X.copy()**适用于字典和集合，这两种对象不能使用全部切片，因为他们并不sequences

### python的浅拷贝和深拷贝

![image-20220222122921926](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222122921926.png)

## Equality check

### values

a == b

### same object

a is b

检测指针指向的地址是否相同

![image-20220222124801229](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222124801229.png)

## sys.getrefcount()

获得对象被ref的次数

## 动态类型的作用

让工作量变小，但是让程序更难调试

动态类型是python多态性的根基

## weak reference

由weakref模块实现

如果连接到某一个对象的最后一个引用是weak reference，那么就算这个reference依然存在，这个object依然会被垃圾回收！

> This can be useful in **dictionary-based caches** of large objects