目标：本地使用git push后可以把本地代码提交到vps的git服务器和github上

## 在vps设置Git用户并安装Git

登陆vps，切换到root用户：

    su -
添加一个叫git的用户来处理仓库：

    groupadd git
    adduser git -g git
然后为这个账户设置密码：

    passwd git
然后就是装git了：<br>
Centos/Fedora 执行命令：

    yum install git
Ubuntu/Debian 执行命令：

    apt-get install git

## 将SSH密钥添加到访问列表（其实就是个ssh免密码登陆）

下面是在vps上进行操作：<br>
切换到git账户：

    su git
将刚才产生的 id_rsa.pub 文件上传到git用户的home目录下（/home/git/）。<br>
然后告诉SSH守护进程去接受哪些ssh密钥：

    mkdir ~/.ssh && touch ~/.ssh/authorized_keys
下面是`windows`上的操作：

>如果你的vps ssh端口号不是22可以在本地.ssh文件夹下配置个config文件（没有新建）

    host bwg
    hostname xx.xx.xx.xx
    port xxxx

打开git bash，执行下面的命令，将产生的公钥内容拷贝到vps上的authorized_keys (注意替换命令中的用户名和ip) ：

    cat .ssh/id_rsa.pub | ssh  git@bwg "cat >> ~/.ssh/authorized_keys"
然后看看能不能免密码登陆：

    ssh  git@bwg
第一次登陆的时候会让你输入密码，以后再登陆就不需要输入密码了。

=====================================

如果每次登陆都需要密码，则按照如下方法处理：<br>
1.进行ssh登录时，出现：”Agent admitted failure to sign using the key“ .<br>
   执行： 
   
    $ssh-add
   强行将私钥 加进来。<br>
2.如果无任何错误提示，可以输密码登录，但就是不能无密码登录，在被连接的主机上（如A向B发起ssh连接，则在B上）执行以下几步：

    $chmod o-w ~/<br>
    $chmod 700 ~/.ssh<br>
    $chmod 600 ~/.ssh/authorized_keys<br>
3.如果执行了第2步，还是不能无密码登录，再试试下面几个

    $ps -Af | grep agent<br>
检查ssh代理是否开启，如果有开启的话，kill掉该代理，然后执行下面，重新打开一个ssh代理，如果没有开启，直接执行下面：

    $ssh-agent
还是不行的话，执行下面，重启一下ssh服务

    $sudo service sshd restart
4.执行ssh-add时提示“Could not open a connection to your authenticationh agent”而失败
执行： 
    ssh-agent bash

## 在服务器上创建裸版本库：

ps：远程仓库通常只是一个裸仓库（bare repository） — 即一个没有当前工作目录的仓库。因为该仓库只是一个合作媒介，所以不需要从硬盘上取出最新版本的快照；仓库里存放的仅仅是 Git 的数据。简单地说，裸仓库就是你工作目录中 .git 子目录内的内容

我们就在 /home/testgit/ 下创建一个叫 sample.git的裸仓库吧：

    mkdir /home/testgit
    cd /home/testgit
    git init --bare sample.git
//这里 git init 是初始化空仓库的意思，而参数 --bare 是代表创建裸仓库，这个参数一定记得带上

当运行完上面的最后一句命令时，会有提示：Initialized empty Git repository in /home/testgit/sample.git/ 
如果你得不到该结果，可能就要回头检查哪一步出问题了

1. 创建web站点目录www

如果你已经拥有lamp环境，那么相信你已经了解该目录，搭建lamp环境详情可以看我的另一篇博客：centos 7搭建lamp平台环境、Centos7 系统下怎么更改apache默认网站目录

现在我的 web 站点目录在 /home/www

2. 在本地克隆服务器上的裸仓库：

前提：本地已安装git 
打开 git bash ，我打算在我的D盘下clone 远程git服务器的版本库

    cd /d
    git clone git@bwg:/home/testgit/sample.git 

在这里如果没有配置公钥的话，会提示输入密码，但是我们可能并不知道密码，那就配置公钥咯： 

如果使用git push失败了，极有可能是因为服务器的权限问题，就比如之前我们建的 testgit 文件夹，在这里我的解决方法是：

    chown -R git:git testgit

将testgit文件夹以及下面的子文件夹都赋给了git,这样就保证了推送成功。

第一次push可能会有一些提示，因为裸版本库还什么都没有，你可能需要 git push origin master写全命令，之后就没必要了，直接 git push 就可以了。

到目前为止，我们完成了第一个任务，实现了一个共享平台，既可拉取数据，又可以推送数据。

## 实现自动同步到站点目录（www）

就比如刚才我们往远程仓库推送了index.html文件，虽然提示推送成功，但是我们现在在服务器端还看不到效果，心理总是不爽。又比如我写了个html页面，我想在站点中马上看到，那自动同步就派上用场了。

自动同步功能用到的是 git 的钩子功能，

服务器端：进入裸仓库：/home/testgit/sample.git

    cd /home/testgit/sample.git
    cd hooks
这里我们创建post-receive文件

    vim post-receive
在该文件里输入以下内容

    #!/bin/bash
    git --work-tree=/home/www checkout -f
保存退出后，将该文件用户及用户组都设置成git

    chown git:git post-receive
由于该文件其实就是一个shell文件，我们还应该为其设置可执行权限

    chmod +x post-receive
现在我们可以在本地计算机中修改index.html文件，或者添加一个新文件，提交到远程仓库，然后到/home/www下面，看看有没有我们刚才提交的文件。

如果你在Git推送的工程中发现推送成功 但是在www目录下并没有自己的代码，这时候你可要注意了：这是由于文件夹的权限的原因造成的！ 假设你的www目录的所属的用户组为root，你可以将你的git用户加入这个组;并给git添加写入权限，或者其他解决方法，反正你要服务器上的git用户有权限进入www文件夹。

## 本地同时提交到vps的git服务器和github

这里有个方便的方法：在本地仓库.git里config文件里加上你的github地址

    [remote "origin"]
	url = git@bwg:/home/testgit/sample.git
	url = git@github.com:xxx/xxxx.git
	