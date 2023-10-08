---
title: "记一次折腾 Surge (github pages替代品) "
description: "记一次折腾 Surge (github pages替代品)"
pubDate: "2023-10-08　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-10-08-surge/04.png"
tags:
    - Surge 
    - 学习折腾
    - pages平替
---

## 起因
  
   ![切图1](http://img.blog.loli.wang/2023-10-08-surge/05.png)

   看到老师发这玩意，不管是什么，总得折腾一番 😁

## 如何使用 Surge.sh 免费部署静态网站

Surge.sh 是一个免费的静态网站主机，您可以通过命令行与之交互。它可以快速轻松地在线获取新站点和应用程序，无论是手动还是作为 CI 构建过程的一部分。以下是如何开始使用该服务。类似github 的pages功能

## 第一次运行
我们假设您已经有了要部署到 Web 的文件目录。如果还没有，请创建一个新文件夹，添加一个 index.html 和一些简单的入门内容。

Surge 是通过Npm发布的JavaScript的引用程序 ，在这之前必须安装Node.js ，再然后使用npm安装Surge

    npm install --global surge

安装完成后执行指令
``` bash

surge
```   
执行后会要求你注册/登录一个相关的账号，填写完后，会要求让你填写需要发布的目录，填写完成后自动发布

 ![切图2](http://img.blog.loli.wang/2023-10-08-surge/02.png)
 ![切图3](http://img.blog.loli.wang/2023-10-08-surge/03.png)


## 补充，如何绑定域名
只需要在需要发布的 Web 文件目录，建立一个CNAME文件，内部填写需要绑定的域名即可

 ![切图3](http://img.blog.loli.wang/2023-10-08-surge/07.png)


发布成功

 ![切图4](http://img.blog.loli.wang/2023-10-08-surge/06.png)