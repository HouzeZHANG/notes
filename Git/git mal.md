# Git_manual

## 0实战

### `git pull`和`git fetch`的区别

`git pull` = `git fetch` + `git merge`

### 如何删除远程分支

`git push origin :newOne`

## 1开始

### 1.1

>Une gestionnaire de version est un système qui enregistre l'évolution d'un fichier ou d'un ensemble de fichiers au cours du temps de manière à ce qu'on puisse **rappeler** une version **antérieure** d'un fichier à tout moment. Version control system en anglais.  Il vous permet de ramener un fichier à un état précedent, de ramener le projet complet à un état précedent, de **visualiser les changements** au cours du temps. Utiliser un VCS signifie aussi géneralement que si vous vous trompez ou que vous perdez des fichiers, vous pouvez facilement revenir à un état stable.

|一些词汇表达||
|---|---|
|la gestion de version|版本管理|
|système de gestion de version distribués|分布式版本管理系统|

>分布式版本管理系统可以 dupliquer complèment le dépot d'un des clients peut être copié sur le serveur pour le restaurer

## 3git分支

### 3.1分支简介

Git保存的不是文件的变化或者差异，而是一系列不同时刻的**快照**

在进行提交操作的时候，创建的commit object会保存一个指向快照的指针。commit object还会保存**提交者的信息**以及指向它**父对象**的指针。

![commit操作之后Git仓库中的状态](https://git-scm.com/book/en/v2/images/commit-and-tree.png)

**blob对象**保存**文件快照**  
**树**对象记录**目录结构**和**blob对象索引**  
**提交对象**包含指向前一个**树对象的指针**和**提交信息**  

git的分支本质上是**指向提交对象commit object的可变指针**，正因为如此，分支的创建和销毁都异常高效（40个字符+1个换行符，**长度为41个字符的校验和**）

默认分支名称为**master**

#### 分支创建与切换

`git branch testing`
在当前的提交对象上创建一个指针

![](https://git-scm.com/book/en/v2/images/two-branches.png)


`git checkout testing`
切换分支到testing分支

`git checkout -b <newbranchname>`
创建新分支+切换分支

`git branch -v`
查看所有分支的最后一次提交

#### HEAD指针

指向**当前所在的本地分支**的指针

`git log --decorate`

查看不同分支所指向的commit object

### 3.2分支的新建与合并

如何修复线上发布版的bug？

**切回master分支，创建新分支，提交修改，切换回master，merge新分支，删除新分支，切换回开发分支iss53**

`git merge iss53`
将当前分支merge到iss53这个commit版本

`git merge`会有不同的情况发生，如果merge的分支是当前分支的直接后继，那么git会将当前分支**fast-forward**到目标分支，因为不需要解决冲突

![](https://git-scm.com/book/en/v2/images/basic-branching-5.png)
如图所示，master分支本来指向C2，fast-forward到C4的时候不需要解决冲突

`git branch -d <branchname>`
删除分支，将创建的hotfix分支删除，因为它在修复完bug之后已经没用了

#### 将hotfix分支merge到iss53分支

如果checkout到之前的版本，进行了一些修改，你想将这些修改归入当前的分支，可以checkout到当前分支，随后merge之前更新之后的branch

`(venv) houzezhang@ThinkPad-X1-Carbon-6th:~/Documents/code/CSLMSM$ git **merge issu1**
Merge made by the 'recursive' strategy.
 cleansky_LMSM/db_init/pg_db_initial.py | 5 +++--
 1 file changed, 3 insertions(+), 2 deletions(-)`

我在localdev上merge issu1分支，将issu1上对数据库的修改更新到localdev上

总之，merge之前需要checkout到你**想要合并更新的分支**


#### 三方合并

![](https://git-scm.com/book/en/v2/images/basic-merging-1.png)

C5和C4并没有公共的祖先节点，所以git使用三方合并，比较C4，C5和C2三个commit，随后git会创建一个新的提交，被称为**合并提交**C6

![](https://git-scm.com/book/en/v2/images/basic-merging-2.png)

#### 遇到冲突时的分支合并

冲突原因，对**同一段代码**做了**不同的修改**

### 3.3分支管理

`git branch --merged`
`git branch --no-merged`
分别显示已经被合并的分支，和所有未被合并的分支

一般来说，git不允许用户删除未被合并的分支

### 3.4Git分支-分支开发工作流


#### 长期分支

![](https://git-scm.com/book/en/v2/images/lr-branches-2.png)

使用不同的流水线隔离不同稳定性的版本

#### 主题分支

略

### 3.5远程分支

拉取远程分支之后，本地git仓库会自动创建**远程跟踪分支**，且取名为**origin/master**

![克隆之后的服务器与本地仓库](https://git-scm.com/book/en/v2/images/remote-branches-1.png)


`git fetch <server>`
`fetch`指令会将目标服务器上的数据拉取到本地git仓库，就算出现分叉，也没有关系，origin/master会标记目标服务器当前的master分支，origin/master分支好似一个**书签**，这个书签不可修改，一般的工作流是checkout到这个分支，然后创建新分支进行开发；亦或是对该分支进行merge操作
![](https://git-scm.com/book/en/v2/images/remote-branches-3.png)

#### 多个远程仓库的情况

`git remote add <new server>`
添加新的远程仓库

![两个远程仓库的情形](https://git-scm.com/book/en/v2/images/remote-branches-4.png)

![fetch第二个远程仓库之后的情形](https://git-scm.com/book/en/v2/images/remote-branches-5.png)

可以看到，现在本地仓库同时记录了两个远程仓库的全部信息，两个远程跟踪分支同时由**server别名/master**标注，分得一清二楚哈哈

`git push remote branch`
将本地分支推送到某个远程服务器的某个分支

