---
title: "Vue3 打包组件库出错 Cannot read properties of null (reading 'isCE')"
description: "Vue3 打包组件库出错 Cannot read properties of null (reading 'isCE')"
pubDate: "2024-01-24  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-01-24-vueComponentsErrorIsCe/01.png"
tags:
    - Vue3
    - Vue3 打包组件库出错
    - 前端进阶
---

写了套 React 的组件库后，觉着无法满足自己的需求，又删了重写了。。 从搭建 Monorepo，到编写组件测试的时候就发现了问题。

![切图1](http://img.blog.loli.wang/2024-01-24-vueComponentsErrorIsCe/01.png)

原因

造成这个问题是因为又 2 个不同的 vue 版本，因为我打包的组件库内有个 vue 的版本，而靶场用例上也有个 vue 版本，2 个 vue 版本产生冲突，导致这个错误

解决方案

组件库内部屏蔽 vue 导出,修改 vite.config.ts

```bash
# vite.config.ts

rollupOptions: {
    external: ['vue'],
    output: {
      globals: {
        vue: 'Vue',
      },
    },
 },

```


成功解决