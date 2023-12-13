---
title: "ViteSSG 搭建博客 01 (ssg项目项目搭建)"
description: "ViteSSG 搭建博客 01 (ssg项目项目搭建)"
pubDate: "2023-12-05　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-12-13-ssgblog01/01.png"
tags:
    - ViteSSG
    - ssg项目项目搭建
    - ViteSSG 搭建博客 01 (ssg项目项目搭建)
---



### 项目准备

``` bash 
# 强烈建议使用 pnpm
npm i -g pnpm 

# 安装主要项目依赖
pnpm add vue typescript less vue-router

pnpm add @unhead/vue @vitejs/plugin-vue vite vite-plugin-pages vite-ssg -D
```


### 开始

Node 版本需要高于 14 以上

示例以多页应用为例

``` jsx
// package.json
{
    "script":{
        "dev":"vite",
        "build":"vite-ssg build"
    }
}

```

``` jsx
// main.ts
import { ViteSSG } from "vite-ssg";
import App from "./App.vue";
import routes from "~pages";

export const createApp = ViteSSG(
  App,
  { routes },
  ({ app, router, routes, isClient, initialState }) => {}
);

```

``` jsx
// vite.config.ts
import { defineConfig } from "vite";
import vue from "@vitejs/plugin-vue";
import Pages from "vite-plugin-pages";

export default defineConfig({
  plugins: [vue(), Pages({ extensions: ["vue", "md"] })],
  ssgOptions: {
    script: "async",
    formatting: "prettify",
  },
});
```

编写页面,在 pages 目录下新建文件夹 index 然后建立目录 index.vue

``` jsx
// src/pages/index/index.vue
<template>
  <div class="Index">
    <div>Index</div>
    <div>{{ index }}</div>
    <div>{{ index2 }}</div>
  </div>
</template>
<script lang="tsx" setup>
import { ref } from "vue";

const index = ref("idx");
const index2 = ref("Leo");
</script>


```

最后执行 `pnpm build` 即可生成静态构建的文件

![切图2](http://img.blog.loli.wang/2023-12-13-ssgblog01/01.png)
