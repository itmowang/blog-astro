---
title: "React之路 - 第二篇 "
description: "React之路 - 知识累计篇"
pubDate: "Jul 02 2023"
heroImage: "http://img.blog.loli.wang/2023-8-24-ReactExperience/01.png"
tags:
    - React
    - 学习折腾
    - React之路 - 第二篇
---


也算是用React写过几个项目了，不管是实际业务上面感觉都有一定的把握。特此准备写一个脚手架项目模板。

## 项目准备
```bash
建立 react-admin 文件夹

pnpm init 

# 安装依赖 
pnpm add typescript
pnpm add vite 
pnpm add react 
pnpm add react-router-dom
pnpm add @vitejs/plugin-react-swc

# 生成ts配置文件 
tsc --init
```

创建 **vite.config.ts** 文件

``` bash

import { defineConfig, PluginOption } from "vite";
import react from "@vitejs/plugin-react-swc";

export default defineConfig({
  resolve: {
    alias: {
      "@": "/src",
    },
  },
  plugins: [react()] as PluginOption[],
  server: {
    port: 8081,
  },
  preview: {
    port: 3000,
  },
});

```

根目录创建 index.html

``` bash

```



