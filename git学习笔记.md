## Git 学习笔记

### 创建仓库

+ 创建repository，可以理解为一个目录，此目录下的所有文件都可以被Git管理。
+ 首先创建一个空目录，命令：**mkdir** gitrepository
+ 将此目录（gitrepository）变为Git管理的仓库，命令：**git init**
+ 添加文件到仓库，命令：**git add** test.md
+ 提交文件到仓库，命令：**git commit -m** "8.21commit"
+ ![1](C:\Users\Mr.hao\Desktop\images\1.jpg)



### 版本穿梭

+ 查看当前仓库的状态，命令：**git status**
+ ![2](C:\Users\Mr.hao\Desktop\images\2.jpg)
+ 修改后的文件，可以查看其修改的内容，命令：**git diff** test.md
+ ![3](C:\Users\Mr.hao\Desktop\images\3.jpg)
+ 查看文件修改的版本，显示从最近到最远的提交日志，命令：**git log** 或者 **git log --pretty=oneline**
+ ![4](C:\Users\Mr.hao\Desktop\images\4.jpg)
+ ![5](C:\Users\Mr.hao\Desktop\images\5.jpg)
+ Git中，用**HEAD**表示当前版本，上一个版本用**HEAD^**，上上一个版本就是**HEAD^^**，往上100个版本写成**HEAD~100**。比如，回退到上一个版本，命令：**git reset --hard HEAD^**
+ ![6](C:\Users\Mr.hao\Desktop\images\6.jpg)
+ 查看工作区文件的内容，命令：**cat** test.md
+ ![7](C:\Users\Mr.hao\Desktop\images\7.jpg)
+ Git提供了一个命令 **git reflog** 用来记录每一次提交的命令，通过此命令，可以查到commit id，利用commit id 可以穿梭与各个提交的版本之间，命令：**git reset  --hard** 70e2a，此处70e2a是某个提交版本commit id
+ ![8](C:\Users\Mr.hao\Desktop\images\8.jpg)
+ ![9](C:\Users\Mr.hao\Desktop\images\9.jpg)

### 管理修改

+ Git跟踪并管理的是修改，而非文件。

+ 什么是修改呢？

  >比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

+ 举个例子：对 test.md 添加一行，执行 **git add test.md** 命令，再对 test.md 添加一行，执行 **git commit** 命令，结果如下：

+ ![10](C:\Users\Mr.hao\Desktop\images\10.png)

+ 如上图所示，执行命令 **git status** 后发现第二次的修改并没有提交，这是因为，第一次修改后执行命令 **git add**，将第一次修改添加到了暂存区，接着执行了 **git commit** 提交到了master，但是第二次修改并没有添加到暂存区，所以没有提交到master。因此，需要将第二次修改添加到暂存区，即执行命令 **git add**，再执行**git commit**

### 撤销修改

* 当你对工作区的文件修改后，想直接丢弃掉工作区的修改时，用命令 **git checkout --file**
* 当你对工作区的文件修改后并且添加到了暂存区，想丢弃修改时，首先，用命令 **git reset HEAD file** 回到工作区，然后再用命令 **git checkout --file** 丢弃修改。

###  删除文件

* 当我们在工作区删除文件后，Git知道删除了文件，因此，工作区和版本库中的文件不同，通过 **git status** 可以知道删除了哪些文件。
* ![11](C:\Users\Mr.hao\Desktop\images\11.png)
* 此时，有两种做法。第一种就是从版本库中删掉该文件，用命令 **git rm** hei.md，并且 **git commit**
* ![12](C:\Users\Mr.hao\Desktop\images\12.png)
* 第二种做法是，如果你误删了该文件，可以用 **git checkout -- file** 将文件恢复到最新版本。

### 远程仓库

+ 将Github作为远程仓库，与本地Git仓库进行连接。Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以需要创建SSH Key，命令：ssh-keygen -t rsa -C "your email"，然后一路回车，使用默认值即可。
+ ![13](C:\Users\Mr.hao\Desktop\images\13.png)
+ 登录github，打开setting，找到SSh Keys，点击 New SSh key，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，这样就添加好了SSh。
+ 在github中创建新的仓库，如：learning-note，此仓库是空的。
+ 现在，把本地的learning-note仓库与github上的learning-note关联起来，命令：**git remote add origin https://github.com/Mrtianhao/learning-note.git**

