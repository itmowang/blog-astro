---
title: "vite 多页面应用配置"
description: "vite 多页面应用配置"
pubDate: "2023-9-22　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-9-22-multAppliction/01.png"
tags:
    - package 
    - 学习折腾
    - exports
---

## 起因
一个程序媛妹妹问我vite如何配置多应用，我仔细想了想，什么是多应用？？，后来经过gpt搜索，百度资料，哦~ 原来叫做 **多页面应用** ，然后这就去研究。

想打包出来的目录结构是这样的:

![切图1](http://img.blog.loli.wang/2023-9-22-multAppliction/01.png)


妹子是使用rollup配置的，看了下代码， 写的一个插件，导入到vite插件里面。看上去并不合理，也并不友善，同样的查看了vite文档 有相关的处理方案

## 自己动手

看文档，只需要根目录定义好相应的目录结构，在rollupOptions中配置好相应的入口，就可以成功

![切图2](http://img.blog.loli.wang/2023-9-22-multAppliction/03.png)

但是我们需要动态的读取目录，更好的读取应用, 所以需要使用fs去读取下文件夹内文件

``` jsx
import fs from "fs";

//...

  // 加载所有子目录
  const appliction = fs.readdirSync("./appliction");
  // 合并成input入口数组
  const input = Object.fromEntries(
    appliction.map((item) => [
      item,
      path.resolve(`${__dirname}/appliction/${item}/index.html`),
    ])
  );

//...

// 获取出来的目录结构
// {
//     app1:'xxx/xxx/appliction/app1/index.html'
// }


//...
  return {
    base: "./",
    outDir: "dist",
    plugins: [vue()],
    build: {
      target: "es2015",
      cssCodeSplit: true,
      assetsDir: "appliction",
      rollupOptions: {
        input: {
          main: path.resolve(__dirname, "index.html"),
          ...input,
        }, 
      },
  },
//...

```



这时候我们就打包出来了相应的目录，结构

![切图2](http://img.blog.loli.wang/2023-9-22-multAppliction/02.png)


不过有个缺点，目录结构都在assets内，想将打包出来的js文件css文件放到他们自己的文件结构内，例如

``` jsx

    - dist
        - page1
            - static
            - index.html    
        - page2
            - static
            - index.html 
    index.html

```

所以需要配置下rollup的输出格式

``` jsx

 return {
    base: "./",
    outDir: "dist",
    plugins: [vue()],
    build: {
      target: "es2015",
      cssCodeSplit: true,
      assetsDir: "appliction",
      rollupOptions: {
        input: {
          main: path.resolve(__dirname, "index.html"),
          ...input,
        },
        output: {
          entryFileNames: "appliction/[name]/static/[name].[hash].js",
          chunkFileNames: "appliction/[name]/static/[name].[hash].js",
          assetFileNames: "appliction/[name]/static/[name].[hash].[ext]",
        },
      },
    },


```

这样就打包出了我们所需要的目录结构

![切图3](http://img.blog.loli.wang/2023-9-22-multAppliction/01.png)


参考文档：
 [ 我的github仓库 ](https://github.com/itmowang/mw-cli/tree/master/packages/mw-create/template/multi-application-template)
    
[vite官方] (https://vitejs.dev/guide/build.html#multi-page-app)