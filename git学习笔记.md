# Git简介 #

git是目前世界上 **最先进** 的分布式版本控制系统，由Linux之父Linus于2005年开发。

与传统的cvs或者svn相比，git的 **优势** 在于:

+ **无需联网就可以进行工作**

+ **没有中央服务器，每个人的电脑上都是一个完整的版本库**

+ **安全性要高很多，某一个人的电脑坏掉了不要紧，随便从其他人哪里复制一个就可以了**

+ **所谓的中央服务器仅仅只是用来协同工作，交换文件而已，每一个人的本地库都可以进行特版本的恢复**

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

由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key。

    $ ssh-keygen -t rsa -C "252174621@qq.com"

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH key”，填上任意的title，在key文本框里面粘贴id_rsa.pub的
内容，点“Add Key”，你就应该看到已经添加的Key。

** 为什么GitHub需要SSH Key呢 ** 因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。
    
   



