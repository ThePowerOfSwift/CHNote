# 常用Shell脚本

## 一、解放生产力

以下脚本需要放入一个可执行文件中，实现双击就可以运行！

### 1.1、快速提交代码

```
# Mac 上可以去掉脚本的第一行标志：「#!/bin/bash」
# 加上这个，颜色码会失效

# 1、cd 到当前目录
currentDir=$(cd "$(dirname "$0")"; pwd)
cd ${currentDir}

# 2、获取当前的分支
currentBranch=$(git symbolic-ref --short HEAD)

# 3、获取提交的信息
echo "\033[32m——-----请输入提交信息(不要输入空格)：🙃——-----\033[0m"
read commitInfo

# 4、提交操作
git add .
git commit -m $commitInfo
echo "\033[32m——-----git 提交完毕🙃—-----\033[0m"

# 5、推送代码
git push -u origin $currentBranch
echo "\033[32m——-----git 推送完毕🙃—-----\033[0m"


sleep 3
exit
```

### 1.2、一步提交 Framework 版本

Carthage 更新版本的快捷命令

```
#!/bin/bash

echo "\033[32m 请输入版本修改信息：🙃🙃🙃🙃🙃 \033[0m"
read commitInfo

git add .
git commit -m $commitInfo

echo "\033[32m 请输入 Tag 版本号(如：1.0.0)：🙃🙃🙃🙃🙃\033[0m"
read tagVersion
echo "\033[32m 请输入 Tag 信息：🙃🙃🙃🙃🙃\033[0m"
read tagInfo

# git tag -a 1.0.5 -m '添加link，解决报错'
git tag -a $tagVersion -m $tagInfo
git push origin --tags
```

### 1.3、重装电脑的脚本

把需要安装的终端环境命令放在一起，实现一键安装。

```
#!/bin/bash

# 安装 Homebrew
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# 安装 node.js
brew install node
# 查看安装版本
npm -v

# 安装 rvm
curl -L https://get.rvm.io | bash -s stable

# 安装 watchman
brew install watchman

# 安装 flow
brew install flow
```

### 1.4、批量添加文件后缀

1. cd 到相应的文件下
2. 执行(添加`.txt`后缀)：`for i in *; do mv "$i" "$i.txt"; done`

### 1.5、Xcode禁用索引

```
# 1、干掉 Xcode
killall Xcode

# 2、禁用 Xcode 建索引
defaults write com.apple.dt.Xcode IDEIndexDisable 1

# 3、打开 Xcode
open /Applications/Xcode.app

# 4、提示用户操作完成，睡眠 2 秒，然后退出
echo "\033[32m+++++Xcode 禁用索引成功！🌚😁🌚🙃🌚😅+++++\033[0m"
sleep 2
exit

# 注意事项：
# 1、第一行不能写这个："#!/bin/bash"，会引起颜色失效，然后会默认弹框
# 2、sleep 时间必须大于等于 2 秒，否则 iTerm2 就会给出弹框提示脚本执行时间过短。。。![](http://oy7b0gogl.bkt.clouddn.com/20180718165809.png)
```

### 1.6、Xcode启用索引

```
# 1、干掉 Xcode
killall Xcode

# 2、禁用 Xcode 建索引
defaults write com.apple.dt.Xcode IDEIndexDisable 0

# 3、打开 Xcode
open /Applications/Xcode.app

# 4、提示用户操作完成，睡眠 2 秒，然后退出
echo "\033[32m+++++Xcode 启用索引成功！🌚😁🌚🙃🌚😅+++++\033[0m"
sleep 2
exit

# 注意事项：
# 1、第一行不能写这个："#!/bin/bash"，会引起颜色失效，然后会默认弹框
# 2、sleep 时间必须大于等于 2 秒，否则 iTerm2 就会给出弹框提示脚本执行时间过短。。。![](http://oy7b0gogl.bkt.clouddn.com/20180718165809.png)
```

### 1.7、批量更换 git 远程仓库地址

总体来说这个脚本不常用，一般公司不会经常更换git仓库地址。

1. cd 到目录
2. 遍历目录
3. 判断目录里面是否包含 .git 文件
4. 执行 git 操作脚本

```
#1、遍历目录
#2、获取目录名称，
#3、拼接远程仓库地址

cd /.../Project01
git remote rm origin    #删除远程仓库关联
git remote add origin http://xxx.com/Project01.git     
git push origin master  #提交代码
git push origin --tags  #提交标签

cd /.../Project02
git remote rm origin    #删除远程仓库关联
git remote add origin http://xxx.com/Project02.git     
git push origin master  #提交代码
git push origin --tags  #提交标签

cd /.../Project03
git remote rm origin    #删除远程仓库关联
git remote add origin http://xxx.com/Project03.git     
git push origin master  #提交代码
git push origin --tags  #提交标签
```


