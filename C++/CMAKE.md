# CONTENT

- [](#)
- [CMAKE简介](#cmake简介)
- [0.使用CMAKE进行编译的步骤](#0使用cmake进行编译的步骤)
- [1.同一目录单个源文件](#1同一目录单个源文件)
- [2.同一目录多个源文件](#2同一目录多个源文件)
  - [`aux_source_directory`自动添加源文件](#aux_source_directory自动添加源文件)
- [3.](#3)


# CMAKE简介
>write once, run anywhere
只需编写一个版本的cmakelist.txt可以跨平台编译

# 0.使用CMAKE进行编译的步骤
1. 编写cmakelist.txt指定编译顺序
2. 使用`cmake <PATH>`生成`makefile`
`PATH`是cmakelist.txt所在的目录
3. 使用`make`进行编译

`cmake_minimum_required`指定CMAKE最低版本
`projet`参数指定命令名称
`add_executable(Demo main.cc)`将`main.cc`编译成`Demo`这个可执行文件

# 1.同一目录单个源文件

```cmake
# 最低版本号要求
cmake_minimum_required(VERSION 3.16.3)

# 项目信息
project(Demo2)

# 指定生成目标（objname sourcefile__code...）
add_executable(Demo1 calcul_sqrt.c)
```

# 2.同一目录多个源文件
```cmake
# 最低版本号要求
cmake_minimum_required(VERSION 3.16.3)

# 项目信息
project(Demo2)

# 指定生成目标（objname sourcefile__code...）
add_executable(Demo2 calcul_sqrt.c my_pt.c)
```

## `aux_source_directory`自动添加源文件

```cmake
# 最低版本号要求
cmake_minimum_required(VERSION 3.16.3)

# 项目信息
project(Demo2)

# 使用aux_source_directory查找指定目录下的所有源文件
# aux_source_directory(<dir> <variable>)
aux_source_directory(. DIR_SRCS)

# 指定生成目标（objname sourcefile__code...）
add_executable(Demo2 ${DIR_SRCS})
```

# 3.多目录多源文件

>如果将一部分头文件和源文件整合到math文件夹下，该如何调整cmake以正常编译？

需要在根目录和math目录下分别编写CMakeLists.txt文件，先将math文件夹中的文件编译成静态库再由main函数调用

**在项目根目录下：**

1. 将根目录中的包含main函数的源文件转化成目标文件Demo`add_executable(Demo main.cc)`
2. 使用`target_link_libraries(Demo Library_name...)`指令将库文件和本地的obj文件链接

**在库文件的根目录下：**

1. 创建新的`CMakeLists.txt`
2. 使用`add_library(Library_name source_files_set)`将该目录下的源文件打包成静态库文件