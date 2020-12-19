## git ##

一、git工作区

git的工作区有三个或者四个。

三个工作区：工作目录、暂存区、本地资源库

四个工作区：工作目录、暂存区、本地资源库、远程资源库

> 工作目录：一般就是我们本地的文件，直接对其文件或内容进行修改
>
> 暂存区：stage/index，在.git文件下的index文件中
>
> 本地资源库：.git文件就是本地资源库
>
> 远程资源库：github、gitlab、gitee等这些都属于远程资源库

所以文件就会有上述资源的转变，工作目录-->暂存区、暂存区-->本地资源库、本地资源库-->远程仓库、远程仓库-->本地资源库、本地资源库-->暂存区、暂存区-->工作目录。所以，git的部分命令也就由此展开。

二、git安装

https://git-scm.com/	下载，然后安装->无脑下一步

三、git配置

git安装完成后，首先查看git的配置。

> git config -l 或 git config --list
>
> git config --system -l 或 git config --system --list ，查看git系统配置
>
> git config --global -l 或 git config --global --list，查看git全局配置

例图：

<img src="../images/git/git1-config.png" alt="git1-config" style="zoom:67%;" />

其实git的配置就是一个文件内容。

git config --system -l ,git的system级别的日志在 C:\Program Files\Git\etc\gitconfig中

![git2-systemconfig](../images/git/git2-systemconfig.png)

git config --global -l ,git的global级别的日志在 C:\Users\Administrator\.gitconfig中

![git3-globalconfig](../images/git/git3-globalconfig.png)

四、git添加用户名和邮箱

添加用户名和邮箱分为全局和项目级别。添加方式可以使用命令行方式，也可以直接修改文件。

1、全局添加

> 命令行方式

git config --global user.name "张三"

git config --global user.email "张三@mail"

> 修改文件方式

打开C:\Users\Administrator\\路径下的.gitconfig文件，添加即可

2、项目级别

> 命令行方式，需要先init一个git仓库。cmd，进入到该项目中。

git config user.name "李四"

git config user.email "李四@mail"

我们可以打开该仓库中隐藏文件夹.git/config文件

<img src="../images/git/git4-projectconfig.png" alt="git4-projectconfig" style="zoom:80%;" />

> 修改文件方式

也可以直接打开仓库中的隐藏文件夹.git/config文件，添加name和email即可。

五、ssh key

我们为git设置好了name和email，其实已经可以使用了。但是为什么还需要生成秘钥呢？

如果不设置秘钥，那么在我们每次操作文件(提交、拉取等)时，经常需要我们输入用户名和密码。为了方便操作，需要生成一个免密操作的秘钥。

> ssh-keygen

使用上面的命令，就会生成两个秘钥文件，一个私钥，一个公钥。

![git5-key](../images/git/git5-key.png)

id_rsa：是私钥，id_rsa.pub：公钥

将公钥信息添加到远程仓库即可进行免密操作。

六、初始化一个仓库

初始化仓库有两种方式，

> git init，在本地初始化一个仓库
>
> git clone，从远程仓库中克隆一个仓库

七、文件在各区域内的流向

前面我们说过，git的工作区有3个或者4个，分别是工作目录、暂存区、本地资源库、远程资源库。

我们怎么样将一个文件层层流转呢？

<img src="..\images\git\git6-filechange.png" alt="git6-filechange" style="zoom:67%;" />

根据上图，我们可以学习几个命令

git add：git add  filename 或 git add ./（将所有文件添加到暂存区）

git commit：git commit -m“desc”，将暂存区中的文件添加到本地仓库

git push：git push git地址 分支，将本地仓库中的内容添加到远程仓库

git pull：git pull git地址 分支，将远程仓库中的内容拉取到本地仓库

git reset：git reset hash值，回退到指定版本

git checkout：git checkout --filename 取消暂存，或者git restore --staged filename----------------

八、文件状态

文件的状态有四种，未跟踪、未修改、已修改、已暂存

untracked：未跟踪，不受git管理。在工作空间中，新增一个文件，这个文件状态就是untracked。

unmodify：已入库，未修改，文件内容与仓库中一致。将暂存区的文件使用git commit命令提交到本					 地仓库中，文件状态就是unmodify。

modify：已修改。修改工作目录中已经提交的文件，此时文件就是modify。

staged：已添加至暂存区。将新增的文件使用git add filename，此文件状态变为staged。

<img src="D:\a-github\MianShi\images\git\git7-filestatus.png" alt="git7-filestatus" style="zoom:80%;" />

可以通过git status 或者 git status filename查看具体文件的状态

九、版本前进和后退

git的版本前进和后退有三种方式，分别是索引值、^ 、~ 。推荐使用索引值方式，所以就不在介绍^和~的方式。

首先使用git log，查看提交的日志信息。空格下页，b上页，q退出。

