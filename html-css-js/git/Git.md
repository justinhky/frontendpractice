# Git notes
大家可以去阅读廖雪峰的Git教程，他的教程目的性比较强，就是让你掌握Git的基本用法，我现在的这个目录完全就是照着他的Git教程建起来的。
我觉得够用了，太高级的功能也不适合我，我只要掌握基本的使用功能足以。

## 文档日志history
- 20220404：因遗忘翻阅而重新整理了git add相关内容  
- 20220406：版本库和本地分支不一致的解决办法

## Git概念和原理
Git是分布式版本控制系统Distributed Vernsion Control System，他有一个核心的逻辑是，Git跟踪并管理的是“修改”。
Git分为三个区域：  
1. 工作区working directory，或者叫workspace，就是你建立的文件夹目录
2. 暂存区，index或者叫stage
3. 版本库repository，分别为本地版本库和远程版本库
    - 本地版本库local repository
    - 远程版本库remote repository，为我们保存一份代码
    - head指向git创建的第一个master分支  
    - master分支是主分支  
4. head指针：git内部的一个指针，指向当前分支版本顶端，也就是在当前分支你最近的一个提交  
5. 工作区、暂存区和版本仓库都是在本地电脑，commit命令是提交到本地版本库，没有网络也可以提交。push是提交到远程仓库，必须有网络才可以提交。


## FAQ（这是常见问题记录，想看安装使用请[直接跳转](#install)）
1. git pull时冲突的解决办法  
- 1.1 忽略本地修改，强制拉取远程到本地，适合于本地版本已无用可以强拉
```
git fetch --all
git reset --hard origin/dev
git pull
```
- 关于commit和pull的先后顺序，commit——》pull——》push 和 pull——》commit——》push的顺序，两种情况都遇到过代码冲突。解决方法如下：
2. 未commit先pull，视本地修改量选择revert或stash
```
// 场景
同事 有新提交
我 没有pull -> 修改了文件 -> pull -> 提示有冲突
```
2.1 本地修改量小  
- 如果本地修改量小，例如只修改了一行，可以按照以下流程  
```
-> revert(把自己的代码取消) -> 重新pull -> 在最新代码上修改 -> [pull确认最新] -> commit&push
```
2.2 本地修改量大，冲突较多  
有两种方式处理
```
-> stash save(把自己的代码隐藏存起来) -> 重新pull -> stash pop(把存起来的隐藏的代码取回来 ) -> 代码文件会显示冲突 -> 右键选择edit conficts，解决后点击编辑页面的 mark as resolved->  commit&push
-> stash save(把自己的代码隐藏存起来) -> 重新pull -> stash pop(把存起来的隐藏的代码取回来 ) -> 代码文件会显示冲突 -> 右键选择resolve conflict -> 打开文件解决冲突 ->commit&push
```
3. 已commit未push，视本地修改量选择reset或直接merge  
```
// 场景
同事 有新提交
我 没有pull -> 修改了文件 -> commit -> pull -> 提示有冲突
```
3.1 修改量小，直接回退到未提交的版本（可选择是否保存本地修改）
```
-> reset(回退到未修改之前，选hard模式，把自己的更改取消) -> 重新pull -> 在最新代码上修改 -> [pull确认最新] -> commit&push
```
3.2 修改量大，直接merge，再提交（目前常用）
```
-> commit后pull显示冲突 -> 手动merge解决冲突 -> 重新commit -> push
```


## Git常用指令
## 常见注意事项
1. 不要用windows自带的记事本工具编辑文档，会产生编码错误  

