# Git skills
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
* git status:查看当前分支的工作区状态。  
* git diff:查看文件有哪些具体修改。  
```git
git diff readme.txt
```
* git log:查看由近到远的提交日志。
* git log --pretty=oneline:简洁版查看提交日志  

### 版本回退
* git reset --hard [版本id]

### 撤销修改
* git checkout -- file
 命令`git checkout -- readme.txt`是把文件readme.txt文件在工作区的修改全部撤销，有两种情况:  
 1. readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；  
 2. readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。  
 也就是让这个文件回到最近一次git commit或git add时的状态。  