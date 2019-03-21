# GitBook教程

## 一、安装gitbook

安装参考：[Mac GitBook安装和使用](https://www.jianshu.com/p/9f24f8e27fc6)

### 1.1、安装环境准备

* 从[Node网站](https://nodejs.org/en/#download)下载 node.pkg 文件安装即可
* 检查npm是否安装成功：`npm -v`
* 检查node是否存在：`node -v`

### 1.2、安装gitbook

1. 安装Gitbook命令：`sudo npm install -g gitbook-cli`
    1. 注意安装命令一定要加 sudo，否则会出现下面的报错
    2. 命名：`npm install -g gitbook-cli`是安装不成功的
2. 检查是否安装成功：`gitbook -v`

#### 1.2.1、执行 gitbook init 报错
```
You need to install "gitbook-cli" to have access to the gitbook command anywhere on your system.
If you've installed this package globally, you need to uninstall it.
>> Run "npm uninstall -g gitbook" then "npm install -g gitbook-cli"
```

## 二、使用gitbook

使用参考：[GitBook 简明教程](http://www.chengweiyang.cn/gitbook/basic-usage/README.html)

### 2.1、新建书籍

1. 创建新的书籍文件夹，并进入文件夹
2. 执行 `gitbook init` 命令初始化书籍目录
    1. 会生成 `README.md` 和 `SUMMARY.md` 两个必须文件
    2. `README.md` 是对书籍的简单介绍
    3. `SUMMARY.md` 是书籍的目录结构
3. 执行 `gitbook serve` 编译和预览书籍
    1. 会生成文件夹：`_book`，然后可以访问本地网站`http://localhost:4000`来访问书籍
    2. 首先调用 gitbook build 编译书籍
    3. 完成以后会打开一个 web 服务器，监听在本地的 4000 端口
4. serve 启动后，在Book目录下的修改会实时同步到网站`http://localhost:4000`，可以随时预览网站效果

#### 2.1.1、如何关闭gitbook serve

有时候执行 `gitbook serve`，会报错：
```
Error: listen EADDRINUSE: address already in use :::35729
```

**解决方案：**（参考：[mac关闭指定端口](https://blog.csdn.net/mingzznet/article/details/38345875)）

1. 执行 `gitbook serve`，获取服务的端口号：
    1. `Live reload server started on port: 35729`
2. 执行 `lsof -i:35729`，查看端口的进程信息：
    1. `COMMAND  PID USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME`
    2. `node    2771 dd01   23u  IPv6 0x7953faeb24d2c63d      0t0  TCP *:35729 (LISTEN)`
    3. 我们可以获取到 PID 就是 2771
3. 执行 `kill -9 2771`，可以关闭这个进程

#### 2.1.2、注意事项

1. 尽量使用英文的命名，包括文件夹、文件名称
2. 专门的功能模块使用专门的文件夹来方式
3. 文件夹下面的主文件使用README来命名，提交git仓库后可以直接预览

### 2.2、发布书籍

#### 2.2.1、gitbook官网访问问题

* [gitbook官网](https://www.gitbook.com)
* 必须翻墙，可能因为节点不是美国的，还必须选择全局模式
* 难道让我选择：https://love2.io

```
A network error has occurred. The service may be blocked by your ISP or in your area.
```

#### 2.2.2、发布前的步骤

1. 本地创建 GitBook，并进行了预览、调试
2. 上传 GitBook 源文件到 GitHub 仓库

#### 2.2.3、发布书籍

参考：
* [如何在新版的gitbook上写自己的书](https://segmentfault.com/a/1190000015012209)
    * [书籍地址：](https://zhangzhen.gitbook.io/qmake-learn/)
    * [Gitbook GitHub地址](https://github.com/zhangzhen2618/Qt-learn)
    * gitbook 仓库需要包含的文件：`.gitbook.yaml` [参考](https://github.com/zhangzhen2618/Qt-learn/blob/master/.gitbook.yaml)
* [gitbook官方文档](https://docs.gitbook.com)

发布步骤：
1. 先创建 organization
2. 然后再在 organization 下创建一个 space
3. space 下点击更多，点击 integration 关联 GitHub 账号里面的仓库




