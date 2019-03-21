# Git使用指南

git 使用指南整理

## 一、git 各种状态

[秒懂Git的区和状态](http://shengshui.com/?p=2582?zhihu)

### 1.1、首先了解下git所处的4种区 (工作区, 暂存取，本地仓库, 远程仓库) 

![](https://image-1258017831.cos.ap-guangzhou.myqcloud.com/v2-cbfc1a38a47024ef210320af4c220c1e_hd.jpg)

* git add . (git add <file>)  ：加入到暂存区
* git commit -m "add: xxx"  : 加入到本地仓库
* git push origin master : 加入到远程仓库

### 1.2、git的5种状态

* Origin(未修改)
* Modified(已修改)
* Staged(已暂存)
* Committed(已提交)
* Pushed(已推送)

### 1.3、git diff 对比修改

* 已修改，未暂存：git diff
* 已暂存，未提交：git diff --cached
* 已提交，未推送：git diff master origin/master

### 1.4、撤销修改(观看上面的图)

* 已修改，未暂存：git checkout . (git checkout <file>)
* 已暂存，未提交：git reset (git reset --hard 会覆盖)
* 已提交，未推送：git reset --hard origin/master (远程仓库覆盖本地仓库)
* 已推送：git reset --hard <commitID> (如果要覆盖远程必须强制推  git push -f)

[修改Git commit message](http://shengshui.com/?p=2214)

## 二、git 常用命令

* 提交日志：`git log --pretty=oneline`
* 提交日志：`git log --since=2.weeks`（最近两个礼拜的提交）
* 提交日志：`git log --since="2018-04-01"`（某日期开始的提交）
* 提交日志：`git log --author=gitster`（查看某个人的提交）
* 提交日志：`git log --since="2018-04-01" --pretty=oneline`（组合查看）
* 回滚版本：`git reset --hard b70e59944d312fff806b475a81a48bd914fb79ae`
* 设置标签：`git tag -a 1.0.0 -m 'Version1.0.0'`
* 推送标签：`git push origin --tags`
* 查看分支：`git branch`
* 切换分支：`git checkout newBranchName`
* 创建分支：`git branch newBranchName`
* 推送分支：`git push origin newBranchName`