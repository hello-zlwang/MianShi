git

一、git工作区

git的工作区有三个或者四个。

三个工作区：工作目录、暂存区、本地资源库

四个工作区：工作目录、暂存区、本地资源库、远程资源库

> 工作目录：一般就是我们本地的文件，直接对其文件或内容进行修改
>
> 暂存区：
>
> 本地资源库：
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







