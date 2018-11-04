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
因为暂存区的存在，撤销修改分为几种情况（通过 `git status` 查看仓库状态时会提示相关撤销修改的命令）：  
* 修改后，文件没有放入暂存区（即文件一直在工作区）:用 `git checkout --` 文件名 撤销工作区的改动（回到跟版本库一样的状态，即回到最近一次 git commit时的状态，所有改动全部清除）  
* 修改后，文件放入暂存区，且文件没有再次修改（即文件已经进入暂存区）：分两步：先用 `git reset <文件名>` 撤销 `git add` 操作（此时更改仍留在工作区），再执行 git checkout -- 文件名 清除工作区的改动  
* 修改后，文件放入暂存区，且文件再次修改：分三步：先用 git checkout -- 文件名 撤销工作区的改动，再用 git reset <文件名> 撤销 git add 操作（此时更改仍留在工作区），最后执行 git checkout -- 文件名 清除工作区的改动  

 
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

### 查看标签
`git tag`: 可以查看所有标签  

### 删除标签
`git tag -d [tagname]`  

### 查看此版本所修改的内容
`git show [tagname]`

## rebase
git rebase过程相比git merge合并整合得到的结果没有任何区别，但是通过git rebase能产生一个更为整洁的提交历史，合理使用rebase命令可以使我们的提交历史干净简洁。  
常用的场景举例： 
### 将某分支的一段commit粘贴到另一分支上
当我们项目中存在多个分支时，需要将某一个分支中的一段提交同时应用到另一个分支中，如下图:  
![git rebase01](https://github.com/npvip/gitskills/blob/master/img/git02.png)   
实际模拟例子见参考（git rebase用法小结）。  
主要命令如下：  
* rebase复制
```git
git rebase [startpoint] [endpoint] --onto [branchName]
```
其中，`[startpoint]`,`[endpoint]`指的是编辑区间，且是**前开后闭**的，`--onto`是指将指定的
区间复制到分支`[branchName]`上。  
* 处理`HEAD`
执行完复制操作后，才是HEAD还是处于游离状态，如下图所示：  
![git rebase02](https://github.com/npvip/gitskills/blob/master/img/git03.png)  
应切换到上述分支后使用`git reset --hard [logVersion]`，其中[logVersion]指的是复制区间的右边界。  

### 合并多个commit为一个完整commit
当在本地仓库提交多次之后，需要把本地提交push到公共仓库中之前，为了让提交记录更简洁，希望把如下分支B、C、D三个提交记录合并
为一个完整的提交，然后再push到公共仓库。  
![git rebase03](https://github.com/npvip/gitskills/blob/master/img/git04.png)  

使用的命令：`git rebase -i [startpoint] [endpoint]`，其中 -i的意思是弹出交互式界面让用户编辑完成合并操作。  



## 参考
* Git Community Book中文版:http://gitbook.liuhui998.com/4_2.html  
* git rebase用法小结:https://www.jianshu.com/p/4a8f4af4e803  