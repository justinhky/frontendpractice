# Git notes
大家可以去阅读廖雪峰的Git教程，他的教程目的性比较强，就是让你掌握Git的基本用法，我现在的这个目录完全就是照着他的Git教程建起来的。
我觉得够用了，太高级的功能也不适合我，我只要掌握基本的使用功能足以。
## Git概念和原理
Git是分布式版本控制系统Distributed Vernsion Control System，他有一个核心的逻辑是，Git跟踪并管理的是“修改”。
Git分为三个区域：  
- 工作区working directory，就是你建立的文件夹目录
- 版本库repository  
    - stage暂存区  
    - head指向git创建的第一个master分支  
master分支是主分支  
- head指针：git内部的一个指针，指向当前分支版本顶端，也就是在当前分支你最近的一个提交  

## 常见注意事项
- 不要用windows自带的记事本工具编辑文档，会产生编码错误
## Git常用指令

### Git安装
- Windows  
因为我用的windows，所以只记录windows的，其他版本大家自行学习  
从官网下载Git程序[git link](https://git-scm.com/downloads)，安装完成后，运行Git-Bash，出现命令行窗口即代表成功。  

### 为你的电脑git交互起一个名字和邮箱，便于识别不同用户
安装完成后，还需要最后一步设置，在命令行输入：  
$ git config --global user.name "Your Name"  
$ git config --global user.email "email@example.com"  
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。我自己试验了用不同名字不同邮箱是可以的，可能它的主要作用就是用来标识吧，就跟名片类似的感觉  
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。  
- git config  参数：--global
见上  
- pwd  
显示当前目录，尽量不要使用中文目录  
- mkdir  
创建一个空目录  
- git init  
把这个目录变成git可以管理的仓库，这个步骤很重要，务必使用一个空白目录，只有先创建了git目录，
下面的工作才可以开展，因为我第一次就直接用命令，结果一直提示没有可以用的仓库，就是这个原因导致的。  
- ls 参数：-ah  
- dir
ls和dir都可以显示当前目录文件，-ah参数表示同时显示隐藏文件  
- rm和git rm  
rm可以直接删除工作区的文件，git rm+git commit可以删除版本库中的文件

### git提交和管理修改
- git add  
git add添加修改到缓存区，可以一次添加多个文件或者多次添加
```
添加多个文件
git add file_1 file_2 file_3
git提交文件夹的方法
git add catalog_name
添加指定目录下的文件
git config/*
git home/*.php
添加所有文件
git add .
git add --all
```
- git commit 参数：-m  
git commit表示将文件提交到仓库，-m表示为本次提交添加说明  
- git checkout -- filename（必须要--，要不然命令变成切换分支了）  
把readme.txt文件在工作区的修改全部撤销，就是让这个文件回到最近一次git commit或git add时的状态。  

### Git查询命令
- git status  
查看当前仓库的状态  
```
git status -uno, 不显示未跟踪的文件(git status --untracked-files=no)
```
- git fetch origin
update the remote branch in your repository to point to the latest version.
- git diff  
查询最近的修改
- git diff head -- file_name  
查看工作区和版本库最新版本的差别
```
git diff origin/master, 或者 git diff head origin/master
//if you want to accept the remote changes, apply:
git merge origin/master
```
- git log  参数：--pretty=oneline
查看每一次的提交日志，参数--pretty=oneline表示逐行显示  
- git reflog  
查看每一次的命令历史日志

### Git回退
- git reset  
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。  
git reset不会产生commit，它仅仅更新一个branch指向另外一个commit。  
- git reset --hard HEAD^  
返回上一个版本  
- git reset --hard commit_id  
返回指定commit_id的版本  
- git revert  
撤销

### 管理分支
- git checkout -b branch_name  
-b参数表示创建并切换到一个新的分支，相当于下面两个命令  
- git branch dev  
- git checkout dev  
- git branch  
可以查看当前分支
- git branch -d  name
删除分支
- git merge  
合并指定分支到当前分支  
- git log --graph  
查看分支合并图
- git switch -c  
创建并切换分支  
- git merge --no-ff -m "merge with no-ff" dev  
--on-ff表示禁用fast forward  
- git stash  
临时存储分支，可以后续接着工作  
- git stash list  
查看存储的分支
- git branch -D name  
强行删除分支  
- git checkout -b dev origin/dev
创建远程库的分支到本地
- git pull  
同步远程库分支到本地  
- git pull rebase  
把远程库中的跟新合并到本地库中（可能存在冲突需要解决），--rebase的作用是取消本地库中刚刚提交的commit，并把他们接到更新后的版本库中。


## 远程仓库的创建、连接和管理
### 第一步：创建SSH key
- ssh-keygen -t rsa -C "youremail@example.com"  
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，windows的用户主目录是c:\users\yourname。  
里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。
### 第二步：将id_rsa.pub的信息复制到github中
- 登录github，找到add ssh key，添加id_rsa.pub的内容(文件可以用文本编辑器打开，不要用windows自带的编辑器-因为我遵从老师的建议不用windows记事本）  

### 推送到远程库  
- git push &lt;远程主机名&gt; &lt;本地分支名&gt;:&lt;远程分支名&gt;
如果本地分支名与远程分支名相同，则可以省略冒号：及后面的内容“git push &lt;远程主机名&gt; &lt;本地分支名&gt;”
- git push -u origin master  
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。  
- git push origin master
每次本地提交后，使用这个命令提交到远程库  

### 从远程库克隆
- git clone git@github.com:sample/sample.git  
克隆远程库到本地，url是github库的url，用git@github.com:开头的地址，这可以看成是一种url格式
- git remote -v  
查看远程库详细信息，不带参数只显示远程库名字
- git remote rm <name>  
删除远程库，只是删除连个电脑的链接，并不是物理上删除了远程库


## 标签管理
- git tag name commit_id  
为特定的commit id打上标签  
- git show tagname  
显示标签信息  
- git tag -d tagname  
删除标签  
- git push origin v1.0  
推送某个标签到远程  
- git push origin :refs/tags/v0.9  
先用git tag -d删除本地在用这条命令删除远程标签
