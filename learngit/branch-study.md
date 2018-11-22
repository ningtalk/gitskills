# branch-分支学习

## 查看分支
* git branch // 查看本地分支
* git branch -a // 查看本地及远程所有分支

## 切换分支
* git checkout <branchname> // 切换到分支<branchname>

## 创建分支
* git branch <branchname> // 以当前分支为基准创建新分支<branchname>
* git checkout -b <branchname> // 创建新分支并切换到该分支


## 实际场景

### 根据远程某分支创建本地分支
远程仓库有分支 master,dev，需要在本地创建一个分支mydev以远程分支dev为准。  
步骤：
1. 克隆远程仓库: git clone https://github.com/npvip/gitskills.git
2. 创建并切换到分支mydev: git checkout -b mydev origin/dev
