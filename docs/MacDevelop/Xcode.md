# Xcode

## 常用使用知识

### Xcode Preference 设置：

* 非 Retina 屏幕，Theme 主题推荐：Civic
* Retina 屏幕，Theme 主题推荐：Midnight

### Xcode 下载网址：

* Xcode 正式版下载地址：https://developer.apple.com/download/more/
* Xcode beta 版下载地址：https://developer.apple.com/download/

### Xcode 相关路径：

1. 模板保存路径：`/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Source`
2. 代码块保存路径：
    1. `~/Library/Developer/Xcode/UserData` 没有代码块的路径
    2. `~/Library/Developer/Xcode/UserData/CodeSnippets` 有代码块的路径
3. Archives 路径：`~/Library/Developer/Xcode/Archives/`
4. DerivedData 路径：`~/Library/Developer/Xcode/DerivedData/`
5. Provisioning Profiles 文件夹：`~/Library/MobileDevice/`
6. FrameWork 库路径：`~/Library/Developer/Xcode/DerivedData/Build/Products`

### Xcode 虚拟路径

```
$(SRCROOT)
$(PROJECT_DIR)
$(TARGET_NAME)
$(TARGET_NAME)/Supporting Files/Project.entitlements
```

$(SRCROOT)代表的时项目根目录下
$(PROJECT_DIR)代表的是整个项目

PS：往项目添加文件时，例如.a等，要先show in finder ，复制到项目中，然后再拖到xcode项目中

而有时，我们的.a不在工程目录中，比如在工程的父目录上，可以写成：$(SRCROOT)/../YSKit/libWeChatSDK。其中/../ 就是指向父目录。

https://www.cnblogs.com/muyushifang07/p/4460688.html


### Xcode 自己下载的模拟器路径

`/Library/Developer/CoreSimulator/Profiles/Runtimes/`

直接进入可以删除

