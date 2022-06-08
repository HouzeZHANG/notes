# Chapter22-Modules : The big picture

### Python模块简介

module会提供self-contained的namespace，self-contained译为独立的，以降低变量名冲突的情况。

module也是最高层级的编程单元，highest-level program organization unit

通常来说module对应于文件，一个文件就是一个module

可以被称为module的文件不仅包括.py的python脚本，还包括其他语言写的代码文件，甚至包括directories  in packages imports?

### Python如何实现模块导入

#### import

全部导入

#### from

仅仅导入部分names

#### imp.reload

使得程序在运行时进行重新导模块

> Modules and classes are really just glorified namespaces.

### 为什么使用module

因为module能将组件有组织地安排进system中，使用namespace来管理这些在top level of a module定义的name，在导入之后他们会成为被导入模块的attributes

代码复用，namespace partitioning（除非你import其他文件，否则你无法使用其他文件中的name）

### Structure a Program

文件由Python statements组成，main文件叫做top - level file，被导入文件叫做module，main文件包含main flow of control

一般把names defined in a certain module叫做module的attributes

Python导模块一般在import语句被执行的时候才会发生，import语句的作用是将模块名和被加载的模块进行配对（assign）

Python模块中定义的对象都是在运行时被创建的

**object.attribute** natation是python典型的语法

通常来说，module是最高级别的reuse和organizational structure

### Python标准库

Python standard library并不属于Python的一部分

### Import机制（非常重要）

总结：python先在sys.modules中查找包是否已经被导入，如果没被导入，进行查找编译运行三步。查找的地址为（主目录+PYTHONPATH环境变量+PYTHON标准库+.pth文件+site-package），是否编译取决于pycache文件夹中是否存在符合版本号且为最新版本的字节码文件，最后运行，向内存中载入全部module数据。

python使用import hooks来从压缩文件中提取文件！

和C语言的include不同，python的import是真正运行时的操作（runtime operations）

> Bear in mind that all three of these steps are carried out only the first time a module is imported during a program’s execution; later imports of the same module in a program run bypass all of these steps and simply fetch the already loaded module object in memory.
>
> 只有在模块第一次导入的时候（runtime）python才会执行这三步，之后再次导入该包的时候，python会直接加载在内存中的数据
>
> Technically, Python does this by storing loaded modules in a table named <u>**sys.modules**</u> and checking there at the start of an import operation. If the module is not present, a three-step process begins.
>
> 从技术上说，python会通过sys.modules这张表记录所有已经被载入的模块，在执行import语句的时候会遍历这张表（其实是**<u>字典</u>**），如果module不在这张表中，便会执行以下这三步！

#### Step1 : Find

> Python uses a <u>**standard module search path**</u> and known file types to locate the module file corresponding to an import statement.1
>
> Python使用标准模块搜索路径和已知的文件类型来定位module文件
>
> It’s syntactically illegal to include path and extension details in a standard import.
>
> 在导模块的时候，路径名和扩展名不能写
>
>  However, package imports, which we’ll discuss in Chapter 24, allow import statements to include part of the directory path leading to a file as a set of ***<u>period-separated names</u>***.
>
> 在导包的时候可以写路径名和扩展名
>
> Package imports, though, still rely on the normal module search path to locate the leftmost directory in a package path (i.e., they are relative to a directory in the search path).
>
> 导包依然依赖于normal module search path
>
> They also cannot make use of any platform-specific directory syntax in the import statements; such syntax only works on the search path.
>
> 导包语法不能使用非跨平台的路径
>
> Also, note that module file search path issues are not as relevant when you run frozen executables (discussed in Chapter 2), which typically embed byte code in the binary image.
>
> 这个没看懂！什么是frozen executables?

python会无差别地选择各种各样的文件类型！如果在同一个目录下出现同名不同类的文件，会先导入先扫描到的文件。不同目录下的更是如此。

> For example, an import statement of the form import b might today load or resolve to:
> • A source code file named b.py
> • A byte code file named b.pyc
> • An optimized byte code file named b.pyo (a less common format)
> • A directory named b, for package imports (described in Chapter 24)
> • A compiled extension module, coded in C, C++, or another language, and dynamically
> linked when imported (e.g., b.so on Linux, or b.dll or b.pyd on Cygwin
> and Windows)
> • A compiled built-in module coded in C and statically linked into Python
> • A ZIP file component that is automatically extracted when imported
> • An in-memory image, for frozen executables
> • A Java class, in the Jython version of Python
> • A .NET component, in the IronPython version of Python

#### Step2 : Compile to Byte code

