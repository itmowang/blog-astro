---
title: "给表妹的 Astro Blog 搭建流程"
description: "给表妹的 Astro Blog 搭建流程"
pubDate: "2023-11-6　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-6-astrosetup/01.png"
tags:
    - Astro 
    - Blog搭建 
    - 学习折腾
---

表妹上大学了，理工类的学科，看来以后绝对优秀人才呢。因此需要一个blog来记录学习过程。

### 为什么使用 Astro 

当然和我是前端工程师是分不开的关系，本来也是推荐使用一些PHP的blog程序，但是需要一些服务器相关的知识，也并非省时省力。顺带还需要给她传授一点 Git 相关的知识，所以对于正在使用astro 的我当然首选 **Astro** 啦 , 也可以讲下web相关的知识。

### 在此之前

安装好nodejs:

https://nodejs.org/en

熟悉md的编写:

https://www.math.pku.edu.cn/teachers/lidf/docs/Rbook/html/_Rbook/markdown.html

### 在 github 克隆一个 astro 项目 

``` bash

# 首推自己的个人github项目

https://github.com/itmowang/sxq-astro
```

![切图1](http://img.blog.loli.wang/2023-11-6-astrosetup/01.png)

github推出的新功能 **repository templates**  方便快速使用该代码库。使用后会在自己的本地仓库看到该项目


### 编写文章

克隆到自己的私人仓库后 通过 git 工具拉取自己仓库的代码代码。

「文章」存放于`src/content/blog`路径内，可自行清空后新建；


![切图2](http://img.blog.loli.wang/2023-11-6-astrosetup/02.png)


文章内固定格式

``` jsx
---
title: "文章标题"   # 文章标题
pubDate: 2021-03-27 09:45:11  # 发布日期
description: "文章描述。"  # 文章描述
heroImage: "http://img.blog.loli.wang/2023-8-21-cfworkerProxy/01.png" # 主页预览图
---
    # mdx
    文章内容
```


### 发布
``` bash
 # 通过npm发布至线上
 # 强烈要求 Node 版本在 18x + 
    npm i -g pnpm

    pnpm install
    
    pnpm build

    然后将docs目录内的文件部署到服务器上，同样的也可以直接使用 github 的 pages 根据自己的喜好来。

```