### <span id="install">Git安装</span>
1. Windows  
因为我用的windows，所以只记录windows的，其他版本大家自行学习  
从官网下载Git程序[git link](https://git-scm.com/downloads)，安装完成后，运行Git-Bash，出现命令行窗口即代表成功。  

### 为你的电脑git交互起一个名字和邮箱，便于识别不同用户  
1. 配置电脑用户名  
安装完成后，还需要最后一步设置，在命令行输入：  
```  
$ git config --global user.name "Your Name"  
$ git config --global user.email "email@example.com"  
```  
  因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。它的主要作用就是用来标识吧，就跟名片类似的感觉  
注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。  
```  
git config  参数：--global  
```   
2. 显示当前目录的路径，尽量不要使用中文目录  
```
pwd  
```  

3. 创建一个空目录  
```
mkdir  //创建一个空目录  
```
4.  创建初始化仓库  
```
git init  
```
把这个目录变成git可以管理的仓库，这个步骤很重要，务必使用一个空白目录，只有先创建了git目录，下面的工作才可以开展。
5. 显示仓库文件
```
ls 参数：-ah  
dir
```
ls和dir都可以显示当前目录文件，-ah参数表示同时显示隐藏文件  


## 远程仓库的创建、连接和管理
### 第一步：创建SSH key
```
ssh-keygen -t rsa -C "youremail@example.com"  
```
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可。  
如果一切顺利的话，可以在用户主目录里找到.ssh目录，windows的用户主目录是c:\users\yourname。  
里面有id_rsa和id_rsa.pub两个文件，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

### 第二步：将id_rsa.pub的信息复制到github中
- 登录github，找到add ssh key，添加id_rsa.pub的内容(文件可以用文本编辑器打开，不要用windows自带的编辑器）  

### 推送到远程库  
```
git push <远程主机名> <本地分支名>:<远程分支名>
git push <远程主机名> <本地分支名>”  //如果本地分支名与远程分支名相同，则可以省略冒号：及后面的内容“
```

#### 第一次push
1. 推送分支到远程库  
注意：**分支推送顺序的写法是<来源地>:<目的地>，所以注意区分git pull和git push**.  
```
git push <远程主机名> <本地分支名>:<远程分支名>
```
如果本地分支名与远程分支名相同，则可以省略冒号：及后面的内容  
```
git push <远程主机名> <本地分支名>
```
2. 第一次推送分支到远程库  
```
git push -u origin master  
```
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。

#### 有了第一次以后使用以下命令提交到远程仓库
```
git push origin master
```
每次本地提交后，使用这个命令提交到远程库  

### 从远程库克隆
1. 直接克隆
```
git clone git@github.com:sample/sample.git  
```
克隆远程库到本地，url是github库的url，用git@github.com:开头的地址，这可以看成是一种url格式
2. 查看远程库
```
git remote -v  //查看远程库详细信息，不带参数只显示远程库名字
```
3. 删除远程库连接
```
git remote rm <name>  //删除远程库，只是删除当前电脑的远程库链接，并不是物理上删除了远程库，物理上删除远程库直接在github删除
```


### git add提交和管理修改  
git add的目的是将修改文件由工作区提交到暂存区，可以多次提交或者一次提交多个文件，常用语法有如下  

1. 添加一个文件，git add添加修改到缓存区，可以一次添加多个文件或者多次添加  
```
git add file1  
git add -i  [<path>]    //表示查看<path>中所有被修改过或者被删除过但是没有提交的文件。
git add -u [<path>]   //表示把<path>中所有tracked文件中被修改过或者已经删除的信息添加到暂存库中。它不会处理untracked的文件。
git add -a [<path>]  //表示把<path>中所有tracked文件中被修改或者被删除文件和所有untracked的文件信息添加到暂存区。
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
git commit -m  //参数：-m表示此次修改的标注信息
git commit -a -m //参数-a表示可以把tracked的文件提交到本地仓库，就算这文件没有git add也可以提交
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
5. 查看每一次的提交日志，参数--pretty=oneline表示逐行显示  
```
git log  参数：--pretty=oneline
```
6. 查看每一次的命令历史日志
```
git reflog
```


### Git回退
1. 回退
```
git reset  
```
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
4.1 未使用git add 缓存代码时  
```
git checkout -- filepathname  //放弃单个文件的修改
git check out . //放弃所有文件的修改  
```
此命令用来放弃掉所有还没有加入到缓存区(就是 git add 命令)的修改：内容修改与整个文件删除。但是此命令不会删除掉刚新建的文件。因为刚新建的文件还没已有加入到 git 的管理系统中。所以对于git是未知的。自己手动删除就好了。  
4.2 已经使用git add缓存了的代码  
```
git reset HEAD filepathname  
```
比如: git reset HEAD readme.md   
4.3 已经使用 git commit提交了代码  
```
git reset --hard HEAD^ 回退到上一次commit的状态  
```
4.4 回退到任意版本  
```
git reset --hard  commitid  
```  
你可以使用 git log 命令来查看git的提交历史  


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
3. 从远程仓库拉取一条本地不存在的分支并切换到新分支
```
git checkout -b local_branch_name origin/<remote_branchName> //b参数表示创建并切换到一个新的分支，相当于下面两个命令
git branch dev  
git checkout dev  
```
如果出现如下提示信息，表示拉取不成功:
```
Fatal: Cannot update paths and switch to branch xxx at the same time.
Did you intend to checkout 'origin/xxx' which can not be resolved as commit?
```
此时，我们要先执行
```
git fetch
```
然后再执行
```
git checkout -b local_branchName origin/remote_branchName
```

4. 查看，创建和切换分支
```
git branch  //查看分支
git branch <name>  //创建分支
git checkout <name> 或者 git switch <name>  //切换分支
```

- 创建并切换分支
```
git switch -c  
```
5. 删除分支
```
git branch -d  name
git branch -D name  //强行删除分支  
```
6. 合并分支
```
git merge --no-ff -m //"merge with no-ff" dev  
on-ff表示禁用fast forward
```
7. 查看分支合并图
```
git log --graph  
```
8. 临时存储分支
```
git stash  //临时存储分支，可以后续接着工作  
git stash list  //查看存储的分支
```
9. 创建远程库的分支到本地
```
git checkout -b dev origin/dev
```
10. 同步远程库分支到本地  
```
git pull  
git pull rebase  //--rebase的作用是取消本地库中刚刚提交的commit，并把他们接到更新后的版本库中。
```


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
