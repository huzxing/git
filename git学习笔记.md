# Git的安装及配置 #

### windows下的Git安装 ###

从 [http://git-scm.com/download/](http://git-scm.com/download/) 下载然后就是傻瓜式安装即可

### Git的本地环境配置 ###

    $ git config --global "huzaixing123456"
  
    $ git config --global "252174621@qq.com"
    
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的 **名字** 和 **Email** 地址。

**注意** : git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用
户名和Email地址。

# github网站 #

在Git中并不存在主库的概念，每一份复制出的库都可以独立使用。但是的开发的过程中，确实需要一台中央服务器作为各协同工作之间交换的枢纽，其实完全可以自己搭建一个Git服务器，但是现阶段已经有了这样一个免费的git仓库托管服务的平台，这既是github网站，只需要注册一个github账号，就可以免费获得Git远程仓库。

### github配置 ###

由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点 **设置**：

第1步：**创建SSH Key**。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key。

    $ ssh-keygen -t rsa -C "252174621@qq.com"

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH key”，填上任意的title，在key文本框里面粘贴id_rsa.pub的
内容，点“Add Key”，你就应该看到已经添加的Key。

**为什么GitHub需要SSH Key呢** : 因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

# git的常用命令 #

### 创建版本库 ###

选择一个合适的目录，通过以下命令将该目录变成Git可管理的仓库

    git init
    
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库，细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。   
    
### 提交文件 ###

第一步：使用git add命令，将要提交的文件添加到仓库暂存区

    git add hzx.txt
    
第二步：使用git commit命令将文件提交到本地仓库

    git commit -m "本次提交说明"
    
-m后面输入的是本次提交的说明，可以不输入任何内容，但是为了更好的协同工作，以及后期版本的调整，写入一些有意义的文字描述是必须的。

### 版本回退 ###

查看提交记录

    git log

每次提交都会产生一个commit id，Git的commit id是一个SHA1计算出来的一个非常大的数字，用十六进制表示，只要找到commit id，就可以任意穿梭于各个版本之间

会退到指定版本

    git reset --hard d458hyd(commit id)
    
其中的commit id可以只写最前面的七位，Git会自动匹配。当然会退到某一个版本还有快捷的指令，如下：    

    git reset --hard HEAD^(会退到上一个版本)
    git reset --hard HEAD^^(会退到上上个版本)
    git reset --hard HEAD~100(会退到上一百个版本)
    
未来版本

    git reflog
    
有时候回退到某一个版本时想更新到未来版本，但是git log是查不到的，可以用此指令查看全部的操作日志，找到commit id。    
    
### 管理修改 ###

查看文件状态

    git status
    
查看文件详细修改内容

    git diff HEAD -- hzx.txt
    
### 撤销修改 ###

    git checkout -- hzx.txt
    
+ 第一种情况：文件修改后还未放进暂存区，此时撤销，就会回退到没做修改之前的状态
+ 第二种情况：文件修改后已经放进暂存区，此时又做了修改，撤销的话会回到增加到缓存区的状态
+ 另外注意，如果提交到暂存区后没做任何修改，此时回退没有效果。再想做版本只能通过commit id了;checkout后面一定个要有--，要不然就成为分支切换了;刚删除的文件也可以用此方式恢复文件。

### 删除文件 ###

    git rm hzx.txt(删除指定的文件)
    git commit -m "提交说明"（将删除文件的记录提交到本地仓库，注意，前面无须add到暂存区了）
    
# 分支管理 #

### 创建分支 ###

    git branch (查看分支)
    git branch hzx (创建分支hzx)
    git checkout hzx （切换到hzx分支）
    git checkout -b hzx （创建分支hzx，并且切换到hzx分支 -b表示创建并切换）
    
### 合并 ###

切换到要合并到的分支，比如将hzx合并到master，则先切到master分支。

    git merge hzx
    
### 删除分支 ###

    git branch -d hzx
