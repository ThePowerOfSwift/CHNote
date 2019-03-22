# Carthage

## 一、常用命令

* 更新命令：`carthage update --platform iOS`
* 添加支持：`carthage build --no-skip-current`
* 添加支持：`carthage build --no-skip-current --platform iOS`
    * 只生成 iOS 平台的

## 二、使用教程

### 2.1、安装命令：

```
$ brew install Carthage         //安装
$ carthage version              //查看 Carthage 版本
$ brew upgrade carthage         //升级
$ sudo brew uninstall carthage  //卸载
```

### 2.2、使用步骤：

```
1、创建一个空的carthage文件
    $ touch Cartfile
2、使用Xcode打开该文件
    $ open -a Xcode Cartfile
3、编辑Cartfile
    $ github "SVProgressHUD/SVProgressHUD" ~> 1.0
    $ Cartfile 格式说明 
    $ 依赖源 Dependency origin，Carthage 支持两种类型的源，一个是github，另一个是git。
        $ github 表示依赖源，告诉Carthage去哪里下载文件。依赖源之后跟上要下载的库，格式为Username/ProjectName
        $ git 关键字后面跟的是资料库的地址，可以是远程的URL地址，使用git://, http://, ssh://，或者是本地资料库地址。
4、运行 Carthage 执行以下命令：保存并关闭Cartfile文件，回到终端，
    $ carthage update --platform iOS
5、升级指定Frameworks
    $ carthage update SVProgressHUD --platform iOS
6、添加FrameWorks到项目中  目的是告诉Xcode链接你的app到这个framework，允许你在代码中使用。
    $ General ——> Embedded Binaries ——> add 
7、选择菜单上的Build Phases，并添加一个新的Run Script，并添加以下命令：
    $ /usr/local/bin/carthage copy-frameworks （carthage copy-frameworks命令剔除了额外的框架）
    $ 点击Input Files下面的+号为每一个framework添加条目：
        $ $(SRCROOT)/Carthage/Build/iOS/SVProgressHUD.framework
```

### 2.3、还需添加的 Run Script：

```
APP_PATH="${TARGET_BUILD_DIR}/${WRAPPER_NAME}"

# This script loops through the frameworks embedded in the application and
# removes unused architectures.
find "$APP_PATH" -name '*.framework' -type d | while read -r FRAMEWORK
do
FRAMEWORK_EXECUTABLE_NAME=$(defaults read "$FRAMEWORK/Info.plist" CFBundleExecutable)
FRAMEWORK_EXECUTABLE_PATH="$FRAMEWORK/$FRAMEWORK_EXECUTABLE_NAME"
echo "Executable is $FRAMEWORK_EXECUTABLE_PATH"

EXTRACTED_ARCHS=()

for ARCH in $ARCHS
do
echo "Extracting $ARCH from $FRAMEWORK_EXECUTABLE_NAME"
lipo -extract "$ARCH" "$FRAMEWORK_EXECUTABLE_PATH" -o "$FRAMEWORK_EXECUTABLE_PATH-$ARCH"
EXTRACTED_ARCHS+=("$FRAMEWORK_EXECUTABLE_PATH-$ARCH")
done

echo "Merging extracted architectures: ${ARCHS}"
lipo -o "$FRAMEWORK_EXECUTABLE_PATH-merged" -create "${EXTRACTED_ARCHS[@]}"
rm "${EXTRACTED_ARCHS[@]}"

echo "Replacing original executable with thinned version"
rm "$FRAMEWORK_EXECUTABLE_PATH"
mv "$FRAMEWORK_EXECUTABLE_PATH-merged" "$FRAMEWORK_EXECUTABLE_PATH"

done
```

## 三、设置技巧

### 3.1、快速设置的技巧

![](https://image-1258017831.cos.ap-guangzhou.myqcloud.com/20180828232205.png)

1. 项目主目录找到 `XXX.xcodeproj` 右键显示包内容
2. 找到 `project.pbxproj` 使用 Sublime 打开
3. 搜索自定义的名字：`CH__Carthage-Copy-Frameworks`
4. 可以批量设置，
5. 更高级的做法，使用命令行打开文件，进行设置：`open -a Sublime\ text /Users/wanggw/Desktop/Proj-AiMei/am-1-user/Amy.xcodeproj/project.pbxproj`

open -a Sublime\ text /Users/wanggw/Desktop/Proj-ATax/ATax/ATax.xcodeproj/project.pbxproj


### 3.2、Input Files

* $(SRCROOT)/Carthage/Build/iOS/SnapKit.framework
* $(SRCROOT)/Carthage/Build/iOS/ObjectMapper.framework
* $(SRCROOT)/Carthage/Build/iOS/Kingfisher.framework
* $(SRCROOT)/Carthage/Build/iOS/ESPullToRefresh.framework

### 3.3、Output Files

* $(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/SnapKit.framework
* $(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/ObjectMapper.framework
* $(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/Kingfisher.framework
* $(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/ESPullToRefresh.framework



