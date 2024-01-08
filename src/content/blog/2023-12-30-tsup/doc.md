---
title: "简单使用 tsup 进行打包"
description: "简单使用 tsup 进行打包"
pubDate: "2023-12-30  23:27:24"
heroImage: "http://img.blog.loli.wang/2023-12-30-tsup/01.png"
tags:
    - tsup
    - 打包工具
    - 组件库
---

### 起因。

最近在编写自己的组件库，使用`monorepo`模式进行开发,`monorepo`开发将utils单独作为工具库，原本打算使用tsc编译出去的，无意中发现了打包工具。

### 介绍

tsup 是一个基于 ESBuild 实现在零配置的情况下快速打包 Typescript 模块的库，支持 .ts、.tsx的转换。它基于esbuild，但是同时也选择融合其他的构建工具共同参与，弥补了esbuild的不足。


### 安装使用
``` bash
# pnpm 安装 同样也可以npm yarn 等
pnpm add tsup -D

```

packages.json 文件中声明

```json
{
    "build":"tsup"
}
```

简单使用可以在命令后面加输出路径等 也可以添加配置文件去使用

```json
{
    "build":"tsup src/index.ts src/cli.ts"
}
```

也可以使用配置文件，根目录下面新建一个 `tsup.config.ts` 文件

```jsx

import { defineConfig } from 'tsup'

export default defineConfig({
  entry: ['./src/index.ts'], // 打包入口
  splitting: false,
  sourcemap: true,
  clean: true,
})

```

```json
"scripts": {
    "build": "tsup --format esm,cjs,iife --config tsup.config.ts"
},
```

这里也可以定义打包目录之类的，详情查看官网。配置信息比较完全
https://tsup.egoist.dev/#what-can-it-bundle