<img src="D:\a-github\MianShi\images\git\git8-gitlog.png" alt="git8-gitlog" style="zoom:80%;" />

**commit 7c75871790350db41d79e1f7e107de8954790fac (HEAD -> master)** 

解释：7c75871790350db41d79e1f7e107de8954790fac 就是索引值，根据文件获取对应的hash值作为本次的索引。HEAD -> master，HEAD是指针，指向master分支，表示指向最新的commit提交位置。



git reflog，更加直观的查看提交信息

<img src="D:\a-github\MianShi\images\git\git9-reflog.png" alt="git9-reflog" style="zoom:80%;" />

**7c75871 (HEAD -> master) HEAD@{0}: checkout: moving from hot_fix to master**

解释：7c75871，就是一个hash值的前7位。HEAD -> master，HEAD是指针，指向master分支，表示指向最新的commit提交位置。HEAD@{0}，表示从当前版本退回到其他版本的值，如从7c75871退回到85f6598版本需要三步。

git reset --hard 索引值，就可以直接前进或回退到指定版本。

<img src="D:\a-github\MianShi\images\git\git10-getreset.png" alt="git10-getreset" style="zoom:80%;" />

从上图，我们可以看到版本已经退回到08a5a26版本。

<img src="D:\a-github\MianShi\images\git\git17.png" alt="git17" style="zoom:50%;" />

git reset 有三个参数

​	--soft，仅仅在本地库移动head指针

​	--mixed，本地库和暂存区都移动head指针

​	--hard，本地库和暂存区和工作空间都移动head指针

版本回退作用：在我们本地库中的一个文件被删除了，怎么找回来呢？我们可以退回到该文件还存在的版本，找到该文件后，在前进到最新版本就可以。



十、分支

git branch -v，查看所有的分支

<img src="D:\a-github\MianShi\images\git\git11-gitbranch.png" alt="git11-gitbranch" style="zoom: 67%;" />



git branch branchname，创建一个新的分支

<img src="D:\a-github\MianShi\images\git\git12-gitbranch.png" alt="git12-gitbranch" style="zoom: 67%;" />



git checkout branchname，切换分支

<img src="D:\a-github\MianShi\images\git\git13-gitcheckout.png" alt="git13-gitcheckout" style="zoom: 67%;" />



git merge branchname，分支合并

现在两个分支A和B，想把B分支合并到A上，需要先切换到A分支上，git merge B进行合并。

合并冲突：合并代码时，难免会出现文件内容冲突问题。

创建A分支，并在文件最后一行添加内容

<img src="D:\a-github\MianShi\images\git\git14.png" alt="git14" style="zoom:67%;" />

创建B分支，并在文件最后一行添加内容

<img src="D:\a-github\MianShi\images\git\git15.png" alt="git15" style="zoom:67%;" />

切换到A分支下，将B分支合并到A分支上。发生了冲突。

<img src="D:\a-github\MianShi\images\git\git16.png" alt="git16" style="zoom:67%;" />

什么意思呢？HEAD表示当前分支的内容，从<<<<<< 到 =====之间

==== 到 >>>>之间的内容是合并的分支内容。

发生冲突后，只需要修改此文件，删除不需要的内容，git add添加到暂存区中，

git commit -m"merge commit" ,此时不需要携带文件名。

十一、远程分支推送和拉取

git remote add 别名 仓库地址，为远程仓库地址创建一个别名

git push 仓库 分支，推送

git pull，拉取，git pull=git fetch + merge，

git fetch，只是将远程仓库地址拉取到本地仓库中，并没有修改我们工作目录中的内容。

git checkout 远程仓库/分支 切换到从远程仓库拉取下来的分支上，就可以查看拉取下来的内容

git merge ，将本地仓库内容与工作目录的内容进行合并

git fetch 仓库地址 分支

git checkout 仓库地址/分支

git merge 仓库地址/分支



十二、标签

当我们进行版本的前进后后退，是怎么样操作呢？

git reset --hard 索引值，索引值？一串hash值，你能记住吗？所以，这时候，标签就发挥用处了。

git tag，查看所有的标签

git tag tagname，为最近一次的commit创建tag

git show tagname，查看tag的详细信息

<img src="D:\a-github\MianShi\images\git\git18.png" alt="git18" style="zoom: 50%;" />

git tag tagname 索引值，为指定的提交创建tag

git tag -d tagname，删除指定标签

git push 仓库地址 tagname，提交指定标签

git push 仓库地址 --tags，提交所有的标签

git push 仓库地址:refs/tags/tagname，删除远程标签



十三、暂存区和本地仓库在哪里？

暂存区和本地仓库以及工作目录都是在我们的本地电脑上，工作目录我们都知道，但是暂存区和本地仓库在哪里呢？

当我们在使用git init 初始化一个git仓库后，只清楚git自动给我们创建了一个.git文件，并没有去关注他的结构，现在我们先看下.git文件结构目录。

