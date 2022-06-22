# Cygwin

[什么是CygWin](https://zhuanlan.zhihu.com/p/56692626)

>All problems in computer science can be solved by another level of indirection. --David Wheeler
1. Cygwin是windows下的一个中间层，用于兼容POSIX
2. `.dll`的全称是`dynamic - link library`动态链接库
3. cygwin1.dll实现了POSIX系统调用的模拟层，原生Windows
4. cygwin上的应用程序编译后是Windows PE格式的可执行文件，且cygwin无法运行LinuxUnix环境下的二进制文件