> After finding a source code file that matches an import statement by traversing the <u>**module search path**</u>, Python next compiles it to <u>**byte code**</u>, if necessary
>
> 在搜索模块搜索路径之后，如果python发现import文件和路径中的文件名符合，那么会将其编译为字节码文件
>
> During an import operation Python checks both <u>**file modification times**</u> and the <u>**byte code’s Python version number**</u> to decide how to proceed.
>
> 在导入操作执行之后，Python会检查文件修改的时间节点和字节码版本来决定之后的操作
>
> The former uses file “<u>**timestamps**</u>,” and the latter uses either a “<u>**magic**</u>” number embedded in the byte code or a filename, depending on the Python release being used.
>
> 文件修改的时间节点用时间戳来进行判定，后者字节码版本则是使用magic number来进行判断，magic number的生成方式取决于python解释器的版本

##### 需要编译：

如果字节码文件比源代码文件更老（比如你修改了源代码文件），或者更换了生成字节码文件的解释器，Python将会自动生成新的字节码文件

在3.2版本之后，字节码文件被单独存放在pycache目录中，并以编译他们的Python解释器版本号命名，这有效地解决了当一台设备安装多个解释器时需要反复编译字节码的问题，所以3.2版本之后，需要编译的情况只有字节码文件比源代码文件更老这一种情况

##### 不需要编译：

Python解释器发现字节码文件并不比源文件老，于是跳过编译步骤。此外，如果在指定目录下只找到了字节码文件而不存在源文件，Python解释器会直接读取字节码文件！也就是说你可以只用字节码文件来构建一个Python程序，这种策略使Python更快！

因为编译往往由import语句触发，所以不太容易见到你的主程序的字节码文件，除非他们被其他程序所调用。只有被import的文件才会在计算机上留下.pyc的字节码文件。

> The byte code of top-level files is used internally and discarded; byte code of
> imported files is saved in files to speed future imports.
>
> 主程序的字节码文件被隐式创建并被销毁，被导的模块的字节码会被保留以便提高程序运行效率

加了\__name\__和\__main\__语法的脚本既可以当作top-level code作为主程序运行，也可以被引用，其机制将在后续文章中介绍

#### Step3 : Run

执行模块的字节码文件！

> and any assignments made to names during this step generate attributes of the resulting module object

> Because of this, any given module is imported only once per process by default. Future imports skip all three import steps and reuse the already loaded module in memory.

Python的模块导入操作会消耗大量的计算机资源——目录查找、编译器调用、解释器执行。。。所以任何模块只会被import导入一次，如果想重复导入，需要使用imp.reload函数

#### 关于pycache的细节

> Byte code is instead stored in files in a subdirectory named __pycache__, which Python creates if needed, and which is located in the directory containing the corresponding source files.

#### 2.X和3.X之争，兼容性问题

> On the other hand, it is not without potential incompatibilities in programs that rely on the prior file and directory structure. This may be a compatibility
> issue in some tools programs, for instance, though most well-behaved tools
> should work as before. See Python 3.2’s “What’s New?” document for details on potential impacts.

### sys.path模块搜索路径(module search path)配置（非常重要）

> you need to know how to tap into its search path in order to extend it.
>
> the path attribute of the standard library module sys
>
> 标准库sys的path成员

因为import只管module的名字，不管路径和扩展名，所以sys.path在导入模块的时候扮演者重要角色，python便利这个list然后选定第一个遇到的module。

Python在启动（program startup）的时候就会配置好这个变量！（按照下面的顺序添加）

```python
sys.path.append('.\\form')
append方法只会在当前程序运行期间对PTAH进行修改！

print(sys.path)
```

