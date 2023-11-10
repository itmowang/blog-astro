---
title: "dependencies 和 devDependencies 的区别(回忆录1)"
description: "dependencies 和devDependencies 的区别"
pubDate: "2023-11-11　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-11-dependenciesAnddevDependencies/01.png"
tags:
    - dependencies
    - devDependencies
    - 学习折腾
---

## 回忆录1: 一次给别人解决BUG引发的问题

事情是这样的，一个小伙伴问我一个问题。项目写了个插件，导出到NPM中了，但是通过npm install 下来无法使用，仔细检查，发现依赖都是装载在 **devDependencies** 中

###  理解

区别:

    dependencies 用于生产环境
    devDependencies 用于开发环境，打包成npm插件后无法获取内容

拓展:

npm install xxx -g 表示全局安装，通常用于安装脚手架 yarn pnpm webpack 等工具

npm install xxx –save(-S) 表示本地安装，会被加至dependencies部分

npm install xxx –save-dev(-D) 表示本地安装，会被加至
devDependencies部分


npm install会默认下载dependencies和devDependencies中的所有依赖包

1.如webpack、html-webpack-plugin等工具包就安装在devDependencies开发环境下，

项目部署到开发环境所必须的依赖包则安装在dependencies生产环境下。
在项目编译时dependencies、devDependencies里的依赖其实没有影响，最重要的区别体现在:

npm包发布的时候，其他的开发者可以从你发布的npm包中下载dependencies里的依赖包，而不能下载devDependencies里的内容。

