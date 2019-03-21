# 000-Mac 终端工具 

## 一、iTerm2

### 1.1、iTerm2 安装：

* 去官网下载 iTerm2 dmg 文件直接安装就可以了
* iTerm2：[官网地址](https://www.iterm2.com)

### 1.2、oh-my-zsh 安装：

```
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
```

### 1.3、pip 安装：

```
sudo easy_install pip
```

### 1.4、Powerline 安装：

```
pip install powerline-status
```

## 二、Homebrew


### 2.1、安装命令：

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

### 2.2、更新命令：

```
brew update
```

### 2.3、其他命令：

* 使用brew安装软件：`brew install git`
* 使用brew卸载软件：`brew uninstall wget`
* 搜索：`brew search /wge*/`   
    * 使用brew查询软件，其中/wge*/是个正则表达式，需要包含在/中
* 列出已安装的软件：`brew list`
* 打开brew的官方网站：`brew home`
* 显示软件信息：`brew info`
* 显示包依赖：`brew deps`

注意：如果遇到Error: The /usr/local directory is not writable.错误，
就执行以下命令sudo chown -R $(whoami):admin /usr/local，再更新。

## 三、RVM（Ruby Version Manager）

[Ruby China：更多关于 Ruby 的文档](https://ruby-china.org/wiki/rvm-guide)

* Ruby 管理工具 rvm：`curl -L https://get.rvm.io | bash -s stable`
* RVM 版本：`rvm -v`
* 列出已知的 Ruby 版本：`rvm list known`
* Ruby 版本安装1：`rvm install 2.3.0`
* Ruby 版本安装2：`rvm install 2.2.0 --disable-binary`
* 切换 Ruby 版本：`rvm use 2.2.0`
* 设置默认版本：`rvm use 2.2.0 --default`
* 查询已经安装的ruby：`rvm list`
* 卸载一个已安装版本：`rvm remove 1.8.7`

可能会报错如下：

```
To start using RVM you need to run `source /Users/yourusername/.rvm/scripts/rvm` in all your open shell windows, in rare cases you need to reopen all shell windows.
```

解决如下，终端运行：`source /Users/yourusername/.rvm/scripts/rvm`



