# Git 常用操作

## 一、git 管理用户名

### 1.1、全局配置

* 全局设置用户名：$ git config --global user.name "XXXX"
* 全局设置邮箱：$ git config --global user.email "XXXX@gmail.com"
* 全局设置查看命令：$ git config -l

### 1.2、局部配置 

注：项目单独配置的用户名具有比全局配置的用户更高优先级

#### 1.2.1、使用命令设置

* 局部设置用户名：$ git config user.name "XXXX"
* 局部设置邮箱：$ git config user.email "XXXX@gmail.com"
* 设置查看命令：$ git config --list

#### 1.2.2、直接修改文件

1. 进入 .git 目录，找到 config 文件并打开
2. 修改 config 文件添加用户名和邮箱：

```
[user]
    name = XXXX
    email = XXXX@foxmail.com
```

## 二、git 撤销回滚

### 2.1、撤销当前修改

撤销当前的修改：$ git reset —hard

### 2.2、回滚到某次提交

回滚代码到某个版本
git reset --hard f8b05d07dc9220e79387b9a183e9ebaab97257cd
git reset –soft f8b05d07dc9220e79387b9a183e9ebaab97257cd 
会将之间的修改全部进行revert,然后在进行add commit操作就行了.

重置到某一版本：$ git reset 1d7f5d89346
恢复最后一次暂存的改动：$ git stash pop

### 2.3、回滚到标签

1. 先 git clone 整个仓库
2. 然后 git checkout tag_name 就可以取得 tag 对应的代码了
3. 但是这时候 git 可能会提示你当前处于一个“detached HEAD" 状态，因为 tag 相当于是一个快照，是不能更改它的代码的，如果要在 tag 代码的基础上做修改，你需要一个分支：git checkout -b branch_name tag_name，这样会从 tag 创建一个分支，然后就和普通的 git 操作一样了。

## 三、git 代码冲突

1. 提交代码到本地 Git
2. 拉取代码，发现冲突：会显示冲突文件

### 3.1、解决方法一：直接打开文件修改

1. Finder 中打开冲突文件
2. 搜索关键词，快速定位冲突地方：**<<<<<<<** / **>>>>>>>** / **HEAD**，
3. 解决冲突
    1. 去掉被人代码
    2. 去掉自己的代码
    3. 合并代码

### 3.2、解决方法二：使用 Sourcetree 工具

1. Sourcetree 打开工程
2. 提交修改到本地
3. 拉取远程代码，发现冲突文件
4. 右键冲突文件，选择**解决冲突**：
    1. 方式一：外部合并工具，选择**Action**，比如保存两者
    2. 方式二：使用**我的版本**，会直接修改
    3. 方式三：使用**他人版本**，会直接修改
5. 提交合并代码的操作
6. 推送到远端

## 四、git 忽略文件

在git中如果想忽略掉某个文件，不让这个文件提交到版本库中，可以使用修改根目录中 .gitignore 文件的方法（如无，则需自己手工建立此文件）。这个文件每一行保存了一个匹配的规则例如：

```
# 此为注释 – 将被 Git 忽略
 
*.a       # 忽略所有 .a 结尾的文件
!lib.a    # 但 lib.a 除外
/TODO     # 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
build/    # 忽略 build/ 目录下的所有文件
doc/*.txt # 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```

规则很简单，不做过多解释，但是有时候在项目开发过程中，突然心血来潮想把某些目录或文件加入忽略规则，按照上述方法定义后发现并未生效，原因是.gitignore只能忽略那些原来没有被track的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。那么解决方法就是先把本地缓存删除（改变成未track状态），然后再提交：

```
git rm -r --cached .
git add .
git commit -m 'update .gitignore'
```

## 五、git 记住密码

让本地快速提交、记住密码的三种方法：

1. 带密码形式的添加远程仓库：
    1. git remote add origin http://yourUsername:password@git.oschina.net/name/project.git
    2. git remote add origin http://yourUsername:yourPassword@xxx.com/xxproject.git
2. 设置存储密码：
    1. 长期存储：git config --global credential.helper store
    2. 默认15分钟：git config --global credential.helper cache
    3. 自定义保存时长：git config credential.helper 'cache --timeout=3600' （**保存一小时**）
3. 添加 SSH Key：
    1. 生成SSH：`ssh-keygen -t rsa -C "XXXX@gmail.com"`
    2. 查看SSH：`cat ~/.ssh/id_rsa.pub`

## 六、git 修改仓库名

* 修改仓库名：$ git remote rename  oldname newname  (一般oldname是origin) 
* 注：以后推送时执行的命令就不再是 git push origin master  而是 git push newname master 拉取也是一样的

## 七、git 其他使用

### 7.1、SSH Key：常用命令

1. 生成 SSH Key：`ssh-keygen -t rsa -C "XXXX@gmail.com"`（一路回车，或者设置一个密码）
2. 拷贝 SSH Key：`cat ~/.ssh/id_rsa.pub`
3. 添加 SSH Key：
4. 测试 SSH Key：`ssh -T git@git.oschina.net`
5. 获取 ssh key 方法一：`vim ~/.ssh/id_rsa.pub`
6. 获取 ssh key 方法一：`cat ~/.ssh/id_rsa.pub`

### 7.2、SSH Key：关于码云可能添加不了 SSH Key 的坑，解决办法：

1. ping gitee 网址：`ping gitee.com`，获取 ip 地址
2. 添加`218.11.0.86	gitee.com`到`/etc/hosts`文件中
3. 第二步应该会遇到无法编辑的情况，解决方法：
    1. 拖动`hosts`文件到桌面
    2. 编辑`hosts`文件
    3. 拖回`/etc/`路径，选择`鉴定`，输入登录密码，搞定！！！
4. ssh -T git@git.github.com(52.74.223.119)

### 7.3、SSH 提交方式，多用户的情况下配置：

* [SSH：Git多用户，不同项目配置不同Git账号](https://blog.csdn.net/onTheRoadToMine/article/details/79029331)
* [同一客户端下使用多个git账号](https://www.jianshu.com/p/89cb26e5c3e8)
