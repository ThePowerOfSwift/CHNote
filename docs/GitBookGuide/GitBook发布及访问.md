# GitBook发布及访问

这是我的[GitBook书籍](https://wanggw.gitbook.io/chnote)

## 一、发布前准备工作

### 1.1、上传 GitBook 到 GitHub 仓库

1. 在 GitHub 上新建一个仓库
2. 把本地创建 GitBook 上传到 GitHub 仓库

## 二、gitbook官网发布

[GitBook 简明教程](http://www.chengweiyang.cn/gitbook/basic-usage/README.html)这个教程是针对比较老的GitBook版本，其实对新版本的GitBook参考意义不大。

### 2.1、注意事项

1. [gitbook官网](https://www.gitbook.com)
2. 必须翻墙，可能因为节点不是美国的，还必须选择全局模式
3. 难道让我选择：https://love2.io

访问可能遇到的报错如下：

```
A network error has occurred. The service may be blocked by your ISP or in your area.
```

### 2.2、发布的大概流程：

1. 注册 GitBook 账号，或者使用 GitHub 账号直接登录
2. 创建 organization
3. 创建 space（也就是具体的某个 gitbook）
4. 把 space 关联(integration) 到 GitHub 某个仓库
5. 对 gitbook 进行定制，比如设置 logo

### 2.3、发布步骤：

1. 先创建 organization
2. 然后再在 organization 下创建一个 space
3. space 下点击更多，点击 integration 关联 GitHub 账号里面的仓库
4. 关于 GitBook 访问地址：
    1. 地址格式：https://{organization}.gitbook.io/{space} 
    2. 我的地址：https://wanggw.gitbook.io/chnote

### 2.4、GitBook更新：

* 只需要把本地的 GitBook 仓库最新的代码推送到 GitHub 仓库 GitBook 就会更新

### 2.5、参考：

* [如何在新版的gitbook上写自己的书](https://segmentfault.com/a/1190000015012209)
    * [书籍地址：](https://zhangzhen.gitbook.io/qmake-learn/)
    * [Gitbook GitHub地址](https://github.com/zhangzhen2618/Qt-learn)
    * gitbook 仓库需要包含的文件：`.gitbook.yaml` [参考](https://github.com/zhangzhen2618/Qt-learn/blob/master/.gitbook.yaml)
* [gitbook官方文档](https://docs.gitbook.com)

## 三、遗留事项及问题

### 3.1、遗留事项

1. 没有去给 gitbook 添加自定义样式

### 3.2、存在的问题

1. 目录紊乱了，没有按照 Summary 里面的顺序排版




