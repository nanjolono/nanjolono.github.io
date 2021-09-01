---
layout: post
title:  "git单分支!"
date:   2021-09-01 17:58:25 +0800
categories: jekyll update
---
#Git基础
从这一章开始，你将学会基础的git命令，包含了日常开发中最主要的一些基本操作。创建一个新的git代码仓库开始，在***单分支***模型上，查看一个文件的状态，设置仓库中的信息，基础的提交推送，撤销已经提交的修改等等。
##创建一个新的git仓库

###在已经存在的项目中初始化一个git仓库
####初始化本地仓库
当已经有一个在开发中的项目时，代码版本管理的工作需要托管给git，需要在已经创建的项目是用命令行切换到项目文件夹中执行。
git init
当看到返回信息
Initialized empty Git repository in /Users/gitTest/Documents/code/test/.git/
说明已经创建成功了一个git仓库
这是上述在osx 和linux 是这么操作的，windows提供了另一种选择
新建一个文件夹
(img)
右键选择git bash here
(img)
在这个命令行里执行
(img)
这样成功的初始化了一个新的仓库，那么这个标红的部分指的是代码当前所在的分支，这个提示只有在windows的git bash here客户端才会有的，非常的实用。

注：命令行在不同的操作系统中操作方式不同，需要在命令行中切换到项目路径下执行

####关联远程仓库
那么成功的初始化了一个本地仓库，那么接下来，就可以对远端仓库进行关联
git remote add origin [url]
那么接下来，应该拿到这个url，以github为例子的话，需要先登录github
(img)
新建一个仓库
(img)
新建成功后把这个URL复制粘贴下来
(img)
比如这个例子就是
git remote add origin https://github.com/nanjolono/myGitPractice.git
(img)
接下来就可以拉取代码了
git pull origin master
(img)
###在已有的仓库中clone新的代码
当在远端仓库中已经存在了代码时，需要获取代码，需要执行git clone命令
git clone [remoteUrl]
当然，这个remoteUrl是一个参数，这里指的是git远端仓库的地址，示例中，在github仓库获取，
(img)
当获取到指定的git仓库地址后，可以执行
git clone https://github.com/nanjolono/myGitPractice.git
看到如下结果时，代码已经拉取成功
gitTest@MacBook-Pro code % git clone https://github.com/nanjolono/myGitPractice.git                                                   
Cloning into 'myGitPractice'...
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 5 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (5/5), 4.72 KiB | 603.00 KiB/s, done.
当下载成功后，该路径下会创建一个新的文件夹，名称为git仓库的名称，如果需要更改文件夹名称。可以在clone 后增加参数
git clone https://github.com/nanjolono/myGitPractice.git myGit
这样，重新拉取代码后的文件夹名称为myGit了，当然，你可以更改一些别的名字 
##仓库中文件的状态
那么拉取代码成功后，使用命令行切换到项目根目录中，
cd myGitPractice
###查看状态
执行查看状态的指令
git status
返回结果
On branch master
Your branch is up to date with 'origin/master'.

nothing to commit, working tree clean
如果看到了
fatal: not a git repository (or any of the parent directories): .git
说明在命令行中没有切换到项目路径中
比如讲，git这个目录在test/gitpractice下
(img)
但是现在命令行客户端在test下，执行git命令是无法识别到git项目的

###Untracked File
那创建一个新的文件
echo "test" > test.txt
创建成功后，执行
git status
返回结果
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	test.txt

nothing added to commit but untracked files present (use "git add" to track)
可以看到，新建的test.txt文件的状态为 Untracked files，新建的文件是不会被git版本控制中所纳入管理的，提交推送的时候不会检查未被追踪的文件。如果是临时生成的测试文件，可以选择不纳入版本控制中。如果需要纳入版本控制中，可以执行
git add test.txt
返回结果
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	new file:   test.txt
这个时候可以看到，新建的文件已经被纳入了版本控制中，处于一个修改待提交的状态。
##提交推送第一批文件
###git add 添加提交的文件
这个命令可以将文件添加到git 版本库中，可以单个提交，也可以批量提交。
举个例子
(img)
这里已经新建了两个文件，一个是test.txt和一个main.txt，那么添加main.txt文件就是git add main.txt
通过git status可以看到，main.txt已经不在未追踪文件区域（Untracked files）里了，而是在已提交文件区域（Changes to be committed）里。
当然，也可以批量提交文件
这里在src路径下新建了first.txt和test.txt文件，那么接下来提交整个src目录就可以。
使用
git add ./src
(img)
###git commit  添加提交信息
在执行git add 后，这里学习一个暂时学习git commit 一个最简单的选项，在提交的时候添加提交信息
git commit -m 'message'
(img)
###git push 推送的到远端仓库中
执行
git push origin master
这条命令就可以直接将代码推送到远端仓库中
通过github来查看是否推送成功
(img)
由此可见已经推送成功了。
##后悔药？git还真有
###git log 查看提交记录
通过git log，可以查看提交的历史记录，打开git bash here，直接执行
git log 
(img)
可以看到，有两次提交记录。那么每次提交的时候都会产生一次新提交记录。推送后，别人更新代码的时候，也会将这些记录更新到自己的仓库中。那么这个功能就是一个日志，记录了每次代码变化的功能。那么接下来通过这个日志的功能进行代码回退。
###git reset 提交代码的回退
代码提交出错了？这样的情况常有，这里可以使用git reset 命令来进行反悔的操作。
git reset 

####保存代码
那么在提交推送代码后，可能代码提交错了，想撤销提交，那么这里就需要保存代码，只回退提交文件的状态。
那么先观察一下当前的代码库状态
(img)
在当前的情况下，所有的代码已经提交推送了。那么此时my first commit这一次提交我提交了错误的文件，想要撤回这一次推送，然后重新提交，但是还想保留my first commit修改的内容。那么就需要使用到
git reset --soft [想要回退到的指定的版本号]
那么在这里，执行的命令就是
git reset --soft 35c354985f5ead59710566a8efbd7332b6f5ee2c
(img)
那么在进行回退操作的后。
首先通过git status 查看文件，发现推送的文件已经变更为待推送状态。通过git log查看，之前的最新的一条记录已经被删除掉了。那么就可以进行重新推送了。
(img)

####丢弃代码
那么这一种情况是与上一个reset —hard属于并列的情况，这种是在想要回退代码的的时候，中间产生的变更丢弃不要。可以使用—hard选项。那么来操作一下。
(img)
那么在second commit中，提交了三个文件，那么在执行git reset —soft的时候，文件会被标注为修改待提交的状态。但是在使用git reset —hard后，文件已经丢失。并且没有被记录的到版本库里。
(img)
已经变成了远端仓库的第一次的初始化状态，所有的文件均已回退了。并且中间产生的文件内容回退了。

####代码的推送，在推送代码的时候，其实会发现，代码推送是失败的。
(img)
这里回退的是远端仓库的代码，所以这里在回退的时候，本地的代码与远端的代码版本不一致，会导致这样的情况发生，那么这部分现在是单分支个人开发，所以这里可以使用强制推送，将本地的代码强制推送覆盖到远端，由于这个部分是单人单分支开发，所以可以采取这种策略，到多分枝多人合作开发的部分，可以在学习其他的指令。
使用
git push -f origin master
(img)
那么在强制推送后，代码成功的推送到了远端。

