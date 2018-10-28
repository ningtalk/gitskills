# Git操作记录
git基本操作.  

## 基本操作
### 工作区和暂存区
* 工作区：工作的文件目录下    
* 版本库：工作区有一个隐藏目录.git，是版本库    
![工作区和暂存区](https://github.com/npvip/gitskills/blob/master/img/git01.jpeg)  
往版本区里添加的时候，分两步执行：  
1. `git add`:把文件修改添加到暂存区；  
2. `git commit`:把暂存区的左右内容提交到当前分支。  

### 状态查看  
* `git status`:查看当前分支的工作区状态。  
* `git diff`:查看文件有哪些具体修改。  
```git
git diff readme.txt
```

### 版本回退
* `git reset --hard [版本id]`

### 撤销修改
* `git checkout -- file`
 命令`git checkout -- readme.txt`是把文件readme.txt文件在工作区的修改全部撤销，有两种情况:  
 1. readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；  
 2. readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。  
 也就是让这个文件回到最近一次git commit或git add时的状态。  
 
## 查看提交历史
`git log`: 查看由近及远的提交日志，查看时要退出按`Q`   
`git log --oneline`: 查看历史提交记录简洁版本  
`git log --oneline --graph`: 可以查看历史中什么时候出现分支、合并  
`git log --reverse --oneline`: 查看由远及近的提交日志（逆向）  
`git log --auhtor=[username] --oneline -5`: 查看某用户的提交日志  
 
## 远程仓库 
远程仓库是指托管在因特网或其他网络中的你的项目的版本库。  
### 查看远程仓库  
`git remote`:此命令会列出你指定的每个远程仓库的简称。  
`git remote -v`:此命令会显示需要读写远程仓库使用的Git保存的简称和url。  
`git remote show origin`:
### 添加远程仓库
`git remote add <shortname> <url>`:此命令添加一个新的远程 Git 仓库。  
```
$ git remote add pb https://github.com/npvip/gitskills.git
```
如果想拉去pb仓库中有而你本地仓库没有的信息，可以运行`git fetch pb`  
### 从远程仓库拉取
`git fetch [remote-name]`:  
该命令会访问远程仓库，从中拉取所有你还没有的数据。  
### 推送到远程仓库
`git push [remote-name] [branch-name]`:  

### 远程仓库的移除与重命名
`git remote rename [old shortname] [new shortname]`:重命名  
`git remote rm [old shortname]`:移除  

## 分支
### 分支创建
`git branch testing`:创建分支testing  
`git log --oneline --decorate`:查看分支当前所指对象  
### 分支切换
`git checkout testing`:切换到testing分支  
`git checkout -b [分支名]`:创建并切换到分支  

### 删除分支
`git branch -d [branchname]`  

### 合并分支
`git merge`: 合并分支到当前分支  

## 标签
项目达到一个重要的阶段，并且希望永远记住那个特别的提交快照，可以使用`git tag`給它打上标签。  
`git tag -a v1.0`

