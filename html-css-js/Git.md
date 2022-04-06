
# Git notes
大家可以去阅读廖雪峰的Git教程，他的教程目的性比较强，就是让你掌握Git的基本用法，我现在的这个目录完全就是照着他的Git教程建起来的。
我觉得够用了，太高级的功能也不适合我，我只要掌握基本的使用功能足以。

## 文档日志history
- 20220404：因遗忘翻阅而重新整理了git add相关内容  

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
1. 配置电脑名字和邮箱  
安装完成后，还需要最后一步设置，在命令行输入：  
```
git config  参数：--global
```
```
$ git config --global user.name "Your Name"  
$ git config --global user.email "email@example.com"  
```
因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。我自己试验了用不同名字不同邮箱是可以的，可能它的主要作用就是用来标识吧，就跟名片类似的感觉  
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。  
 
2. 显示当前目录，尽量不要使用中文目录  
```
pwd
```
3. 创建一个空目录  
```
mkdir 
```
4. 创建git初始目录
```
git init  
```
把这个目录变成git可以管理的仓库，这个步骤很重要，务必使用一个空白目录，只有先创建了git目录，
下面的工作才可以开展，因为我第一次就直接用命令，结果一直提示没有可以用的仓库，就是这个原因导致的。
5. 显示目录文件
```
ls 参数：-ah  
dir
```
ls和dir都可以显示当前目录文件，-ah参数表示同时显示隐藏文件  


### git add提交和管理修改  
git add的目的是将修改文件由工作区提交到暂存区，可以多次提交或者一次提交多个文件，常用语法有如下  
1. 添加一个文件，git add添加修改到缓存区，可以一次添加多个文件或者多次添加  
```
git add file1  
```
2. 添加多个文件，中间用空格隔开  
```
git add file1 file2 file3...  
```
3. config目录下及子目录下所有文件
```
git add config/*  
```
4. 添加home目录下的所有.php文件  
```
git add home/*.php  
```
5. git add . 添加所有的文件，或者git add --all 添加所有的文件
```
git add . 或者git add --all  
```
6. git add 添加文件夹  
```
git add <category1>
```
7. git commit表示将文件提交到仓库，-m表示为本次提交添加说明  
```
git commit 参数：-m  
```


### Git查询命令
1. git status  查看当前仓库的状态  
```
git status -uno, 不显示未跟踪的文件(git status --untracked-files=no)
```
2. update the remote branch in your repository to point to the latest version.
```
git fetch origin
```
3. 查询最近的修改
```
git diff  
```
4. 查看工作区和版本库最新版本的差别
```
git diff head -- file_name  
```
```
git diff origin/master, 或者 git diff head origin/master
//if you want to accept the remote changes, apply:
git merge origin/master
```
5. 查看每一次的提交日志，参数--pretty=oneline表示逐行显示  
```
git log  参数：--pretty=oneline
```
6. 查看每一次的命令历史日志
```
git reflog
```


### Git回退
1. git reset  
git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。  
git reset不会产生commit，它仅仅更新一个branch指向另外一个commit。
2. 返回上一个版本  
```
git reset --hard HEAD^  
```
3. 返回指定commit_id的版本  
```
git reset --hard commit_id
```
4. 撤销 
```
git revert
```
 5. 未使用git add 缓存代码时，git check out 放弃所有文件修改 
 ```
git checkout -- filepathname (必须要--，要不然命令变成切换分支了）
```
此命令用来放弃掉所有还没有加入到缓存区(就是 git add 命令)的修改：内容修改与整个文件删除。  
但是此命令不会删除掉刚新建的文件。因为刚新建的文件还没已有加入到 git 的管理系统中。所以对于git是未知的。自己手动删除就好了。  
6. 已经使用git add缓存了的代码，使用git reset HEAD
```
git reset HEAD filepathname
比如: git reset HEAD readme.md
```
7. 已经使用 git commit提交了代码  
```
git reset --hard HEAD^ 回退到上一次commit的状态  
git reset --hard  commitid  
```
此命令可以用来回退到任意版本 ，你可以使用 git log 命令来查看git的提交历史  


### git rm删除文件
1. 将文件从暂存区和工作区中删除  
```
git rm <file1>
```
2. 删除之前修改过并且已经放到暂存区域的话，则必须要使用强制删除选项 -f  
```
git rm -f <file1>
```
3. 如果想把文件从暂存区域移除，但仍然希望保留在当前工作目录中，即仅仅从跟踪清单中删除，使用--cached选项即可  
```
git rm --cached <file1>
```
4. 递归删除，如果后面跟的是一个目录为参数，怎会递归删除整个目录中的所有子目录和文件  
```
git rm -r *  
git rm -r <category1>
```


### 管理分支
1. b参数表示创建并切换到一个新的分支，相当于下面两个命令 
```
git checkout -b branch_name
```
```
git branch dev  
git checkout dev  
```
2. 可以查看当前分支
```
git branch  
```
3. 删除分支
```
git branch -d  name
```
4. 合并指定分支到当前分支
```
git merge
```
5. 查看分支合并图
```
git log --graph  
```
6. 创建并切换分支  
```
git switch -c  
```
7. 合并分支
```
git merge --no-ff -m //"merge with no-ff" dev  
on-ff表示禁用fast forward 
```
8. 临时存储分支
```
git stash  //临时存储分支，可以后续接着工作  
git stash list  //查看存储的分支
```
9. 删除分支  
```
git branch -D name  //强行删除分支  
```
10. 创建远程库的分支到本地
```
git checkout -b dev origin/dev
```
11. 同步远程库分支到本地  
```
git pull  
```
12. 把远程库中的跟新合并到本地库中（可能存在冲突需要解决），
```
git pull rebase  //--rebase的作用是取消本地库中刚刚提交的commit，并把他们接到更新后的版本库中。
```


## 远程仓库的创建、连接和管理
### 第一步：创建SSH key
```
ssh-keygen -t rsa -C "youremail@example.com"  
```
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，windows的用户主目录是c:\users\yourname。  
里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

### 第二步：将id_rsa.pub的信息复制到github中
- 登录github，找到add ssh key，添加id_rsa.pub的内容(文件可以用文本编辑器打开，不要用windows自带的编辑器-因为我遵从老师的建议不用windows记事本）  

### 推送到远程库  
```
git push <远程主机名> <本地分支名>:<远程分支名>
git push <远程主机名> <本地分支名>”  //如果本地分支名与远程分支名相同，则可以省略冒号：及后面的内容“
```
#### 第一次push
```
git push -u origin master  
```
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，
还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

#### 有了第一次以后使用以下命令提交到远程仓库
```
git push origin master
```
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
