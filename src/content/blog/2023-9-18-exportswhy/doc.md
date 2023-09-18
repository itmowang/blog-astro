---
title: "package.json 中 exports 的理解"
description: "package.json 中 exports 的理解"
pubDate: "2023-9-18　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-9-18-exportswhy/01.png"
tags:
    - package 
    - 学习折腾
    - exports
---


### 起因
  学习某低代码平台代码，看**packages**中有个exports，指向了不同的js文件，疑惑为什么这么做

### 解惑

  在通常情况下，我们会使用 main:"index.js" 指向单独指向一个所抛出的 **exports** 

  但是使用过 exports 后，会生成一个对应关系，抛出不同的模块，并消除替换了 **mian** 字段的默认行为 例如

``` jsx
 {
  "exports": {
    ".": "./main.js",
    "./core/test": "./test.js",
  }
}

// 使用时可以使用如此的对应关系 分模块去使用

// ".": "./main.js",
import test from 'package'

// "./core/test": "./test.js",
import test from 'package/core/test'

```

### 根据模块语法 引用不同的文件

``` jsx
"exports": {
    ".": {
      "import": "./lib/esm/index.mjs",
      "require": "./main.js"
    },
    "./core/test": "./test.js"
  }
```


### 后续疑问

exports 为抛出不同的模块,那么ts中的tsconfig 的paths 和 vite的  resolve.alias 区别是什么？