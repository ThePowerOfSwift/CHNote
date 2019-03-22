# Fastlane

## 一、安装

1. 先安装 Xcode 的 Command Line Tools：`xcode-select --install`
2. 安装 Fastlane：`sudo gem install fastlane` 
3. 更新 Fastlane：`sudo gem update fastlane`

## 二、使用

1. **cd 到项目目录**
2. 初始化 fastLane：`fastlane init`
3. 安装蒲公英插件：`fastlane add_plugin pgyer`
4. 安装版本设置插件：`fastlane add_plugin versioning`
5. 编辑 Fastfile 文件，编写 Fastlane Action
6. **cocoapods管理包的话：**需要在 `Gemfile` 文件中添加 `gem "cocoapods"`
7. 执行发布命令：

```
# Xcode clean 操作
xcodebuild clean -scheme XXX;
# 执行 fastlane 发布
bundle exec fastlane release_ipa_toPgyer
```


