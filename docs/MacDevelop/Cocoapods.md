# Cocoapods

[cocoapods官网](https://cocoapods.org)

## 一、安装：

### 1.1、安装命令

1. $ sudo gem install -n /usr/local/bin cocoapods
2. $ pod setup

### 1.2、Ruby 源更换：

1. gem sources --remove https://rubygems.org/
2. gem sources -a https://ruby.taobao.org/       
    1. 说明：更换成淘宝的源，方便下载
3. gem sources -l

## 二、使用：

### 2.1、使用：

1. cd 项目目录
2. 创建 Podfile 文件，并添加依赖
3. 执行安装命令：pod install

### 2.2、其他命令：

* 查看ruby版本：ruby -v
* 查看ruby源：gem sources
* 安装cocoapods版本：sudo gem install cocoapods
* 查看cocoapods版本：pod --version
* 更新本地缓存的cocoa pods库为最新：pod setup 
* 查看第三方版本：pod search thirdName

```
$ CocoaPods pod install/pod update更新慢的问题
    $  pod install --verbose --no-repo-update
    $  pod update --verbose --no-repo-update
    $  如果不加后面的参数，默认会升级CocoaPods的spec仓库，加一个参数可以省略这一步，然后速度就会提升不少。
$ 如果编译的时候报 pods 里面的库找不到的错误，执行一下更新 pods 命令
```

### 2.3、更新

```
【汇总命名：sudo gem install cocoapods; pod setup】

【步骤一：】
sudo gem install cocoapods 
sudo gem install cocoapods -v 1.1.1 【安装 1.1.1 版本】
sudo gem install cocoapods --pre    【安装预览版本】   
【步骤二：设置仓库】
pod setup
```

### 2.4、报错解决

解决办法：[CocoaPods使用总结](https://www.jianshu.com/p/e2806f9d9e6f)

```
安装 遇到一个坑：**[!] CocoaPods was not able to update the `master` repo. 
If this is an unexpected issue and persists you can inspect it running `pod repo update --verbose`**

* sudo gem uninstall cocoapods
* sudo gem install cocoapods
* pod setup
* pod install
```



