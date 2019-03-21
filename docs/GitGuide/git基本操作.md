# Git 基本操作

## 一、git 仓库

### 1.1、本地仓库

* 创建步骤：
    * $ git init
    * $ git add .
    * $ git commit -m 'initial'
* 删除方式：
    * 方法一：$ find . -name ".git" | xargs rm -Rf
    * 方法二：$ rm -rf .git
    * 方法三：直接删除 .git 文件（显示隐藏文件的情况下）

### 1.2、远程仓库

* **查看**远程仓库：$ git remote -v
* **添加**远程仓库：
    * 一般形式添加：$ git remote add origin git@xxx.git
    * 带密码形式添加：$ git remote add origin http://yourusername:password@git.oschina.net/xx-project.git
    * 注：比如同一台Mac操作多个GitHub账号的时候，需要使用到上述命令
* **提交**远程仓库：
    * 主分支提交：$ git push origin master 
    * 开发分支提交：$ git push origin develop
* **拉取**远程仓库： 
    * 主分支拉取：$ git pull origin master 
    * 开发分支拉取：$ git pull origin develop
* **移除**远程仓库：$ git remote rm origin

### 1.3、状态和日志

1. 查看git状态：$ git status
2. 查看有多少暂存：$ git stash list
3. 查看提交历史：$ git log
    1. 注：会按提交时间列出所有的更新，最近的更新排在最上面
4. 查看所有分支的所有操作记录：$ git reflog
    1. 注：包括commit和reset的操作，包括已经被删除的commit记录，git log则不能察看已经删除了的commit记录
5. 暂存：$ git stash  

## 二、git 分支

### 2.1、分支相关操作

1. 查看本地分支：$ git branch  (前面带“星号”的分支表示当前所在的分支)
2. 查看远程分支：$ git branch -r
3. 查看所有分支：$ git branch -a  （远程分支会用红色表示出来（如果你开了颜色支持的话）） 
4. 创建本地新分支：$ git branch newBranchName
5. 切换到本地新分支：$ git checkout newBranchName
6. 推送本地新分支到 origin：$ git push origin newBranchName 
7. 重名名分支：$ git branch (-m | -M) <oldbranch> <newbranch>    (注：m/M 至少选择一个)

### 2.2、删除本地分支

* 删除分支：$ git branch -d branchName 
* 注：-d，表示“在分支已经合并到主干后删除分支”。如果使用大写的-D的话，则表示“不论如何都删除分支”

### 2.3、删除远程分支

删除远程分支，需要先将远程分支下载到本地，然后删除本地，然后提交

1. $ git checkout <branchname>
2. $ git push origin --delete <branchname>
3. $ git push origin: <branchname>

### 2.4、分支管理策略：

可以参照阮一峰的：[Git分支管理策略](http://www.ruanyifeng.com/blog/2012/07/git.html)

* 直接创建develop分支并切换过去：`git checkout -b develop master`
* 切换到Master分支：`git checkout master`
* 对Develop分支进行合并：`git merge --no-ff develop`
    * 使用--no-ff参数后，会执行正常合并，在Master分支上生成一个新节点。为了保证版本演进的清晰，我们希望采用这种做法。
    * 详情请查看：https://sandofsky.com/blog/git-workflow.html

## 三、git 标签

* 参考网址：[Git-基础-打标签](https://git-scm.com/book/zh/v1/Git-基础-打标签) 
* 标签有两种类型：轻量级的（lightweight）和含附注的（annotated），但是不推荐使用轻量级的标签

### 3.1、创建标签

1. 创建一个含附注类型的标签：git tag -a 1.0.0 -m 'tag info'

### 3.2、删除标签：

1. 删除本地：git tag -d 2.0.0
2. 删除远程：git push origin :refs/tags/2.0.0

### 3.3、常用命令

1. 显示标签列表：$ git tag
2. 显示某个标签的详细信息：$ git show v1.0.0
3. 推送本地标签到云仓库：git push origin --tags
4. 后期添加标签：
    1. 查看提交历史：$ git log --pretty=oneline
    2. 某次提交添加标签：$ git tag -a v1.2.1 9fceb02

    







