<img src="D:\a-github\MianShi\images\git\git19.png" alt="git19" style="zoom:67%;" />

1、hooks，里面是git提供的命令脚本

2、info，存放仓库的一些信息

3、logs，记录每次跟新的操作。HEAD文件内容如下：![git20](D:\a-github\MianShi\images\git\git20.png)

看到这个文件，是不是发现，这些就是我们git log展示的信息。

4、objects，保存git的所有对象

可以根据每次提交生成的hash值与objects中的一个文件对应。

<img src="D:\a-github\MianShi\images\git\git21.png" alt="git21" style="zoom:50%;" />

也就是说，我们每次提交，都会生成一个object对象与之对应。

5、refs

<img src="D:\a-github\MianShi\images\git\git22.png" alt="git22" style="zoom:50%;" />

heads/master文件存储了当前最新的hash值

tags，有没有很熟悉，firsttag就是我们创建的标签，firsttag文件内也存储了与之对应的hash值

6、COMMIT_EDITMSG，最近一次提交的commit的信息

7、config，项目级别文档配置文件

8、description，仓库的描述信息

9、HEAD，映射ref引用，最新一次提交操作的hash值

HEAD文件内容：ref: refs/heads/master，指向了master文件。

<img src="D:\a-github\MianShi\images\git\git23.png" alt="git23" style="zoom: 50%;" />

10、index，暂存区stage

11、ORIG_HEDA，HEDA指针的前一个版本hash值(最新一次提交操作的前一次提交操作的hash值)



查看暂存区的内容git ls-files --stage 或 git ls-files -s

查看暂存区中某个文件的内容git cat-files -p 文件hash值

<img src="D:\a-github\MianShi\images\git\git24.png" alt="git24" style="zoom:50%;" />

暂存区中文件的hash值正好与objects文件中的一个文件对应。



原理：

1. 当我们新初始化的git仓库，.git文件中是没有index文件的，objects中只有两个空的文件夹info和pack。

2. 当我们创建一个新的文件test.txt，并将此文件提交到暂存区后，会创建一个index文件，并且在objects中创建一个文件。index其实是一个二进制文件，存储索引列表。每个索引都有一个40位的16进制SHA-1 Hash以及他对应的文件名与之对应，索引中还包括文件模式和权限、时间戳等。每一个索引都与对象库objects中的一个文件对应。这个index文件中除了一些索引之外他还维护了一些提前计算好的tree对象的内容（也就是工作区中的一个个tree对象）

3. 当我们将暂存区中的内容提交到本地库时，又会生成与工作目录中对应的tree对象，在生成一个commit对象。我们的commit对象指向我们顶层的tree对象，我们的分支名以及标签指向这个commit对象。

4. 当我们修改文件添加到暂存区后，在objects中有会创建一个新的对象。index中该文件的索引就会指向对象库中新的对象。会重新计算tree对象，当执行commit时，又会根据计算的tree对象在对象库中生成一个tree对象。新生成的commit对象指向新的tree。

   <img src="D:\a-github\MianShi\images\git\git25.png" alt="git25" style="zoom:67%;" />



十四、命令总结



git config -l，git config --system -l，git 从fit --global -l 查看git配置信息

git config user.name "" 添加用户名，git config user.email "" 添加邮箱

git init，初始化一个git仓库

git clone 远程仓库 分支，克隆仓库

git add filename 将filename添加至暂存区,  git add ./ 将所有文件添加至暂存区

git rm --cached file ,删除暂存区中的文件，保留工作目录中的文件

git rm file ,删除工作区文件，并且将这次删除放入暂存区

git mv sourcefilename lastfilename，修改文件名，并且将修改后的文件放入暂存区

git commit -m "xxx" 将暂存区内容提交到本地仓库

git commit -a 可以直接将工作目录中的内容提交到本地仓库

git commit --amend -m "xxx"，修改上次提交的描述等信息

git push

git pull

git branch ，查看本地所有分支

git branch -r，列出所有远程分支

git branch -a，列出所有本地分支和远程分支

git branch branchname，新建分支

git checkoutout branchname，切换分支

git merge branchname 将branchname分支合并到当前分支

git push origin --delete，删除远程分支

git branch -dr [remote/branch]，删除远程分支



git checkout filename，恢复暂存区的指定文件到工作区

git checkout . ，恢复暂存区的所有文件到工作区

git reset filename，将指定文件恢复到上一此提交的版本

git reset --hard 索引值，将版本前进或后退到指定版本





十五、git工具

工作中我们一般很少去直接使用命令，推荐两个比较好用的git工具

TortoiseGit：https://download.tortoisegit.org/

SourceTree：https://www.sourcetreeapp.com/



文章参考：

git暂存区原理：https://blog.csdn.net/s646575997/article/details/52143586





 