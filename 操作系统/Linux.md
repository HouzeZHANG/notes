# 鸟哥的LINUX

- [鸟哥的LINUX](#鸟哥的linux)
- [第一部分Linux的规则与安装](#第一部分linux的规则与安装)
  - [Day1第0章 计算机概论](#day1第0章-计算机概论)
    - [CPU的指令集架构](#cpu的指令集架构)
    - [20M/5M光纤传输速度](#20m5m光纤传输速度)
    - [计算机的五大单元](#计算机的五大单元)
    - [为什么购买的500G硬盘在格式化完成后只有460G左右的容量？](#为什么购买的500g硬盘在格式化完成后只有460g左右的容量)
    - [CPU速度和什么有关？](#cpu速度和什么有关)
    - [什么是CPU的外频和倍频？](#什么是cpu的外频和倍频)
    - [前端总线速度，位宽与字长](#前端总线速度位宽与字长)
    - [超线程Hyper-Threading](#超线程hyper-threading)
    - [SDRAM和DDRAM](#sdram和ddram)
    - [双通道设计——提高内存的带宽](#双通道设计提高内存的带宽)
    - [二级高速缓存](#二级高速缓存)
    - [ROM只读存储器COMS芯片与BIOS](#rom只读存储器coms芯片与bios)
  - [Day2第0章 计算机概论](#day2第0章-计算机概论)
    - [显卡](#显卡)
    - [如何计算需要的显存？](#如何计算需要的显存)
    - [HDMI和VGA之间的区别？](#hdmi和vga之间的区别)
    - [什么是扇区？](#什么是扇区)
    - [关于MySQL配置](#关于mysql配置)
  - [Day3（2022-01-21）第5章Linux的文件权限与目录配置](#day32022-01-21第5章linux的文件权限与目录配置)
    - [三种身份和三种操作权限](#三种身份和三种操作权限)
    - [用户组](#用户组)
    - [为什么su -无法切入ubuntu的root账户？](#为什么su--无法切入ubuntu的root账户)
    - [ls指令](#ls指令)
      - [五种文件类型](#五种文件类型)
      - [操作权限](#操作权限)
      - [用户群组](#用户群组)
      - [文件大小单位](#文件大小单位)
      - [关于文件名](#关于文件名)
    - [如何通过命令行来修改系统语言？](#如何通过命令行来修改系统语言)
    - [文件属性与权限的修改](#文件属性与权限的修改)
      - [chgrp](#chgrp)
      - [chown](#chown)
        - [cp](#cp)
      - [chmod](#chmod)
        - [数字法](#数字法)
        - [符号法（特别适用于不知道文件本来的权限）](#符号法特别适用于不知道文件本来的权限)
    - [目录与文件的权限比较（重点）](#目录与文件的权限比较重点)
        - [文件权限](#文件权限)
        - [目录权限](#目录权限)
  - [Day4（2022-01-22）第5章Linux的文件权限和目录配置](#day42022-01-22第5章linux的文件权限和目录配置)
    - [目录与文件的权限比较（重点）](#目录与文件的权限比较重点-1)
    - [Linux的文件种类与扩展名](#linux的文件种类与扩展名)
      - [regular file常规文件](#regular-file常规文件)
        - [纯文本文件ASCII](#纯文本文件ascii)
        - [二进制文件binary](#二进制文件binary)
        - [数据文件data file](#数据文件data-file)
      - [目录directory](#目录directory)
      - [链接文件link](#链接文件link)
      - [设备与设备文件device](#设备与设备文件device)
        - [区块文件block](#区块文件block)
        - [字符串设备文件character](#字符串设备文件character)
        - [串行端口的接口设备、键鼠](#串行端口的接口设备键鼠)
      - [数据接口文件sockets](#数据接口文件sockets)
      - [数据输送文件fifo,pipe](#数据输送文件fifopipe)
    - [关于Linux文件名的长度](#关于linux文件名的长度)
    - [FHS（FileSystem Hierarchy Standard）](#fhsfilesystem-hierarchy-standard)
    - [directory Tree目录树](#directory-tree目录树)
- [第三部分-学习shell与shell script](#第三部分-学习shell与shell-script)
  - [第十一章-正则表达式与文件格式化处理](#第十一章-正则表达式与文件格式化处理)
    - [re手册摘要](#re手册摘要)
    - [11.1 开始之前，什么是正则表达式](#111-开始之前什么是正则表达式)

# 第一部分Linux的规则与安装

## Day1第0章 计算机概论

### CPU的指令集架构

<u>RISC精简指令集</u>

Reduced instruction Set Computer

比如Oracle的SPARC

<u>CISC复杂指令集</u>

Complex Instruction Set Computer

比如x86架构，个人电脑多用x86架构的指令集



### 20M/5M光纤传输速度

下载20M上行5M



### 计算机的五大单元

算术与逻辑单元+内存+**控制单元**+输入设备+输出设备



### 为什么购买的500G硬盘在格式化完成后只有460G左右的容量？

因为硬盘制造商一般使用十进制为单位

而转化为数据容量后一般使用2的10次方为单位

硬盘的最小组成单位为sector扇区



### CPU速度和什么有关？

和指令集架构相关联

CPU的时钟频率是什么？外频*倍频



### 什么是CPU的外频和倍频？

CPU的外频指的是CPU和外部设备相连接时的频率

倍频指的是CPU内部的加速频率

外频*倍频 = CPU频率

通常被超频的是外频

Intel的turbo睿频技术是Intel研发的智能超频的技术



### 前端总线速度，位宽与字长

**前端总线速度**（FSB  Front side Bus）指的是**内存和内存控制芯片**之间的传输速度

$内存控制芯片对内存的工作频率*位宽 = CPU从内存中取得的最大带宽$

与总线位宽相似，CPU每次能够处理的数据量成为字长

字长有32位64位之分



### 超线程Hyper-Threading

在每一个CPU内部将重要的寄存器分成两组，让两个程序分别使用这两组寄存器，让这两个程序竞争使用CPU，达到CPU级别的进程调度而非操作系统级的进程调度


### SDRAM和DDRAM

Dynamic Random Access Memory动态随机存取内存是个人电脑的主要内存

SDRAM和DDRAM

DDRAM是double data RAM的缩写，双倍数据传输

内存的带宽 = 频率速度*位宽

SDRAM和DDRAM的内部频率一致，频率速度DDRAM是SDRAM的两倍！

### 双通道设计——提高内存的带宽

ps : 对于服务器来说，内存的容量有时比CPU的时钟频率还要重要

内存一般的带宽最大为64位，为了提升内存的带宽，将两块内存的总线一起使用



### 二级高速缓存

因为数据在CPU和内存之间传输需要经过**内存控制器**，会花更多的时间

如果直接在CPU内部放置**L2 cache**二级缓存，由此L2的频率和CPU保持一致，一般由SRAM实现，中文名叫**静态随机存储器**



### ROM只读存储器COMS芯片与BIOS

CMOS记录硬件的参数与是否应该启用

BIOS basic Input Output System 该系统过去写死到ROM中，现在一般会写入闪存中以便于（固件）更新，每次开机时现读取ROM中的BIOS

## Day2第0章 计算机概论

### 显卡

显存，显卡的内存

GPU，专门用于3D运算的处理器

### 如何计算需要的显存？

$屏幕分辨率\cdot每个像素占用的内存\cdot刷新率 = 显存最低要求$

### HDMI和VGA之间的区别？

HDMI能同时传输视频和声音，VGA只能传输视频信号

### 什么是扇区？

同心圆面上切出的小区块

外围的圆会有更多的扇区，所以数据的读写通常会从外圈开始往内写

高容量硬盘每个扇区有4kb

### 关于MySQL配置

一般来说不允许远程登录root账户，只允许localhost登录root账户，因为这样确保了root账户的安全

## Day3（2022-01-21）第5章Linux的文件权限与目录配置

### 三种身份和三种操作权限

owner，group，others

read，write，execute

### 用户组

每个账号可以同时属于多个用户组

账户信息记录在/etc/passwd

个人密码记录在/etc/shadow

### 为什么su -无法切入ubuntu的root账户？

因为在Ubuntu中root账户默认是**disable**的

可以使用sudo -i来切入root

root账户~#

普通账户~$

### ls指令

list，显示文件的文件名与相关属性，-al，列出所有文件的详细熟悉

`drwx------  4 root root 4096 janv. 21 20:45 .`
`drwxr-xr-x 20 root root 4096 janv. 20 02:43 ..`
`-rw-------  1 root root   28 janv. 21 20:45 .bash_history`
`-rw-r--r--  1 root root 3106 déc.   5  2019 .bashrc`
`drwx------  2 root root 4096 août  19 12:41 .cache`
`-rw-------  1 root root  142 janv. 21 11:20 .mysql_history`
`-rw-r--r--  1 root root  161 déc.   5  2019 .profile`
`drwxr-xr-x  4 root root 4096 janv. 20 01:59 snap`

文件类型+文件权限+链接数（**有多少文件链接到此节点的inode**）+文件拥有着owne+文件所属用户组group+文件大小+文件最后被修改的日期+文件名

#### 五种文件类型

normal file[-]，link file[|]，directory[d],外围存储设备[b]，串行端口设备[c]（键盘鼠标）

> In [computing](https://en.wikipedia.org/wiki/Computing), a **directory** is a [file system](https://en.wikipedia.org/wiki/File_system) cataloging structure which contains references to other [computer files](https://en.wikipedia.org/wiki/Computer_file), and possibly other directories. 

#### 操作权限

r可读，w可写，x可执行

`d rwx --- ---`

三个为一组，1+3*3总共10个标识符，分别代表文件拥有者的权限，加入此用户组的账号的权限和非本人且没有加入用户组的其他账号的权限

root基本上不受系统权限的限制，无论文件的权限是什么，默认root都可以读写

#### 用户群组

新建projecta群组，讲class1，class2，class3加入projecta群组

如果文件的详细信息中显示所属projecta群组，那么class1-3的权限对应5-7位

#### 文件大小单位

`drwx------  4 root root 4096 janv. 21 20:45 .`

单位为bytes字节，.文件（目录）的大小为4096字节

#### 关于文件名

如果文件名前有.，则意味着文件为隐藏文件

`ls`

`ls -a`

### 如何通过命令行来修改系统语言？

略

### 文件属性与权限的修改

#### chgrp

group必修在**/etc/group**中存在才可以

`root@houzezhang-ThinkPad-X1-Carbon-6th:/home# chgrp root houzezhang/`

`chgrp [-R] new_group file_name`

[-R] 意味着是否是递归修改所有子文件和目录

#### chown

own所有者必须在**/etc/passwd**文件中出现

> chown owner_name file_name
>

chown实现修改用户群组

> chown user.group file_name
>

用chown同时修改群组

> chown .sshd initial-setup-ks.cfg
>
> chgrp sshd initial-setup-ks.cfg
>

##### cp

> cp 源文件 目标文件
>

将.bashrc这个文件复制成.bashrc_test，且传送给bin这个人

> root@houzezhang-ThinkPad-X1-Carbon-6th:/etc# cp bash.bashrc bash.bashrc_test
>
> -rw-r--r--   1 root root    2319 Feb 25  2020 bash.bashrc
> -rw-r--r--   1 root root    2319 Jan 21 22:35 bash.bashrc_test

cp指令会把权限和设置都完全复制，所以在复制之后需要修改文件权限，但是该文件还是属于root，所以bin用户无法修改该文件的所有权，必须由root修改

> chown bin bash.bashrc_test
>

#### chmod

##### 数字法

rwx的权分别为421，每种身份的权各自累加，组成一个三位8进制数

> chmod [-R] 三位八进制数 文件或目录
>

> root@houzezhang-ThinkPad-X1-Carbon-6th:/etc# chmod 777 bash.bashrc_test 
>

> root@houzezhang-ThinkPad-X1-Carbon-6th:/etc# ls -l bash.bashrc_test 
> -rwxrwxrwx 1 root root 2319 Jan 21 22:35 bash.bashrc_test

##### 符号法（特别适用于不知道文件本来的权限）

ugoa代表四种身份

rwx代表三种权限

+-=代表加入，移除，设置

> chmod u=rwx,go=rx .bashrc
>

### 目录与文件的权限比较（重点）

> drwxr-xr-x  2 houzezhang houzezhang 4096 Jan 20 03:46 Desktop
>

##### 文件权限

> A **computer file** is a [computer resource](https://en.wikipedia.org/wiki/System_resource) for recording [data](https://en.wikipedia.org/wiki/Data_(computing)) in a [computer storage device](https://en.wikipedia.org/wiki/Computer_data_storage), primarily identified by its [file name](https://en.wikipedia.org/wiki/Filename). **Just as words can be written to paper, so can data be written to a computer file.** Files can be edited and transferred through the Internet on that particular computer system.
>
> Different [types of computer files](https://en.wikipedia.org/wiki/File_format) are designed for different purposes. A file may be designed to store a [Image](https://en.wikipedia.org/wiki/Digital_image), a written message, a [video](https://en.wikipedia.org/wiki/Digital_video), a [computer program](https://en.wikipedia.org/wiki/Computer_program), or any wide variety of other kinds of data. Certain files can store multiple data types at once.
>
> **By using computer programs, a person can open, read, change, save, and close a computer file.** Computer files may be reopened, modified, and [copied](https://en.wikipedia.org/wiki/File_copying) an arbitrary number of times.
>
> Files are typically organized in a [file system](https://en.wikipedia.org/wiki/File_system), which tracks file locations on the disk and enables user access.

文件是存放数据的集合

read：可以读取此文件的实际内容

write：编辑，新增，修改文件的内容（**但不包括删除**）

execute：可以被执行的权限

##### 目录权限

> In [computing](https://en.wikipedia.org/wiki/Computing), a **directory** is a [file system](https://en.wikipedia.org/wiki/File_system) **cataloging structure which contains references to other [computer files](https://en.wikipedia.org/wiki/Computer_file)**, and possibly other directories. 

目录记录文件名

r：可以获取目录结构，即用ls来查看文件列表（read contents in directiry）

w：具有改动目录结构的权限，新建文件与目录，**删除文件与目录**（不论文件的权限是什么），修改文件和目录的名字，移动该目录内的文件和目录（modify contents if directory）

x：是否能将该目录作为工作目录（work directory）是否能cd进该目录（access directory）

## Day4（2022-01-22）第5章Linux的文件权限和目录配置

### 目录与文件的权限比较（重点）

> drwxr--r-- 2 root       root          4096 Jan 23 02:03 testing
>
> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp$ ls -l testing/
> ls: cannot access 'testing/testing': Permission denied
> total 0
> -????????? ? ? ? ?            ? testing

对于只能read的目录，如果适用ls指令，则会显示cannot access该目录，只能查询文件名

> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp$ cd testing/
> bash: cd: testing/: Permission denied

显然，没有x执行的权限，无法cd进入该目录

> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp$ cd testing/
> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp/testing$ dir
> testing
> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp/testing$ ls -l
> total 0
> -rw------- 1 root root 0 Jan 23 02:03 testing
>
> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp/testing$ rm testing 
> rm: remove write-protected regular empty file 'testing'? y
> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/tmp/testing$ ls

在houzezhang成为该目录的owner之后，不仅能够cd进入该目录，还可以**删除**该目录下owner为root的testing文件！因为owner有x和w的权限

如果目录没有r权限，但有wx，依然可以做很多事情，比如作为cp的目标文件夹。如果没有r权限，那么无法进行tab补全。

### Linux的文件种类与扩展名

#### regular file常规文件

##### 纯文本文件ASCII

> cat ~/.bashrc

##### 二进制文件binary

可执行文件（但不包括脚本！）

> cat命令本身就是一个二进制文件！

##### 数据文件data file

> cat /var/log/wtmp

#### 目录directory

#### 链接文件link

#### 设备与设备文件device

集中在/dev文件下

##### 区块文件block

以提供随机存储的接口设备

> houzezhang@houzezhang-ThinkPad-X1-Carbon-6th:/$ ls -l /dev/sda
> brw-rw---- 1 root disk 8, 0 Jan 21 15:51 /dev/sda

##### 字符串设备文件character

##### 串行端口的接口设备、键鼠

#### 数据接口文件sockets

#### 数据输送文件fifo,pipe

基本上Linux的文件扩展名是给用户了解文件可能的用途而已，能否被执行取决于x权限，而能否被成功执行取决于文件的内容

### 关于Linux文件名的长度

一般为255个字节，也就是255个ASCII码或者128个汉字

### FHS（FileSystem Hierarchy Standard）

usr = UNIX Software Resource

略

### directory Tree目录树

目录树的起始点为/根目录

**每个目录不止能使用本地分区的文件系统，也可以使用网络上的文件系统，比如可以使用NFS服务器来挂载某特定目录**

每一个文件在次目录树中的文件名都是独一无二的

**相对路径——不以根目录开头的路径**

**绝对路径——以根目录开头的路径**

# 第三部分-学习shell与shell script

## 第十一章-正则表达式与文件格式化处理

Regular expression正则表达式
用于在管理主机的时候，精简处理日常事务

### re手册摘要

[Python re 文档](https://docs.python.org/zh-cn/3/library/re.html)

正则表达式可以拼接

|符号|效果|案例|
|---|---|---|
|`.`|任意字符||
|`^`|开头||
|`$`|串尾或者串尾`\n`之前的字符||
|`*`|对其前面的正则符号匹配零到无数次|`ab*`意味着`a`,`abb`|
|`+`|一到无数次（和`*`相对）||
|`?`|有或无||
|`{m}`|匹配至少m次重复||
|`{m, n}`|上下界，可以只写`m`或`n`其一||
|`[]`|字符集合|`[a-z]`,`[0-5]`,`[a\-z]`（转义`-`）|
|`|`|正则表达式1或者正则表达式2|`RE1|RE2`|



### 11.1 开始之前，什么是正则表达式

`cp`,`ls`并不支持正则表达式，他们只支持linux的**通配符**（**wild card**），wild card通配符只是linux bash操作接口的一个功能