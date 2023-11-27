---
title: "Node版本管理Volta的使用"
description: "Node版本管理Volta的使用"
pubDate: "2023-11-27　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-27-volatSetup/01.png"
tags:
    - Node版本管理
    - Volta的使用
    - 学习折腾
---

## 为什么要有Volta

一个项目组有多个前端现象，使用的Node版本都不一样，并且有前端工程师一个人管理多个不同node版本的前端项目需要频繁的切换Node版本


## 使用 Volta

    官网：https://volta.sh/

``` bash
# 安装volta 
curl https://get.volta.sh | bash

# 安装node
volta install node

# 指定node版本安装
volta install node@14.15.5

```

在前端项目中配置进行自动切换

``` jsx
// package.json

"volta": {
  "node": "12.20.2",
  "yarn": "1.19.2"
}

```

通过volta 安装好指定的node版本后可以做到打开当前的项目的命令行，自动切换node版本

![切图1](http://img.blog.loli.wang/2023-11-27-volatSetup/02.png)

![切图2](http://img.blog.loli.wang/2023-11-27-volatSetup/03.png)
