# Mac使用

##  一、Mac认识

### 1.1、键盘按键标识认识

* ⌘ Command
* ⇧ Shift
* ⌥ Option
* ⌃ Control
* [Mac键盘符号和修饰键说明](https://www.jianshu.com/p/f46a5f5dfed7)
* [Mac—如何输入⌘、⌥、⇧、⌃、⎋等特殊字符](http://newping.cn/447)
* [⌘ 符号的由来](https://www.zhihu.com/question/56494826)
    * ⌥ 这个符号，是一个铁路分成两道

### 1.2、查看Mac电脑核心数量

1. 直接点击左上角🍎标志，
2. 关于本机
3. 系统报告
4. 在右边的系统概览里面可以查看的到，核心数

### 1.3、查看屏幕尺寸

1. 直接点击左上角🍎标志，
2. 关于本机
3. 显示器：就可以查看屏幕大小，分辨率

### 1.4、清除缓存

* 去到这个目录下进行：
* `/Users/YourUserName/Library/Group\ Containers`
* [OmniDiskSweeper文件大小扫描软件](https://www.omnigroup.com/more)

##  二、Mac设置

### 2.1、系统偏好设置

#### 开机启动设置

* 设置 -> 用户群组 -> 登录项：添加启动项：ShadowSocket

### 1.2、Finder 设置

* 通用
    * 「开启新 Finder 窗口时打开」项下选择你喜欢的目录即可
* 边栏：
    * 去掉所有文件
    * 勾选 Home
    * 去掉共享
* 显示
    * 显示状态栏
* 高级
    * 勾选第一个：【显示所有文件扩展名】
* 标题显示路径：
    * 打开任意 Finder 窗口。前往并打开「显示」－「显示路径栏」 
    * 打开任意 Finder 窗口。前往并打开「显示」－「显示状态栏」 
    * `defaults write com.apple.finder _FXShowPosixPathInTitle -bool TRUE;killall Finder`
    * 还原：`defaults delete com.apple.finder _FXShowPosixPathInTitle;killall Finder`

### 2.3、终端 shell 设置

1. 设置可以安装所有软件：
    1. `$ sudo spctl --master-disable`
2. 让 Finder 显示路径：
    1. `$ defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES`
3. 显示隐藏文件：
    1. `$ defaults write com.apple.finder AppleShowAllFiles -boolean true ; killall Finder`
4. 隐藏隐藏文件：
    1. `defaults write com.apple.finder AppleShowAllFiles -boolean false ; killall Finder`
5. 获取 ssh key：
    1. `$ vim ~/.ssh/id_rsa.pub`
    2. `$ cat ~/.ssh/id_rsa.pub`

### 2.4、xxx.app已损坏,打不开.你应该将它移到废纸篓

xxx.app已损坏,打不开.你应该将它移到废纸篓」，并非你安装的软件已损坏，而是Mac系统的安全设置问题，因为这些应用都是破解或者汉化的,那么解决方法就是临时改变Mac系统安全设置。

出现这个问题的解决方法：
修改系统配置：系统偏好设置... -> 安全性与隐私。修改为任何来源
如果没有这个选项的话（macOS Sierra 10.12）,
打开终端，
执行 `sudo spctl --master-disable` 即可。

### 2.5、国外网友推荐的 Mac 设置：

* [💻 a list of applications, alfred workflows and various tools that make my macOS experience even more amazing](https://github.com/nikitavoloboev/my-mac-os)

##  三、Mac使用

### 3.1、常用快捷键

1. 桌面切换：`Control + 左右方向键`
2. F1 设置成 Misson Control：`设置 -> 键盘 -> 快捷键 -> Misson Control -> 第一个Misson Control设置成 F1`

### 3.2、mac 多屏幕设置主屏幕

* 设置 -> 显示器 -> 排列 -> 然后拖动`白条`
* 拖到哪个屏幕哪个屏幕就是主屏幕(主屏幕：就是会显示桌面上文件的屏幕)

### 3.3、设置 24 小时制

* 设置 -> 语言与地区 -> 时间格式：勾选☑️一下
* 设置，日期与时间里面是设置不了的

### 3.4、修改 Host

1. 右键 Finder选择：`前往文件夹`
2. 输入地址：`/private/etc/`
3. 拷贝 hosts 文件到桌面，进行修改操作
4. 拖回目录：`/private/etc/`

### 3.5、Spotlight 搜索结果在 Finder 中显示

同时按住：`cmd`+`回车`键

### 3.6、Wi-Fi

#### 3.6.1、设置优先连接哪个 Wi-Fi

1. 系统设置 -> 网络
2. 右边栏，在`网络名称`列表中选择需要设置的WiFi名称，勾选`自动加入此网络`
3. 右边栏，在`网络名称`列表中选择其他的WiFi名称，不勾选`自动加入此网络`
4. 这个设置方法好像没啥用：
    1. 设置 -> 网络 -> WiFi ->  高级 -> WiFi连接列表，拖动顺序即表示优先级

#### 3.6.2、不能上网，但是可以ping通

* 设置 -> 网络 -> 顶部的**位置**，添加一个新的就可以了
* 添加 VPN 后无法上网：位置重新设置为原来的自动就好
* 参考：[Mac突然无法上网](https://www.jianshu.com/p/ad92af9ac754)

#### 3.6.3、Wi-Fi 二维码创建：

* 例子：WIFI:T:WPA;S:Wi-Fi名;P:密码;;
* 格式：WIFI:T:WPA;S:wifiname;P:wifipasswd;;
* 说明：
    * WIFI 表示这个是一个连接 WiFi 的协议
    * S 表示后面是 WiFi 的 SSID，wifiname 也就是 WiFi 的名称
    * P 表示后面是 WiFi 的密码，wifipasswd 是 WiFi 的密码
    * T 表示后面是密码的加密方式，WPA/WPA2 大部分都是这个加密方式，也使用WPA。如果写WPA/WPA2我的小米手机无法识别。
    * H 表示这个WiFi是否是隐藏的，直接打开 WiFi 扫不到这个信号。苹果还不支持隐藏模式

#### 3.6.4、AirDrop 突然变得很慢

按住 option 点击右上角 wifi 标志
查看最下面那边的 PHY 模式
如果是 ac ，传输速度应该 OK 的
如果是 n / g，传输速度就会很慢
[参考](https://www.macx.cn/thread-2169221-1-1.html)

### 3.7、App Store

#### 3.7.1、App Store 异常，下载的时候，一直提示登录

去设置里面，选择 App Store，然后退出登录，然后干掉 App Store app，再次进入就可以下载了

#### 3.7.2、iPhone App 没有更新，或者看不大更新按钮

需要搜索 App，然后进入 app 介绍详情界面里面去才可以看到更新按钮。。。

### 3.8、Time Machine

使用 Time Machine 备份电脑需要先格式化硬盘（硬盘格式要求不同😂） 

### 3.9、QuickTime Player

#### 3.9.1、进行视频剪切：进行简单的剪切

直接使用 **QuickTime Player** 
点击左上角菜单栏：编辑，选择：修剪（快捷键 cmd + t ）

#### 3.9.1、进行投屏：把iPhone屏幕投射到Mac


### 3.10、Safari 

1. 开启调试：[使用 Safari 的“开发”菜单](https://support.apple.com/zh-cn/guide/safari/use-the-safari-develop-menu-sfri20948)
2. 安装扩展：其实只要双击就好了😂。。。
3. 翻译扩展：[Polyglot](https://github.com/uetchy/Polyglot)

#### 3.10.1、在 Safari 中模拟 Apple 设备

1. 选取“开发”>“进入响应式设计模式”。
2. 点按位于页面顶部的设备。
3. 如果您未在菜单栏中看到“开发”菜单，请选取“Safari”>“偏好设置”，点按“高级”，然后选择“在菜单栏中显示开发菜单”。

#### 3.10.2、Safari 在不同的电脑之间不能同步书签

在不能同步的电脑上：进入设置，iCloud，退出登录，然后再次登录

### 3.11、Mac-iPhone：投屏

1. 数据线连接 iPhone
2. 选择 QuickTime 
3. 菜单栏 -> 文件 -> 新建影片录制
4. 点击录制界面下面中央的菜单红远点旁边的向下的箭头
5. 选择 iPhone

### 3.12、Mac exec 可执行文件的创建

* `touch xxx`
* 编辑 xxx，填写 shell 命令
* `chmod +x xxx`
* xxx 文件就会变成 exec，双击就可以运行

### 3.13、联系 Apple 支持

* 直接进入下面的网站，苹果那边会打电话过来
* 个人账号硬件等问题：
    * https://support.apple.com/zh-cn/contact
* 开发者所有问题：
    * https://developer.apple.com//contact/#!/topic/select

### 3.14、设置 Mac 接电话☎️

* Mac 设置：
    * iCloud 登录 Apple 账号    
* iPhone 设置：
    * iCloud 登录 Apple 账号 
    * FaceTime 登录 Apple 账号(默认可能没有登录)
    * 设置->电话->在其他设备上通话->允许，并勾选设备

### 3.15、字体文件夹

`/Library/Fonts`

### 3.16、Workflow 

* 列表：http://workflow.sspai.com/#/main/workflow
* workflow and Transloader 联动
    * workflow：创建一个切割文本的，循环发送到 Transloader
* [在 Workflow 应用中创建新的工作流程](https://support.apple.com/zh-cn/HT208314)
* [Workflow 思路教程](https://sspai.com/post/36359)

### 3.17、使用Mac预览功能实现图片拼接

1. 需要拼接的图片全选
2. 在预览左边👈列表栏，点击第一张图片，光标切换到画布上，全选并剪切（「Command+A」「Command+X」）
3. 然后通过「工具-调整大小」来调整画布尺寸，看需要横拼还是竖拼，设置响应的宽高
4. 调整成功后用「Command+V」将图 1 粘贴上去
5. 依次在预览左边👈列表栏，选择其他图片，拷贝到第一个图片画布上，就可以实现图片拼接了
6. 注意：
    1. **其实可以设置成一个超级大的画布，然后来进行各种自由拼接**
    2. **图片层级会严格遵循添加顺序，暂时还没找到怎么切换顺序的按钮**
7. [参考](https://zhuanlan.zhihu.com/p/27993586)

### 3.18、Xcode

#### 3.18.1、触摸板怎么拖Xcode约束：

需要按住 control 键，然后三指移动

#### 3.18.2、Xcode注释快捷键失效的问题

**Command + option + /** 
注释失效-Xcode快捷键/注释快捷键失效的问题

1. 关闭 Xcode
2. 打开 Finder，重命名 Xcode1.app
3. 打开 Xcode，关闭 Xcode
4. 修复完成




## 四、Mac其他软件使用

### 4.1、百度网盘破解

准备材料：

1. Chrome 浏览器
2. Chrome 插件（.crx）
3. 神器：aria2 

【神器aria2】。就这三个东西，简单不？不需要进入终端，不需要输入代码，纯傻瓜式操作

### 4.2、Mac下载图片

* Chrome 插件一：fatkun
    * 插件官方地址：https://chrome.google.com/webstore/detail/fatkun-batch-download-ima/nnjjahlikiabnchcpehcpkdeckfgnohf
* Chrome 插件二：云图 
    * https://chrome.google.com/webstore/detail/picloud-free-image-hostin/bihglmgabibjhgoapmnoddjmmjjpanid/related

### 4.3、微信备份文件存放路径：

* `~/Library/Containers/com.tencent.xinWeChat/Data/Library/Application Support/com.tencent.xinWeChat/`
* `/Users/yourusername/Library/Containers/com.tencent.xinWeChat/Data/Library/Application\ Support/com.tencent.xinWeChat/2.0b4.0.9/Backup`

### 4.4、如何用最快的速度给证件照换底色？

1. 打开你的word/excel/ppt
2. 上方菜单栏“插入” ——“图片”——选择自己的证件照。
3. “图片工具”下，上方菜单栏“格式”——最左侧“删除背景”。
4. 将图片上的覆盖范围改为最大（紫色覆盖整个照片）
5. 上方菜单栏“标记要删除的区域”——点击背景中没有被紫色覆盖的区域。
6. 上方菜单栏“标记要保留的区域”——点击衣服，面部等需要保留的区域。
7. 上方菜单栏“保留更改”（可以看到刚才照片紫色的区域，也就是照片的背景已经被删除掉了）
8. 上方菜单栏“开始”——“主题颜色”（就是那个油漆桶图标）选择自己喜欢的底色～
9. 完成～喝口气水儿奖励自己～

### 4.5、Google 浏览器使用

Google 浏览器地址栏如果有中文，拷贝的时候回自动转码，然鹅Safari不会😂

## 五、Mac设备使用：

### 5.1、Mac忘记密码

#### 方法一：单用户模式更改原来用户账号密码

1. 开机启动时按 cmd+S，进入 Single User Mode
2. 在:/ root#下 输入 mount -uaw / 回车
3. 完成后，输入 rm -rf /var/db/.AppleSetupDone 按下回车键，如果没有任何报错信息，则表明执行成功。
4. 输入 reboot 重新启动

在新的管理员下打开**用户与群组**，打开最下面的锁，问密码时，用新的管理员的帐号的密码。
你会看到至少两个账号，新的管理员的帐号和你原来的帐号，点中原来的账号，选择更改密码。 
你不必有原先的密码就直接可以设新密码。
点下面的登陆选项 ，自动登录选中你原先的账号，重启即可。

#### 方法二：进入 OS X 恢复模式重置

前提：没有开启 **FileVault(文件保险库)** 功能！

1. 按住 Command + R（⌘R） 组合键，并点按开机按钮，直到出现  标志，进入恢复模式（Recovery Mode）（当然，你也可以先按开机键，在听到启动声后，立即按住 ⌘R 键）
2. 选择「以简体中文作为主要语言」（或其他语言），点击向右的箭头
3. 在顶部菜单栏选择「实用工具」
4. 继续选择「终端」
5. 在终端中输入命令（注：连写，且均为小写字母）：resetpassword，回车确认
6. 在出现的「重设密码」窗口中，依次选择包含密码的启动磁盘卷宗、希望重设的用户账户
7. 输入并确认新的用户密码，并为其设置密码提示信息（可选）；点击「重设」
8. 点击菜单栏中的 ，并选择「重启」或「关机」。下次启动时，使用新密码登录即可

#### FileVault

* FileVault 在设置-安全性与隐私中设置
* FileVault 通过自动对磁盘内容进行加密来保护磁盘上的数据。

### 5.2、Mac重装系统

1. 开机按住 option 键，查看是否装了双系统
2. 开机按住 cmd + r 键(点按是不行的，就是要按住不放)，进入重装系统准备界面，然后进行相应的操作就可以了
3. 给移动硬盘装系统也类似:
    1. 先把移动应胖插到 mac 上，然后按住 cmd + r 键开机 

### 5.3、Mac 备份系统到另外一台电脑上

1. 迁移助手的使用：https://support.apple.com/zh-cn/HT204350
2. 可以直接使用软件拷贝全部内容到另外一个移动硬盘上

### 5.4、Mac路径：iPhone 备份路径

`~/资源库/Application Support/MobileSync/Backup`

### 5.5、备份：旧手机数据备份到新手机-指南

1. 删除视频类 App
2. 先把照片视频全部转移，然后在旧手机上删除
    1. 使用 mac 上的**图像捕捉**功能，能一步到位完成这个操作
3. 两台手机升级到相同的 iOS 系统
4. 旧手机备份
5. 恢复备份到新手机

如果您忘记了加密备份的密码：
如果没有密码，您将无法恢复加密备份。在 iOS 11 或更高版本中，您可以通过重设密码来为设备创建新的加密备份。以下是操作方法：
1. 在 iOS 设备上，前往“设置”>“通用”>“还原”。
2. 轻点“还原所有设置”，然后输入您的 iOS 密码。
3. 按照相关步骤还原您的设置。这不会影响您的用户数据或密码，但会还原显示屏亮度、主屏幕布局和墙纸等设置，还会移除您的加密备份密码。
4. 重新将设备连接到 iTunes，然后创建新的加密备份。









