
# Git使用教程

@(示例笔记本)[git]

[原文参考](https://blog.csdn.net/mango9126/article/details/68946439) 
**git是什么**： 分布式版本控制系统；

-----
@[toc]
## git安装

 >   [点击官网下载](https://www.git-scm.com/download/)(我是在三方软件管家下载的)默认安装即可，安装完成后在安装路径下查询 ‘git ->  git bash即可’；或者在任意目录下右键，查看是否有'Git Bash Here'。 

### 设置用户名等信息
   有了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然你也可以对某个仓库指定的不同的用户名和邮箱。
```git
$ git config --global user.name "username"
$ git config --global user.email "uaser@xxx.com"
```

### 远程仓库
注册github账号，因为本地git仓库与github仓库之间传输是通过SSH加密的，故需如下配置：
#### 1、创建SSH Key,
  在用户目录下查找.ssh目录下的id_rsa （非对称加密算法的密文）与id_rsa.pub （明文）文件，若无,输入如下命令，若有则跳过
```cmd
ssh-keygen -t rsa -C "your email"
```
#### 2、添加密文
   在github上点击登录头像打开 'settings ->  Developer settings  ->  Personal access tokens -> Generate new token '，
添加你的id_rsa.pub （明文）

## git基础语法
Git基本常用命令如下：

|方法 |简述|
|:--|:--|
mkdir：          | XX (创建一个空目录 XX指目录名)|
|pwd：            |显示当前目录的路径。|
|git init          |把当前的目录变成可以管理的git仓库，生成隐藏.git文件。|
|git add XX       |把xx文件添加到暂存区去。|
|git commit –m “XX”  |提交文件 –m 后面的是注释。|
|git status        |查看仓库状态|
|git diff  XX      |查看XX文件修改了那些内容|
|git log          |查看历史记录|
|git reset  –hard HEAD^ 或者 git reset  –hard HEAD~ |回退到上一个版本(如果想回退到100个版本，使用git reset –hard HEAD~100 )|
|cat XX         |查看XX文件内容|
|git reflog       |查看历史记录的版本号id|
|git checkout — XX  |把XX文件在工作区的修改全部撤销。|
|git rm XX          |删除XX文件|
|git remote add origin https://github.com/user/testgit |关联一个远程库|
|git push –u(第一次要用-u 以后不需要) origin master |把当前master分支推送到远程库|
|git clone https://github.com/user/testgit  |从远程库中克隆|
|git checkout –b dev  |创建dev分支 并切换到dev分支上|
|git branch  |查看当前所有的分支|
|git checkout master |切换回master分支|
|git merge dev    |在当前的分支上合并dev分支|
|git branch –d dev |删除dev分支|
|git branch name  |创建分支|
|git stash |把当前的工作隐藏起来 等以后恢复现场后继续工作|
|git stash list |查看所有被隐藏的文件列表|
|git stash apply |恢复被隐藏的文件，但是内容不删除|
|git stash drop |删除文件|
|git stash pop |恢复文件的同时 也删除文件|
|git remote |查看远程库的信息|
|git remote –v |查看远程库的详细信息|
|git push origin master  |Git会把master分支推送到远程库对应的远程分支上 |
