---
title: "什么是swc"
description: "什么是swc"
pubDate: "2023-9-10　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-9-13-why-swc/01.png"
tags:
    - 什么是swc
    - swc
    - 学习折腾
    - swc
---

## 什么是 swc

在swc没出现之前，一直是使用 **babel** 来处理转换旧版本 **JavaScript** 的工具，也可以给**typescript**使用，ast解析树，压缩等等.. 是前端工程换不可缺少的一环。

而 **Babel** 是JavaScript编写的，是JavaScript的编译器，SWC 同样也是JavaScript的编译器，不过是用Rust重写的，比Javascript快的多。性能得到了大幅度提升，目前很多常用的工具库都正在用rust重写。所以还不学Rust？


## swc 的使用
``` bash
# 命令

pnpm init

pnpm add @swc/core @swc/cli
```

``` bash
# async.js

const fetch = require("node-fetch");

async function getData() {
    let res = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    let json = await res.json();
    console.log('data', json);
}

getData();

```

### 配置spack

 在根目录创建 spack.config.js 文件 

 ``` bash
 const { config } = require("@swc/core/spack");


module.exports = config({
  // 入口
  entry: __dirname + "/index.js",
  // 输出到哪儿
  output: {
    path: __dirname + "/dist",
  },
  module:{}
  // swc编译配置
//   options: {
//     // 编译规则
//     jsc: {
//         parser: {}, // 解析配置
//         target: "es5", // 转义目标
//         // ... 等可以去官网看具体配置 https://swc.rs/docs/configuration/swcrc
//     },
//     // 输出文件配置
//     module: {
//       type: "commonjs",
//       strict: false,
//       strictMode: true,
//       lazy: false,
//       noInterop: false,
//       ignoreDynamic: false,
//     },
//   },
});

 ```



 ### 更改执行脚本

 ``` bash
 # package.json

  "scripts": {
    "build": "spack"
  }

 # 执行
 pnpm build

 ```

![切图2](http://img.blog.loli.wang/2023-9-13-why-swc/02.png)

![切图3](http://img.blog.loli.wang/2023-9-13-why-swc/03.png)


参考文档：

[SWC - 官方文档](https://swc.rs/docs/usage/bundling)
   

或许准备些一个自己的swc插件后面持续记录