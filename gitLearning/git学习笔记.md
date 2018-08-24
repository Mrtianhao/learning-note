## Git 学习笔记

### 创建仓库

+ 创建repository，可以理解为一个目录，此目录下的所有文件都可以被Git管理。
+ 首先创建一个空目录，命令：**mkdir** gitrepository
+ 将此目录（gitrepository）变为Git管理的仓库，命令：**git init**
+ 添加文件到仓库，命令：**git add** test.md
+ 提交文件到仓库，命令：**git commit -m** "8.21commit"
+ ![1](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/1.jpg)



### 版本穿梭

+ 查看当前仓库的状态，命令：**git status**
+ ![2](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/2.jpg)
+ 修改后的文件，可以查看其修改的内容，命令：**git diff** test.md
+ ![3](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/3.jpg)
+ 查看文件修改的版本，显示从最近到最远的提交日志，命令：**git log** 或者 **git log --pretty=oneline**
+ ![4](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/4.jpg)
+ ![5](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/5.jpg)
+ Git中，用**HEAD**表示当前版本，上一个版本用**HEAD^**，上上一个版本就是**HEAD^^**，往上100个版本写成**HEAD~100**。比如，回退到上一个版本，命令：**git reset --hard HEAD^**
+ ![6](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/6.jpg)
+ 查看工作区文件的内容，命令：**cat** test.md
+ ![7](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/7.jpg)
+ Git提供了一个命令 **git reflog** 用来记录每一次提交的命令，通过此命令，可以查到commit id，利用commit id 可以穿梭与各个提交的版本之间，命令：**git reset  --hard** 70e2a，此处70e2a是某个提交版本commit id
+ ![8](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/8.jpg)
+ ![9](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/9.jpg)

### 管理修改

+ Git跟踪并管理的是修改，而非文件。

+ 什么是修改呢？

  >比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

+ 举个例子：对 test.md 添加一行，执行 **git add test.md** 命令，再对 test.md 添加一行，执行 **git commit** 命令，结果如下：

+ ![10](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/0.png)

+ 如上图所示，执行命令 **git status** 后发现第二次的修改并没有提交，这是因为，第一次修改后执行命令 **git add**，将第一次修改添加到了暂存区，接着执行了 **git commit** 提交到了master，但是第二次修改并没有添加到暂存区，所以没有提交到master。因此，需要将第二次修改添加到暂存区，即执行命令 **git add**，再执行**git commit**

### 撤销修改

* 当你对工作区的文件修改后，想直接丢弃掉工作区的修改时，用命令 **git checkout --file**
* 当你对工作区的文件修改后并且添加到了暂存区，想丢弃修改时，首先，用命令 **git reset HEAD file** 回到工作区，然后再用命令 **git checkout --file** 丢弃修改。

###  删除文件

* 当我们在工作区删除文件后，Git知道删除了文件，因此，工作区和版本库中的文件不同，通过 **git status** 可以知道删除了哪些文件。
* ![11](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/11.png)
* 此时，有两种做法。第一种就是从版本库中删掉该文件，用命令 **git rm** hei.md，并且 **git commit**
* ![12](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/12.png)
* 第二种做法是，如果你误删了该文件，可以用 **git checkout -- file** 将文件恢复到最新版本。

### 远程仓库

+ 将Github作为远程仓库，与本地Git仓库进行连接。Git仓库和GitHub仓库之间的传输是通过SSh加密的，所以需要创建SSh Key，命令：ssh-keygen -t rsa -C "your email"，然后一路回车，使用默认值即可。
+ ![13](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/13.png)
+ 登录github，打开setting，找到SSh Keys，点击 New SSh key，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容，这样就添加好了SSh。
+ 在github中创建新的仓库，如：learning-note，此仓库是空的。
+ 现在，把本地的learning-note仓库与github上的learning-note关联起来，命令：**git remote add origin https://github.com/Mrtianhao/learning-note.git**; 再将本地库的所有内容推送到远程库上，命令:**git push -u origin master**
+ ![14](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/14.png)
+ 注：上面的Mrtianhao换成你的github账户名。

### 克隆远程库

* 我们要克隆远程库，比如这里克隆我的github账户下的仓库NLP-interview，命令： **git clone git@github.com:Mrtianhao/NLP-interview.git**，这里Mrtianhao换成你的github账户。
* ![15](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/15.png)
* 可以看到，我们成功克隆了NLP-interview仓库。

### 分支的创建、合并与删除

* 创建分支，命令：**git branch** new，new是分支名称；切换到新建的分支，命令：**git checkout** new
* 可以通过一条命令代替上述两条命令：**git checkout -b** new，创建并切换到new分支。
* ![16](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/16.png)
* 通过命令 **git branch** 可以查看当前所有分支：
* ![17](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/17.png)
* 现在切换到了新的分支new，对文件hei.md进行修改，然后通过命令 **git add** 和 **git commit** 提交，再切换到主分支master，查看hei.md，发现其中的内容并没有修改，这是因为我们再分支new上进行了提交，并没有再master上提交，现在，将new分支合并到master上，命令：**git merge** new
* ![18](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/18.png)
* 这时候我们在查看hei.md，可以看到内容已经修改。
* 合并完成后，删除new分支，命令：**git branch -d** new
* ![19](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/19.png)

### 解决分支合并中的冲突

* 首先，新建一个新的分支newbra，然后修改hei.md文件内容，再进行git add和git commit操作；切换到master分支上，对hei.md文件进行修改，再进行git add和git commit操作；将分支进行合并，结果如下图所示：
* ![20](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/20.png)
* 可以发现，合并分支时出现了冲突，通过git status可以查看当前状态：
* ![21](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/21.png)
* 这种情况必须手动解决冲突。我们可以对hei.md文件再一次进行修改，然后执行git add和git commit命令，这样就解决了冲突，结果如下：
* ![22](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/22.png)
* 可以看到冲突已解决。通过命令 git log --graph 可以看到分支合并图。
* ![23](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/23.png)
* 合并分支时，git会用Fast Forword模式，但这种模式下，删除分支后，会丢掉分支信息。因此，在合并分支时，可以使用参数 --no-ff，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
* ![24](https://github.com/Mrtianhao/learning-note/blob/master/gitLearning/images/24.png)
* 删除一个没有被合并国的分支，可以通过命令 **git branch -D <name>** 来实现。

### 多人协作

* 首先，用 **git push origin <branch-name>** 推送自己的修改。
* 如果推送失败，是因为远程分支比你的本地分支更新，需要 **git pull** 合并。
* 如果合并有冲突，则手动解决冲突，并在本地提交。
* 没有冲突或者解决冲突后，再用 **git push origin <branch-name>** 就能推送成功。
* 注：如果 **git pull** 提示 no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令 **git branch --set-upstream-to <branch-name> origin/<branch-name>**。
