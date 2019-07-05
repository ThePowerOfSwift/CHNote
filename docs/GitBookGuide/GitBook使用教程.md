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

#### 2.1.1、如何关闭 gitbook serve

* 正常情况下 control + c 组合键就能关闭 serve，但是也会有时出错。
* 有时候执行 `gitbook serve`，会报错：

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

## 三、脚本控制gitbook

### 3.1、快速开启Serve

```
function open_gitbook_chnote() {
	# 1、到达书籍根目录
	currentDir=$(cd "$(dirname "$0")"; pwd)
	cd ${currentDir}
	# 2、开启 gitbook
	gitbook --port 5000 --lrport 5001 serve
	echo "\033[32m=======gitbook serve 完成：🙃 ===========\033[0m"
	# 3、使用 safari 打开地址，下面的命令其实并不会执行
	#sleep 3
	#open -a Safari http://localhost:5000
}

open_gitbook_chnote
```

### 3.2、快速关闭Serve

```
function close_gitbook_chnote() {
	# 1、根据端口号查询对应的pid
	pid=$(lsof -i:5000 | grep node | awk '{print $2}')
	# 2、根据pid杀死进程

	if [  -n  "$pid"  ];  then
		echo "找到了正在执行的进程"
	    kill  -9  $pid;
	else
		echo "没有找到相关进程"
	fi

	sleep 3
}

close_gitbook_chnote
```

### 3.3、端口的设置问题

* 如果有多个gitbook需要本地开启端口设置可以如下：
* gitbook 1： gitbook --port 5000 --lrport 5001 serve
* gitbook 2： gitbook --port 5002 --lrport 5003 serve

### 3.4、参考

* [Linux/macOS 获取进程PID、杀死进程](https://blog.csdn.net/Etheo_W/article/details/79230663)
* [shell脚本中根据端口号kill对应的应用进程](https://blog.csdn.net/KingBoyWorld/article/details/78511319)