PS C:\code\CleanSkyLMSM> & c:/code/CleanSkyLMSM/env/Scripts/python.exe c:/code/CleanSkyLMSM/QT/app.py
['c:\\code\\CleanSkyLMSM\\QT', 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\python37.zip', 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\DLLs', 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib', 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37', 'C:\\code\\CleanSkyLMSM\\env', 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages', '.\\form']

如果出现空字符串意味着当前目录

直接修改sys.path列表往往只对当前脚本有效，如果使用.pth文件或者PYTHONPATH文件来配置目录，往往会起到更加持久的效果

但另一方面建议修改sys.path列表，比如在服务器上配置python程序，此时不存在所谓的PYTHONPATH环境变量！

#### 模块搜索路径的组成（按顺序）

> 1. The home directory of the program
> 2. PYTHONPATH directories (if set)
> 3. Standard library directories
> 4. The contents of any .pth files (if present)
> 5. The site-packages home of third-party extensions

#### 1. Home directory(auto)

取决于你以什么方式运行Python程序：如果是脚本，那么将是主程序所在的目录，如果是交互式运行，那么为当前命令行所在目录，在main函数所在目录的module会将位于其他地址的module重载！因为HOME DIRECTORY是第一个被访问的！一旦生成了对应的字节码文件，就不会重写字节码文件了！正因为如此，最好不要依赖于HOME directory！移植性--

> be careful not to accidentally hide library modules this way if you need them in your program, or use package tools we’ll meet later that can partially sidestep this issue.

#### 2. PYTHONPATH环境变量(可配置)

#### 3. Standard library directories(auto)

往往不需要手动添加到PYTHONPATH中

#### 4. .pth path file directories(可配置)

可以在.pth结尾的文件中逐行列出需要扫描的目录，其效果和PYTHONPATH一致

> For instance, if you’re running Windows and Python 3.3, a file named myconfig.pth may be placed at the top level of the Python install directory (C:\Python33) or in the sitepackages subdirectory of the standard library there (C:\Python33\Lib\site-packages) to extend the module search path. On Unix-like systems, this file might be located in <u>**usr/local/lib/python3.3/site-packages**</u> or <u>**/usr/local/lib/site-python**</u> instead.

在第三方库之前被导入！

#### 5. Lib\site-packages

这是第三方库通常的安装地址

### 关于import的小实验

#### 1. 验证sys.module

验证在导入numpy这个module之后，sys.modules变量中会添加numpy对应的module，确保python不会重复导入numpy

```python
import sys

print(sys.modules)

print("\n")

import numpy

print(sys.modules)
```

PS C:\code\CleanSkyLMSM> & c:/code/CleanSkyLMSM/env/Scripts/python.exe c:/code/test/c.py
{'sys': <module 'sys' (built-in)>, 'builtins': <module 'builtins' (built-in)>, '_frozen_importlib': <module 'importlib._bootstrap' (frozen)>, '_imp': <module '_imp' (built-in)>, '_thread': <module '_thread' (built-in)>, '_warnings': <module '_warnings' (built-in)>, '_weakref': <module '_weakref' (built-in)>, 'zipimport': <module 'zipimport' (built-in)>, '_frozen_importlib_external': <module 'importlib._bootstrap_external' (frozen)>, '_io': <module 'io' (built-in)>, 'marshal': <module 'marshal' (built-in)>, 'nt': <module 'nt' (built-in)>, 'winreg': <module 'winreg' (built-in)>, 'encodings': <module 'encodings' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\__init__.py'>, 'codecs': <module 'codecs' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\codecs.py'>, '_codecs': <module '_codecs' (built-in)>, 'encodings.aliases': <module 'encodings.aliases' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\aliases.py'>, 'encodings.utf_8': <module 'encodings.utf_8' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\utf_8.py'>, '_signal': <module '_signal' (built-in)>, '__main__': <module '__main__' from 'c:/code/test/c.py'>, 'encodings.latin_1': <module 'encodings.latin_1' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\latin_1.py'>, 'io': <module 'io' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\io.py'>, 'abc': <module 'abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\abc.py'>, '_abc': <module '_abc' (built-in)>, 'site': <module 'site' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\site.py'>, 'os': <module 'os' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\os.py'>, 'stat': <module 'stat' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\stat.py'>, '_stat': <module '_stat' (built-in)>, '_collections_abc': <module '_collections_abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_collections_abc.py'>, 'ntpath': <module 'ntpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ntpath.py'>, 'genericpath': <module 'genericpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\genericpath.py'>, 'os.path': <module 'ntpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ntpath.py'>, '_sitebuiltins': <module '_sitebuiltins' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_sitebuiltins.py'>, '_bootlocale': <module '_bootlocale' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_bootlocale.py'>, '_locale': <module '_locale' (built-in)>, 'encodings.gbk': <module 'encodings.gbk' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\gbk.py'>, '_codecs_cn': <module '_codecs_cn' (built-in)>, '_multibytecodec': <module '_multibytecodec' (built-in)>, '_virtualenv': <module '_virtualenv' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\_virtualenv.py'>, 'functools': <module 'functools' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\functools.py'>, '_functools': <module '_functools' (built-in)>, 'collections': <module 'collections' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\collections\\__init__.py'>, 'operator': <module 'operator' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\operator.py'>, '_operator': <module '_operator' (built-in)>, 'keyword': <module 'keyword' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\keyword.py'>, 'heapq': <module 'heapq' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\heapq.py'>, '_heapq': <module '_heapq' (built-in)>, 'itertools': <module 'itertools' (built-in)>, 'reprlib': <module 'reprlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\reprlib.py'>, '_collections': <module '_collections' (built-in)>, 'importlib': <module 'importlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\__init__.py'>, 'importlib._bootstrap': <module 'importlib._bootstrap' (frozen)>, 'importlib._bootstrap_external': <module 'importlib._bootstrap_external' (frozen)>, 'types': <module 'types' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\types.py'>, 'warnings': <module 'warnings' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\warnings.py'>, 'importlib.abc': <module 'importlib.abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\abc.py'>, 'importlib.machinery': <module 'importlib.machinery' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\machinery.py'>, 'importlib.util': <module 'importlib.util' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\util.py'>, 'contextlib': <module 'contextlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\contextlib.py'>}

{'sys': <module 'sys' (built-in)>, 'builtins': <module 'builtins' (built-in)>, '_frozen_importlib': <module 'importlib._bootstrap' (frozen)>, '_imp': <module '_imp' (built-in)>, '_thread': <module '_thread' (built-in)>, '_warnings': <module '_warnings' (built-in)>, '_weakref': <module '_weakref' (built-in)>, 'zipimport': <module 'zipimport' (built-in)>, '_frozen_importlib_external': <module 'importlib._bootstrap_external' (frozen)>, '_io': <module 'io' (built-in)>, 'marshal': <module 'marshal' (built-in)>, 'nt': <module 'nt' (built-in)>, 'winreg': <module 'winreg' (built-in)>, 'encodings': <module 'encodings' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\__init__.py'>, 'codecs': <module 'codecs' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\codecs.py'>, '_codecs': <module '_codecs' (built-in)>, 'encodings.aliases': <module 'encodings.aliases' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\aliases.py'>, 'encodings.utf_8': <module 'encodings.utf_8' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\utf_8.py'>, '_signal': <module '_signal' (built-in)>, '__main__': <module '__main__' from 'c:/code/test/c.py'>, 'encodings.latin_1': <module 'encodings.latin_1' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\latin_1.py'>, 'io': <module 'io' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\io.py'>, 'abc': <module 'abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\abc.py'>, '_abc': <module '_abc' (built-in)>, 'site': <module 'site' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\site.py'>, 'os': <module 'os' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\os.py'>, 'stat': <module 'stat' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\stat.py'>, '_stat': <module '_stat' (built-in)>, '_collections_abc': <module '_collections_abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_collections_abc.py'>, 'ntpath': <module 'ntpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ntpath.py'>, 'genericpath': <module 'genericpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\genericpath.py'>, 'os.path': <module 'ntpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ntpath.py'>, '_sitebuiltins': <module '_sitebuiltins' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_sitebuiltins.py'>, '_bootlocale': <module '_bootlocale' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_bootlocale.py'>, '_locale': <module '_locale' (built-in)>, 'encodings.gbk': <module 'encodings.gbk' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\encodings\\gbk.py'>, '_codecs_cn': <module '_codecs_cn' (built-in)>, '_multibytecodec': <module '_multibytecodec' (built-in)>, '_virtualenv': <module '_virtualenv' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\_virtualenv.py'>, 'functools': <module 'functools' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\functools.py'>, '_functools': <module '_functools' (built-in)>, 'collections': <module 'collections' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\collections\\__init__.py'>, 'operator': <module 'operator' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\operator.py'>, '_operator': <module '_operator' (built-in)>, 'keyword': <module 'keyword' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\keyword.py'>, 'heapq': <module 'heapq' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\heapq.py'>, '_heapq': <module '_heapq' (built-in)>, 'itertools': <module 'itertools' (built-in)>, 'reprlib': <module 'reprlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\reprlib.py'>, '_collections': <module '_collections' (built-in)>, 'importlib': <module 'importlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\__init__.py'>, 'importlib._bootstrap': <module 'importlib._bootstrap' (frozen)>, 'importlib._bootstrap_external': <module 'importlib._bootstrap_external' (frozen)>, 'types': <module 'types' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\types.py'>, 'warnings': <module 'warnings' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\warnings.py'>, 'importlib.abc': <module 'importlib.abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\abc.py'>, 'importlib.machinery': <module 'importlib.machinery' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\machinery.py'>, 'importlib.util': <module 'importlib.util' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\importlib\\util.py'>, 'contextlib': <module 'contextlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\contextlib.py'>, 'numpy': <module 'numpy' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\__init__.py'>, 'numpy._globals': <module 'numpy._globals' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\_globals.py'>, 'numpy.__config__': <module 'numpy.__config__' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\__config__.py'>, 'numpy._version': <module 'numpy._version' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\_version.py'>, 'json': <module 'json' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\json\\__init__.py'>, 'json.decoder': <module 'json.decoder' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\json\\decoder.py'>, 're': <module 're' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\re.py'>, 'enum': <module 'enum' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\enum.py'>, 'sre_compile': <module 'sre_compile' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\sre_compile.py'>, '_sre': <module '_sre' (built-in)>, 'sre_parse': <module 'sre_parse' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\sre_parse.py'>, 'sre_constants': <module 'sre_constants' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\sre_constants.py'>, 'copyreg': <module 'copyreg' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\copyreg.py'>, 'json.scanner': <module 'json.scanner' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\json\\scanner.py'>, '_json': <module '_json' (built-in)>, 'json.encoder': <module 'json.encoder' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\json\\encoder.py'>, 'numpy._distributor_init': <module 'numpy._distributor_init' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\_distributor_init.py'>, 'glob': <module 'glob' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\glob.py'>, 'fnmatch': <module 'fnmatch' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\fnmatch.py'>, 'posixpath': <module 'posixpath' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\posixpath.py'>, 'ctypes': <module 'ctypes' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ctypes\\__init__.py'>, '_ctypes': <module '_ctypes' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\DLLs\\_ctypes.pyd'>, 'struct': <module 'struct' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\struct.py'>, '_struct': <module '_struct' (built-in)>, 'ctypes._endian': <module 'ctypes._endian' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ctypes\\_endian.py'>, 'numpy.core': <module 'numpy.core' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\__init__.py'>, 'numpy.version': <module 'numpy.version' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\version.py'>, 'numpy.core.multiarray': <module 'numpy.core.multiarray' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\multiarray.py'>, 'numpy.core.overrides': <module 'numpy.core.overrides' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\overrides.py'>, 'textwrap': <module 'textwrap' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\textwrap.py'>, 'datetime': <module 'datetime' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\datetime.py'>, 'time': <module 'time' (built-in)>, 'math': <module 'math' (built-in)>, '_datetime': <module '_datetime' (built-in)>, 'numpy.core._multiarray_umath': <module 'numpy.core._multiarray_umath' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_multiarray_umath.cp37-win_amd64.pyd'>, 'numpy.compat': <module 'numpy.compat' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\compat\\__init__.py'>, 'numpy.compat._inspect': <module 'numpy.compat._inspect' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\compat\\_inspect.py'>, 'numpy.compat.py3k': <module 'numpy.compat.py3k' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\compat\\py3k.py'>, 'pathlib': <module 'pathlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\pathlib.py'>, 'errno': <module 'errno' (built-in)>, 'urllib': <module 'urllib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\urllib\\__init__.py'>, 'urllib.parse': <module 'urllib.parse' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\urllib\\parse.py'>, 'pickle': <module 'pickle' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\pickle.py'>, '_compat_pickle': <module '_compat_pickle' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_compat_pickle.py'>, '_pickle': <module '_pickle' (built-in)>, 'numpy.core.umath': <module 'numpy.core.umath' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\umath.py'>, 'numpy.core.numerictypes': <module 'numpy.core.numerictypes' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\numerictypes.py'>, 'numbers': <module 'numbers' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\numbers.py'>, 'numpy.core._string_helpers': <module 'numpy.core._string_helpers' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_string_helpers.py'>, 'numpy.core._type_aliases': <module 'numpy.core._type_aliases' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_type_aliases.py'>, 'numpy.core._dtype': <module 'numpy.core._dtype' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_dtype.py'>, 'numpy.core.numeric': <module 'numpy.core.numeric' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\numeric.py'>, 'numpy.core.shape_base': <module 'numpy.core.shape_base' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\shape_base.py'>, 'numpy.core.fromnumeric': <module 'numpy.core.fromnumeric' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\fromnumeric.py'>, 'numpy.core._methods': <module 'numpy.core._methods' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_methods.py'>, 'numpy.core._exceptions': <module 'numpy.core._exceptions' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_exceptions.py'>, 'numpy.core._ufunc_config': <module 'numpy.core._ufunc_config' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_ufunc_config.py'>, 'collections.abc': <module 'collections.abc' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\collections\\abc.py'>, 'numpy.core.arrayprint': <module 'numpy.core.arrayprint' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\arrayprint.py'>, 'numpy.core._asarray': <module 'numpy.core._asarray' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_asarray.py'>, 'numpy.core.defchararray': <module 'numpy.core.defchararray' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\defchararray.py'>, 'numpy.core.records': <module 'numpy.core.records' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\records.py'>, 'numpy.core.memmap': <module 'numpy.core.memmap' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\memmap.py'>, 'numpy.core.function_base': <module 'numpy.core.function_base' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\function_base.py'>, 'numpy.core.machar': <module 'numpy.core.machar' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\machar.py'>, 'numpy.core.getlimits': <module 'numpy.core.getlimits' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\getlimits.py'>, 'numpy.core.einsumfunc': <module 'numpy.core.einsumfunc' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\einsumfunc.py'>, 'numpy.core._add_newdocs': <module 'numpy.core._add_newdocs' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_add_newdocs.py'>, 'numpy.core._multiarray_tests': <module 'numpy.core._multiarray_tests' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_multiarray_tests.cp37-win_amd64.pyd'>, 'numpy.core._add_newdocs_scalars': <module 'numpy.core._add_newdocs_scalars' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_add_newdocs_scalars.py'>, 'platform': <module 'platform' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\platform.py'>, 'subprocess': <module 'subprocess' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\subprocess.py'>, 'signal': <module 'signal' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\signal.py'>, 'threading': <module 'threading' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\threading.py'>, 'traceback': <module 'traceback' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\traceback.py'>, 'linecache': <module 'linecache' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\linecache.py'>, 'tokenize': <module 'tokenize' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\tokenize.py'>, 'token': <module 'token' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\token.py'>, '_weakrefset': <module '_weakrefset' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\_weakrefset.py'>, 'msvcrt': <module 'msvcrt' (built-in)>, '_winapi': <module '_winapi' (built-in)>, 'socket': <module 'socket' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\socket.py'>, '_socket': <module '_socket' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\DLLs\\_socket.pyd'>, 'selectors': <module 'selectors' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\selectors.py'>, 'select': <module 'select' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\DLLs\\select.pyd'>, 'numpy.core._dtype_ctypes': <module 'numpy.core._dtype_ctypes' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_dtype_ctypes.py'>, 'numpy.core._internal': <module 'numpy.core._internal' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\core\\_internal.py'>, 'ast': <module 'ast' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\ast.py'>, '_ast': <module '_ast' (built-in)>, 'numpy._pytesttester': <module 'numpy._pytesttester' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\_pytesttester.py'>, 'numpy.lib': <module 'numpy.lib' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\__init__.py'>, 'numpy.lib.mixins': <module 'numpy.lib.mixins' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\mixins.py'>, 'numpy.lib.scimath': <module 'numpy.lib.scimath' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\scimath.py'>, 'numpy.lib.type_check': <module 'numpy.lib.type_check' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\type_check.py'>, 'numpy.lib.ufunclike': <module 'numpy.lib.ufunclike' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\ufunclike.py'>, 'numpy.lib.index_tricks': <module 'numpy.lib.index_tricks' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\index_tricks.py'>, 'numpy.matrixlib': <module 'numpy.matrixlib' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\matrixlib\\__init__.py'>, 'numpy.matrixlib.defmatrix': <module 'numpy.matrixlib.defmatrix' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\matrixlib\\defmatrix.py'>, 'numpy.linalg': <module 'numpy.linalg' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\linalg\\__init__.py'>, 'numpy.linalg.linalg': <module 'numpy.linalg.linalg' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\linalg\\linalg.py'>, 'numpy.lib.twodim_base': <module 'numpy.lib.twodim_base' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\twodim_base.py'>, 'numpy.lib.stride_tricks': <module 'numpy.lib.stride_tricks' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\stride_tricks.py'>, 'numpy.linalg.lapack_lite': <module 'numpy.linalg.lapack_lite' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\linalg\\lapack_lite.cp37-win_amd64.pyd'>, 'numpy.linalg._umath_linalg': <module 'numpy.linalg._umath_linalg' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\linalg\\_umath_linalg.cp37-win_amd64.pyd'>, 'numpy.lib.function_base': <module 'numpy.lib.function_base' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\function_base.py'>, 'numpy.lib.histograms': <module 'numpy.lib.histograms' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\histograms.py'>, 'numpy.lib.nanfunctions': <module 'numpy.lib.nanfunctions' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\nanfunctions.py'>, 'numpy.lib.shape_base': <module 'numpy.lib.shape_base' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\shape_base.py'>, 'numpy.lib.polynomial': <module 'numpy.lib.polynomial' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\polynomial.py'>, 'numpy.lib.utils': <module 'numpy.lib.utils' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\utils.py'>, 'numpy.lib.arraysetops': <module 'numpy.lib.arraysetops' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\arraysetops.py'>, 'numpy.lib.npyio': <module 'numpy.lib.npyio' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\npyio.py'>, 'weakref': <module 'weakref' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\weakref.py'>, 'numpy.lib.format': <module 'numpy.lib.format' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\format.py'>, 'numpy.lib._datasource': <module 'numpy.lib._datasource' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\_datasource.py'>, 'numpy.lib._iotools': <module 'numpy.lib._iotools' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\_iotools.py'>, 'numpy.lib.arrayterator': <module 'numpy.lib.arrayterator' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\arrayterator.py'>, 'numpy.lib.arraypad': <module 'numpy.lib.arraypad' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\arraypad.py'>, 'numpy.lib._version': <module 'numpy.lib._version' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\lib\\_version.py'>, 'numpy.fft': <module 'numpy.fft' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\fft\\__init__.py'>, 'numpy.fft._pocketfft': <module 'numpy.fft._pocketfft' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\fft\\_pocketfft.py'>, 'numpy.fft._pocketfft_internal': <module 'numpy.fft._pocketfft_internal' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\fft\\_pocketfft_internal.cp37-win_amd64.pyd'>, 'numpy.fft.helper': <module 'numpy.fft.helper' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\fft\\helper.py'>, 'numpy.polynomial': <module 'numpy.polynomial' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\__init__.py'>, 'numpy.polynomial.polynomial': <module 'numpy.polynomial.polynomial' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\polynomial.py'>, 'numpy.polynomial.polyutils': <module 'numpy.polynomial.polyutils' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\polyutils.py'>, 'numpy.polynomial._polybase': <module 'numpy.polynomial._polybase' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\_polybase.py'>, 'numpy.polynomial.chebyshev': <module 'numpy.polynomial.chebyshev' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\chebyshev.py'>, 'numpy.polynomial.legendre': <module 'numpy.polynomial.legendre' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\legendre.py'>, 'numpy.polynomial.hermite': <module 'numpy.polynomial.hermite' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\hermite.py'>, 'numpy.polynomial.hermite_e': <module 'numpy.polynomial.hermite_e' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\hermite_e.py'>, 'numpy.polynomial.laguerre': <module 'numpy.polynomial.laguerre' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\polynomial\\laguerre.py'>, 'numpy.random': <module 'numpy.random' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\__init__.py'>, 'numpy.random._pickle': <module 'numpy.random._pickle' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_pickle.py'>, 'numpy.random.mtrand': <module 'numpy.random.mtrand' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\mtrand.cp37-win_amd64.pyd'>, 'cython_runtime': <module 'cython_runtime'>, 'numpy.random.bit_generator': <module 'numpy.random.bit_generator' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\bit_generator.cp37-win_amd64.pyd'>, '_cython_0_29_24': <module '_cython_0_29_24'>, 'numpy.random._common': <module 'numpy.random._common' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_common.cp37-win_amd64.pyd'>, 'secrets': <module 'secrets' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\secrets.py'>, 'base64': <module 'base64' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\base64.py'>, 'binascii': <module 'binascii' (built-in)>, 'hmac': <module 'hmac' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\hmac.py'>, '_hashlib': <module '_hashlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\DLLs\\_hashlib.pyd'>, 'hashlib': <module 'hashlib' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\hashlib.py'>, '_blake2': <module '_blake2' (built-in)>, '_sha3': <module '_sha3' (built-in)>, 'random': <module 'random' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\random.py'>, 'bisect': <module 'bisect' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\bisect.py'>, '_bisect': <module '_bisect' (built-in)>, '_random': <module '_random' (built-in)>, 'numpy.random._bounded_integers': <module 'numpy.random._bounded_integers' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_bounded_integers.cp37-win_amd64.pyd'>, 'numpy.random._mt19937': <module 'numpy.random._mt19937' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_mt19937.cp37-win_amd64.pyd'>, 'numpy.random._philox': <module 'numpy.random._philox' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_philox.cp37-win_amd64.pyd'>, 'numpy.random._pcg64': <module 'numpy.random._pcg64' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_pcg64.cp37-win_amd64.pyd'>, 'numpy.random._sfc64': <module 'numpy.random._sfc64' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_sfc64.cp37-win_amd64.pyd'>, 'numpy.random._generator': <module 'numpy.random._generator' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\random\\_generator.cp37-win_amd64.pyd'>, 'numpy.ctypeslib': <module 'numpy.ctypeslib' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\ctypeslib.py'>, 'numpy.ma': <module 'numpy.ma' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\ma\\__init__.py'>, 'numpy.ma.core': <module 'numpy.ma.core' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\ma\\core.py'>, 'inspect': <module 'inspect' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\inspect.py'>, 'dis': <module 'dis' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\dis.py'>, 'opcode': <module 'opcode' from 'C:\\Users\\25230\\AppData\\Local\\Programs\\Python\\Python37\\lib\\opcode.py'>, '_opcode': <module '_opcode' (built-in)>, 'numpy.ma.extras': <module 'numpy.ma.extras' from 'C:\\code\\CleanSkyLMSM\\env\\lib\\site-packages\\numpy\\ma\\extras.py'>}

#### 2. 验证编译环节，字节码文件生成

此外，在这个目录下，出现了一系列字节码文件，将其清空后再次import python，会重新生成对应的numpy字节码文件！

C:\code\CleanSkyLMSM\env\Lib\site-packages\numpy\__pycache__

![image-20220219121448934](C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220219121448934.png)

### .pyo文件

优化字节码文件，比.pyc文件的执行效率更高

### 未完待续

distutils

## 基础面向对象语法

### 类变量的声明，类的公共属性

> class Dog:
>
> 公有属性（所有的实例共用）
>
> ​	d_type = "京巴"
>
> ​	
>
> ​	def say_hi(self):
>
> ​		print("hello my name is " + self.d_type)
>
> 
>
> dog1= Dog()
>
> dog2= Dog()
>
> dog3 = Dog()
>
> print(dog1.d_type)
>
> dog1.say_hi()

公有属性可以在类外部直接修改，并且共用

Dog.d_type = "藏獒"

### 类的私有属性与构造器

id()函数查看对象地址？

私有属性

> def \__init\__(self,name,age):
>
> ​	print('hahahha',name,age)

如何保存记录私有属性？

> def \__init\__(self,name,age):
>
> ​	print('hahahha',name,age)
>
> ​	self.name = name
>
> ​	self.age = age

在类方法的参数列表中，self相当于实例本身，会携带实例的全部信息

> def say_hi(self):
>
> ​	print(self.d_type)

<img src="C:\Users\25230\AppData\Roaming\Typora\typora-user-images\image-20220126121741791.png" alt="image-20220126121741791"  />

### 术语明确

类属性，类变量，属于类，共享——通过对象调用和通过类调用都可以，且都可以修改

Dog.d_type

d1.d_type

**d1.d_type = ...** 这个操作会给d1实例创建新的实例属性d_type，类属性不会变！相当于self.d_type = ...

实例属性，实例变量，属于实例，只能通过实例来调用，且可以修改

d1.d_type = ...

### 对象之间交互

```python
class Person:

​	def \__init\__(self,blood,name):

​		self.blood = blood

​		self.name = name

​	def pat(self,***<u>dog</u>***):

​		dog.blood -= 100

​		print(self.name + "打了" dog.name + "Dog blood = " +dog.blood)



class Dog:

​	def \__init\__(self,blood,name):

​		self.blood = blood

​		self.name = name

​	def bit(self,**<u>person</u>**):

​		person.blood -= 100

​		print(self.name + "咬了" person.name + "Person blood = " +person.blood)



person = Person(300,"Houze")

dog = Dog(100,"藏獒")

person.pat(dog)

dog.bit(person)
```

Houze打了藏獒Dog blood = 0
藏獒咬了HouzePerson blood = 200

### 依赖关系

### 关联关系

在初始化的时候创建self.paterner = None

然后在创建完两个人的对象之后，将其中之一绑定到该属性上，即所谓关联关系，这种叫双向绑定

也可以创建一个新类叫做Relationship，再在人类中存放Relationship属性

def \__init\__ (self):

​	self.couple = []

def make_couple(self,obj1,obj2):

​	self.couple = [obj1,obj2]

​	print("maked couple")

### 组合关系

汽车零件和汽车，飞机零件和飞机。。。

组件本身独立但不能自己运行，必须跟宿主组合在一起

如何实现？在类的构造器里用类的构造器

person.wepon....

### 继承

class person(animal):

​	<u>**pass**</u>

默认继承父类的构造器

继承不仅可以继承父类的方法，也可以重写父类的方法

也可以重写类变量（和实例变量相对）！

### 重写父类方法

#### 重写普通方法

class Person(Animal):

​	def eat(self):

​		**<u>Animal.eat(self)</u>**			父类的eat

​		print("人在优雅地吃")

#### 重写构造方法

直接重写，完全回炉重造

```python
class Animal:
    def __init__(self,name,age):
        self.name = name
        self.age = age
        
class Person(Animal):
    def __init__(self, name, age):
        super().__init__(name, age)
```

<u>**charm告诉我如果想显示地重写子类构造器，必须调用父类构造器**</u>

super().

如果想要添加属性，那么也需要调用父类的构造器

```python
class Animal:
    def __init__(self,name,age):
        self.name = name
        self.age = age

class Person(Animal):

    def __init__(self, name, age, blood):
        super().__init__(self, name, age)
        self.blood = blood
```

需要注意的是，子类的构造器在调用父类的构造器时，需要传入self，这样在父类构造器中，可以将属性绑定到子类实例上！

super(子类类名,self).\__init\__(不加self.....)

### 多继承