## 二、脚本的其它用途

### 2.1、下载网页到文件中

```
#!/bin/bash

echo "输入需要下载的网址"             # 终端输出提示
read url                           # 读取终端输入
curl http://$url -o web.html       # 下载网页数据到 web.html 文件中
```

### 2.2、使用 until 循环下载

使用 until 循环，接收网址参数，下载网页到 WebDownLoad 文件夹里面的 webX.html 文件中

```
#!/bin/bash

# until 循环条件判断，直到 again 参数为 y
# 接收网址，下载网址到 WebDownLoad 里面

mkdir WebDownLoad # 当前目录下创建 WebDownLoad 文件夹
i=1

until [ "$again" = "y" ]
do
    echo "输入新网址"
    read url
    curl http://$url -o WebDownLoad/web$i.html
    ((i++))

    echo "结束🔚：y/n"
    read again
done
```

### 2.3、读取文件并逐行打印

```
#!/bin/sh

# 使用样例：sh readFile.sh Pngs.text

# 读取一个文件的每一行，并在每一行前面加上索引，然后追加写入到 result.txt 文件中
# $1 表示读取到的文件名
# cat $1 表示文件里面的内容，如果直接在终端 cat xx.text，会在终端显示 xx 里面的内容
# >> 表示追加形式写入文件

i=1
for line in `cat $1`
do
    echo $i+$line >> result.txt
    ((i+=1)) #变量相加只能这样写
done
```

### 2.4、批量下载图片 

#### 2.4.1、读取网址并下载图片

```
#!/bin/bash

# 从输入网址，或者 html 内容，然后把 图片 url 写入到 png.text 文件中
echo "输入需要提取 Png 的网址"
read url
curl -s $url | egrep -o "<img src=[^>]*>" | sed 's/<img src=\"\([^"]*\).*/\1/g' > pngs.text

mkdir WebPNGDownLoad

index=0
for line in `cat pngs.text`
do
    curl $line -o WebPNGDownLoad/png+${index}.png
    ((index+=1))
done
```

#### 2.4.2、读取 html 中的 png 地址并下载

```
# 1、读取 html 文件
# 2、获取文件里面的 img ，
# 3、并写入 test_pngs.text 文件中
cat /Users/yourusername/Desktop/Web/findlifee.com/post/549.html | egrep -o "<img src=[^>]*>" | sed 's/<img src=\"\([^"]*\).*/\1/g' > test_pngs.text
```

### 2.5、遍历文件并依次输出文件

```
# https://blog.csdn.net/u012307002/article/details/51308710

filelist=`ls /Users/yourusername/Desktop/MBProgressHUD/`
for file in $filelist
do 
 # echo $file
 # 下面的OK，不错不错，直接这样读取。。。
 cat /Users/yourusername/Desktop/MBProgressHUD/$file
done
```

### 2.6、递归遍历目录，打印文件名字

```
#!/bin/bash 

# 参考：https://blog.csdn.net/Justine_King/article/details/70288265

function ergodic(){  
    for file in ` ls $1 `  
    do  
        if [ -d $1"/"$file ]   
        then  
             ergodic $1"/"$file  
        else  
             echo "$1/$file" 
        fi  
    done  
}  

INIT_PATH="/Users/yourusername/Desktop/Web/findlifee.com/zb_system"  
ergodic $INIT_PATH 
```

## 三、脚本常见问题说明

### 3.1、脚本执行时间过短问题

否则会给出下面的提示：
![GitHub set up-w400](https://image-1258017831.cos.ap-guangzhou.myqcloud.com/20180718165809.png)

解决方法：

```
sleep 2  # 睡眠2秒，时间只能大于等于2秒，然后再执行退出操作
exit
```

### 3.2、脚本日志颜色显示问题

* 脚本的第一行不能添加：`#!/bin/bash`
* 否则 iTerm2 执行时，不能正常显示日志颜色

### 3.3、脚本日志颜色的显示

字体颜色显示格式：

```
echo -e "[字符串背景颜色码]  [字符串字体颜色码]  字符串  [控制码]"
```

### 3.4、脚本日志换行的两种方式

```
## 1、行尾添加换行符
echo "balabalabala ...\n" 

## 2、输出一个空字符串
echo ""
```