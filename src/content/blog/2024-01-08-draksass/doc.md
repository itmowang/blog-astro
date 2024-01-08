---
title: "dart-sass 和 node-sass 的区别以及使用"
description: "dart-sass 和 node-sass 的区别以及使用"
pubDate: "2024-01-08  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-01-08-draksass/02.png"
tags:
    - dart-sass
    - node-sass
    - 区别
---

### 序

在我们开发场景中，如果在`node`环境中使用`node-sass`，经常会有`python`版本安装问题，也有和`node版本`是否和`node-sass`版本有关联关系，还强制安装NET Framework版本，总而言之会出现各种问题，尤其是老项目居多...


![切图1](http://img.blog.loli.wang/2024-01-08-draksass/01.png)

### 什么是Dart Sass
 
`Dart Sass` 是官方力推的 `sass` 继任者。官网主推项目，用来替代`node-sass`，由`dart`开发，对css新特性支持的更加全面，最大的好处是没有`node版本之间的依赖关系`。


### node-sass 和 dart-sass的区别

 - node-sass
        node-sass 是顺应前端工程化而出现的node包，是使用c++实现的libSass的封装，因为使用c++编译，所以速度比较快，前期支撑住了前端工程化的潮流。前端工程化项目的大功臣，遗留缺点有很多，比如硬性要求对应node版本之类的奇怪的错误
 - dart-sass
        dart-sass 是基于dart开发的，他的速度更快， 更易于安装，并且可以编译成纯JavaScript，并且对css新特性获得了更好的支持



### 总结

    后面使用预处理器，直接使用dart-sass啦。毕竟要适应新的时代


