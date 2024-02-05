---
title: "tailwindcss中iconify的使用"
description: "iconify的使用"
pubDate: "2024-02-04  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-02-04-iconifycss/01.png"
tags:
    - iconify
    - Vue3 使用 iconify
    - 前端进阶
---

## 起因

最近正在业余时间编写 Vue 的组件库, 设计完按钮组件后正准备设计 Icon 组件，看大佬 antfu 巨佬的支持过的 iconify 组件库，发现 iconify 的使用方法和我之前使用的 iconfont、font-awesome 等图标库的使用方法完全一致，于是决定使用 iconify 来替换 iconfont、font-awesome 等图标库。

## iconify 的介绍

iconify 是基于 SVG 的图标库，可以使用 iconify 来替换 iconfont、font-awesome 等图标库。拥有市面上所有的流行图标库。

## 个人使用场景

`tailwindcss` 和 `vue3`

## 使用

安装

```bash
pnpm add @iconify-json/mdi-light --D
```

安装 tailwind 插件

```bash
pnpm add @iconify/tailwind -D
```

tailwindcss 中使用

```cjs
import { addDynamicIconSelectors } from '@iconify/tailwind'

{
    "plugins": [
        addDynamicIconSelectors()
    ]
}
```

代码中使用

```jsx

 <span class="icon-[mdi-light--home]" />

```


成功演示 

![切图2](http://img.blog.loli.wang/2024-02-04-iconifycss/02.png)


### 如果你不喜欢 tailwindcss 的插件，也可以使用原生的代码或者vue代码使用

```jsx
// vue代码
import { Icon } from '@iconify/vue'

<Icon icon="mdi-light:home" />
```


## 相关资料


  [iconify 官方文档](https://iconify.design/)
  [tailwindcss 如何使用 入口文档](https://github.com/iconify/iconify/tree/main/plugins/tailwind)