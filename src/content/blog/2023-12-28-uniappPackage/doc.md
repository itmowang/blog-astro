---
title: "UNI-APP 离线打包配置"
description: "UNI-APP 离线打包配置"
pubDate: "2023-12-28　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-12-28-uniappPackage/01.jpg"
tags:
    - uniapp
    - 离线打包
    - SDK
---

### 起因

公司有2款不同的PDA设备`霍尼韦尔`，`SUNMI` 这2款pda设备，在有一次项目升级后，发现`SUNMI`这种设备型号的PDA设备热更新失败，准确的说不是热更新是失败 是热更新下来的APK 安装时无法兼容

如图

![切图1](http://img.blog.loli.wang/2023-12-28-uniappPackage/01.jpg)
 
### 引发原因

项目一直是用的离线打包，`Hbuilder X` 这款开发工具，之前使用云打包的时候会自动调用本地的离线打包，可是有次开发工具更新后，云打包不触发离线打包了。本来并不在意这件事情，毕竟就是打包个安卓包而已，并不在意，打完包就发布了。。

后续就出现问题了，`霍尼韦尔`设备正常，`SUNMI`设备异常，前者设备安卓版本9.0, 后者安卓设备版本7.0，版本不兼容了。低版本的无法安装。

本地模拟器同样的也是这个问题，低版本的无法安装，安装上也是白屏。

经过排查，使用离线打包的就没有问题。

### 如何配置离线打包

开始准备
- [安装 jdk 8](https://www.java.com/zh-CN/download/)
- [安装 Android Studio](https://developer.android.google.cn/studio?hl=zh-cn)
- [下载 UNIAPP 离线 SDK](https://nativesupport.dcloud.net.cn/AppDocs/download/android.html) (注意，下载的SDK版本必须和HubilderX版本对应上)
- [UNIAPP 开发者中心账号](https://dev.dcloud.net.cn/pages/app/list) (注意，提前实名认证啥破玩意都整完)



#### 获取配置信息

在UNIAPP项目中有个 `mainifest.json` 文件 ，里面会看到一些基础配置信息，其中有个` UNIAPP 引用标识 `, 这个也同样是APPID, 也关系到开发中心对应的项目编号。


![切图2](http://img.blog.loli.wang/2023-12-28-uniappPackage/02.png)


#### 生成本地打包资源

生成本地打包资源备用 后续放置到 Android Studio 内使用

![切图3](http://img.blog.loli.wang/2023-12-28-uniappPackage/03.png)

![切图4](http://img.blog.loli.wang/2023-12-28-uniappPackage/04.png)

#### 将本地资源文件夹移动至离线SDK中

将本地资源包复制到该目录下

HBuilder-Integrate-AS\simpleDemo\src\main\assets\apps

![切图4](http://img.blog.loli.wang/2023-12-28-uniappPackage/05.png)

#### Android Studio 导入SDK的示例项目

![切图4](http://img.blog.loli.wang/2023-12-28-uniappPackage/06.png)


#### 修改dcloud_control.xml 中的 appid

在新打开的编辑器中 , 找到 simpleDemo/src/main/assets/data/dcloud_control.xml

进行修改

![切图7](http://img.blog.loli.wang/2023-12-28-uniappPackage/07.png)

修改为之前 `mainifest.json` 定义的APPID，还有当前准备发布的 `版本号`

#### 生成安卓签名

安卓打正式包必须要的，参考官方文档 

https://ask.dcloud.net.cn/article/35777

#### 前往开发者中心生成AppKey 

在我们使用 HbuilderX 后获取Appid后，登录账号,会在后台系统生成相应的应用，进入UNIAPP的开发者中心,选择相应的应用，获取离线的APPKEY

![切图8](http://img.blog.loli.wang/2023-12-28-uniappPackage/08.png)

![切图9](http://img.blog.loli.wang/2023-12-28-uniappPackage/09.png)


#### 修改包名 配置appKey

在 AndroidManifest.xml 中修改包名，在`开发者中心`可以看到相关的包名，一般都是uni.xxx 开头的

![切图10](http://img.blog.loli.wang/2023-12-28-uniappPackage/10.png)

在下方找到

``` xml
 <meta-data
            android:name="dcloud_appkey"
            android:value="239898****************b2d9dbcbf2bc" />
```

android:value 修改成自己的离线 appKey 即可


#### 修改原有的默认APP图标还有打包出来的应用名

修改应用名 /simpleDemo/src/main/res/values/strings.xml

```xml
<resources>
    <string name="app_name">修改自己的应用名</string>
</resources>

```

icon 启动图替换 /simpleDemo/src/main/res/drawable 中的 icon.png push.png splash.png 图片进行替换就好

![切图10](http://img.blog.loli.wang/2023-12-28-uniappPackage/11.png)

### 最后尝试构建 

![切图12](http://img.blog.loli.wang/2023-12-28-uniappPackage/12.png)
![切图13](http://img.blog.loli.wang/2023-12-28-uniappPackage/13.png)
![切图14](http://img.blog.loli.wang/2023-12-28-uniappPackage/14.png)
![切图15](http://img.blog.loli.wang/2023-12-28-uniappPackage/15.png)
![切图16](http://img.blog.loli.wang/2023-12-28-uniappPackage/16.png)


    完成 ，，，总而言之，写UNIAPP的坑很多，如果不是赶时间的话，建议去使用Flutter 等框架，（--）