模拟器占用内存好大。。。
![](http://oy7b0gogl.bkt.clouddn.com/20180807175857.png)

### Xcode dSYM 文件路径

1. cd 到路径：`~/Library/Developer/Xcode/Archives/`，
2. 然后找到今天打包的文件，选择“显示包内容”获取到DSYM文件。

![](http://oy7b0gogl.bkt.clouddn.com/20180808161821.png)
![](http://oy7b0gogl.bkt.clouddn.com/20180808161829.png)
![](http://oy7b0gogl.bkt.clouddn.com/20180808161841.png)

### Xcode 设置自动打包的时候生成 dSYM 文件

1. Build Setting -> Debug Infomation Format
2. 选择 DWARF with dSYM File
3. 一般默认选择 DWARF

### Xcode 代码块

**1、保存路径：**

`~/Library/Developer/Xcode/UserData/CodeSnippets`

Tips：选中代码，然后单击选中的地方，等鼠标变成箭头就可以进行拖动代码了

**2、代码块设置**

添加操作：选中代码，单击，长按，然后拖动到右下角代码块区域

变量的使用：`<#xxxName#>`
Example：<#mark#>、<#type#>、<#value#>

<#xxxName#>
快速打开代码块所在文件夹：
`open ~/Library/Developer/Xcode/UserData/CodeSnippets`

上面这个目录是你添加了自定义代码块之后才会出现

代码块命名规则说明：

1. vXXX：表示变量(Variable) 的代码块
2. focmethod：表示方法(OC Function) 的代码块
3. fswiftmethod：表示方法(Swift Function) 的代码块
4. mark：表示添加：`// MARK: - XX`

### Xcode 支持 Beta 版本

* 下载：Xcode beta 版下载地址：https://developer.apple.com/download/
* cd 到路径：`Xcode_Beta.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport` 
* 添加到路径：`/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport`

### Xcode使用：支持iOS Beta版本的真机来进行调试

1. 去下载最新的 Xcode Beta 版本：
    1. [Downloads Release Xcode](https://developer.apple.com/downloads/)
    2. [Download Beta Xcode](https://developer.apple.com/download/)
    3. 就是 download 多了一个 s 😂
2. 进入进入目录：`Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport`，导出最新版本的iOS设备镜像文件
3. 导入最新版本的iOS设备镜像文件到目录：`/Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/DeviceSupport`

### Xcode 常用设置命令：

1. Index Disable
    1. `defaults write com.apple.dt.Xcode IDEIndexDisable 1`
    2. `defaults write com.apple.dt.Xcode IDEIndexDisable 0`
    3. 索引有问题，需要删除 DerivedData！
2. 设置显示编译时间
    1. `defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES`
3. 提高XCode编译时使用的线程数
    1. `defaults write com.apple.dt.Xcode PBXNumberOfParallelBuildSubtasks 8`
    2. 4 核CPU时设置 8 个线程编译

### Xcode 清理 DerivedData Archives：

/Users/yourusername/Library/Developer/Xcode/DerivedData
~/Library/Developer/Xcode/DerivedData
~/Desktop/Xcode.app

清除 Archives
rm -rf ~/Library/Developer/Xcode/Archives/*

清除 DerivedData
rm -rf ~/Library/Developer/Xcode/DerivedData/*

查看 Provisioning Profiles 文件夹
~/Library/MobileDevice/
open . 

### Xcode 提高编译速度

**很多设置Xcode已经默认了**

1. 将Debug Information Format改为DWARF**默认**
2. 将Build Active Architecture Only改为Yes**默认**

### Xcode 设置函数和表达式的类型检测（Type checking of functions and expressions）

**可以检查出比较耗时的方法**

在 Build Settings --> Other Swift Flags 中加入

* -Xfrontend -warn-long-function-bodies=100 (100 意味着 100 毫秒, 这个数字具体设置多少要依电脑配置和项目大小而定，建议多调整几遍找到大小相对合适的数字，ps: 1 秒= 1000 毫秒)
* -Xfrontend -warn-long-expression-type-checking=100

### Xcode 命令 clean 项目

* `xcodebuild clean -scheme Amy`

### Xcode 打开多个标签显示文件

使用快捷键：`cmd + T`

### Xcode 使用：可以直接拖图片进去的😂

### Xcode 解决注释快捷键失效的问题

**注释快捷键：Command + option + /** 

注释失效-Xcode快捷键
注释快捷键失效的问题

1. 关闭 Xcode
2. 打开 Finder，重命名 Xcode1.app
3. 打开 Xcode，关闭 Xcode
4. 修复完成

### Xcode 模板设置：导入导出备份等操作


添加读写权限：`sudo chmod  777  /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Source`
拷贝模板到相应目录：`sudo cp -R /Users/yourusername/Desktop/GuowenWang.xctemplate /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Source`


使用脚本来执行保存操作：

```
$ /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File Templates/Source
命令行拷贝 XXX.xctemplate 到 Xcode 中： 
$ sudo cp -R /Users/yourusername/Desktop/XXX.xctemplate /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Templates/File\ Templates/Source
如果想随时修改模板，需要给自己的模板路径添加权限
$ sudo chown -R "$USER”:admin 路径
```

## Info.plist 设置

### 1、设置 Http 网络请求

```
<key>NSAppTransportSecurity</key>
<dict>
	<key>NSAllowsArbitraryLoads</key>
	<true/>
</dict>
```

### 2、设置权限访问提示语

```
<key>NSAppleMusicUsageDescription</key>
<string>&quot;XXX-App&quot;需要您的同意,才能访问媒体资料库</string>
<key>NSMicrophoneUsageDescription</key>
<string>&quot;XXX-App&quot;需要您的同意,聊天时才能访问麦克风 </string>
<key>NSPhotoLibraryUsageDescription</key>
<string>&quot;XXX-App&quot;需要您的同意,上传头像,聊天时才能访问相册 </string>
<key>NSCameraUsageDescription</key>
<string>&quot;XXX-App&quot;需要经过您的同意,上传头像,用户评价才能访问相机 </string>
<key>NSLocationAlwaysUsageDescription</key>
<string>&quot;XXX-App&quot;需要经过您的同意,才能始终访问位置,用于查询附近服务信息和导航</string>
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>&quot;XXX-App&quot;需要经过您的同意,才能在使用期间获取您的位置,查询附近服务信息,添加地址和导航</string>
<key>NSLocationWhenInUseUsageDescription</key>
<string>&quot;XXX-App&quot;需要经过您的同意,才能在使用期间获取您的位置,查询附近服务信息,添加地址和导航</string>
```

### 3、设置白名单

```
<key>LSApplicationQueriesSchemes</key>
<array>
	<string>iosamap</string>
	<string>baidumap</string>
	<string>wechat</string>
	<string>weixin</string>
	<string>sinaweibohd</string>
	<string>sinaweibo</string>
	<string>sinaweibosso</string>
	<string>weibosdk</string>
	<string>weibosdk2.5</string>
	<string>mqqapi</string>
	<string>mqq</string>
	<string>mqqOpensdkSSoLogin</string>
	<string>mqqconnect</string>
	<string>mqqopensdkdataline</string>
	<string>mqqopensdkgrouptribeshare</string>
	<string>mqqopensdkfriend</string>
	<string>mqqopensdkapi</string>
	<string>mqqopensdkapiV2</string>
	<string>mqqopensdkapiV3</string>
	<string>mqqopensdkapiV4</string>
	<string>mqzoneopensdk</string>
	<string>wtloginmqq</string>
	<string>wtloginmqq2</string>
	<string>mqqwpa</string>
	<string>mqzone</string>
	<string>mqzonev2</string>
	<string>mqzoneshare</string>
	<string>wtloginqzone</string>
	<string>mqzonewx</string>
	<string>mqzoneopensdkapiV2</string>
	<string>mqzoneopensdkapi19</string>
	<string>mqzoneopensdkapi</string>
	<string>mqqbrowser</string>
	<string>mttbrowser</string>
	<string>alipay</string>
	<string>alipayshare</string>
</array>
```

### 4、设置回调 Scheme 

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLIconFile</key>
        <string></string>
        <key>CFBundleURLName</key>
        <string>weixin</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>wx0abcf149bf24a596</string>
        </array>
    </dict>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string></string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>alipayabcf149bf4a596</string>
        </array>
    </dict>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>WLSH</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>wlsh</string>
        </array>
    </dict>
</array>
```


