# 2022-02-18-PythonConcept-Chapter23-Modules Coding Basics

## 如何创建并使用模块及其attributes？

> All the names assigned at the top level of the module become its
> attributes (names associated with the module object) and are exported for clients to use —they morph from variable to module object attribute automatically.

模块名必须符合Python的变量命名规范，不能使用reserved name命名！

当模块被导入之后，Python将模块名称映射到包含文件路径和扩展名的完整外部文件名

> For instance, a module named M ultimately maps to some external file <directory>\M.<extension> that contains the module’s code.

## extension modules

用其他语言比如C,C++等编写的模块

当extension modules被调用的时候，他们和普通的 python模块一样被处理

https://www.oreilly.com/library/view/programming-python-4th/9781449398712/

这本书中有关于extension modules编程的内容

## 关于import和from的语法

一条import语句可以跟随多个modules

```python
import numpy,pandas
```

from语句之后的import依然可以跟随多个names

```python
from numpy import a,b,c
```

在这种语法下，我们不能使用.来通过module名称检索name，因为**from语句不会将module和module名进行绑定**！我们只能直接使用module中的name来访问attribute

from是import语句的minor extension（较小的扩展），from语句依然会执行查找，编译，运行这三步，但除此以外还会执行第四步，将一个或者多个names拷贝出文件，整个文件都会被加载，但你会获得更加直接的对name的访问方式

```python
from module1 import *
```

> Technically, both import and from statements invoke the same import operation; the from * form simply adds an extra step that copies all the names in the module into the importing scope. It essentially collapses one module’s namespace into another; again, ****the net effect is less typing for us. Note that only * works in this context; you can’t use pattern matching to select a subset of names (though you could with more work and a loop through a module’s dict, discussed ahead).****

这段不懂什么意思

### 2.X和3.X之争

python2允许在函数中使用from import语句，这让python能够在函数运行之前静态检查变量，但总之，还是在Python文件开头进行模块导入操作比较好，这样使程序更加易读

## 多次import同一个module

module只会在第一次导入的时候运行，因为import操作开销巨大，每个文件只会运行一次！所以在模块中初始化的变量，如果在主程序中被修改，如果再次导入该模块，该变量并不会被重新初始化！

> they just fetch the already created module object from Python’s internal modules table.

想要彻底重新地import某个模块，必须使用reload函数

## import和from都是assignment（implicit assignment）

<u>*和chapter6联系上了，chapter6介绍了python的assignment module*</u>

def，import，from都是executable的**statement**，并不是compile-time declarations

也就是说他们可以被nested内嵌在if语句，def语句，to be loaded only on calls这我不懂，在try语句中出现。

> • import assigns an entire module object to a single name.
> • from assigns one or more names to objects of the same names in another module.

import将一个single name绑定到一个完整的module上

？？？

> All the things we’ve already discussed about assignment apply to module access, too. For instance, names copied with a from become references to shared objects; as with function arguments, reassigning a copied name has no effect on the module from which it was copied, but changing a shared mutable object through a copied name can also change it in the module from which it was imported.

![image-20220222144731929](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220222144731929.png)

新建一个variable x，将其绑定到module上，通过x来修改可变对象，自然会修改可变对象本身，而不是创建一个新对象！