---
title: "Tailwind + Antd Css冲突解决方案(按钮颜色透明)"
description: "Tailwind + Antd Css冲突解决方案(按钮颜色透明)"
pubDate: "2023-12-14　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-12-14-tailwindButtionOpe/01.png"
tags:
    - Antd
    - Antd tailwind 颜色冲突
    - 学习折腾
---

## 问题引发

公司开展新项目，准备使用React，用React的主流框架肯定是Antd啦，为了防止公司样式污染以及结合了一些老项目的痛点，决心使用Tailwind来弥补这些问题，然后引发了按钮没有颜色的Bug 在原有Css中 Tailwind的优先级比Antd要高所以引发了这个问题

![切图1](http://img.blog.loli.wang/2023-12-14-tailwindButtionOpe/02.png)


## 解决方案

1. tailwind.config.js 配置文件修改 
 
将 preflight: false 修改为 false

``` jsx
  /** @type {import('tailwindcss').Config} */
export default {
  content: ['./src/**/*.{js,jsx,ts,tsx}'],
  theme: {
    extend: { 
    }
  }
  // plugins: [],
  // corePlugins: {
  //   preflight: false
  // }
}
```

2. 修改 tailwind @layer样式


``` jsx
@tailwind base;
@tailwind components;
@tailwind utilities;


/* @layer base { 
  button, [type='button'], [type='reset'], [type='submit']
  { background-color: #3b82f6; 
  }
} */
```


3. 全局修改 antd 全局样式

将自己的全局Css样式中处理这个这个引入

``` jsx
// global.css
:global(.ant-btn-primary) {
  background-color: #1677ff !important;
}
// 或者
.ant-btn-primary{
     background-color: #1677ff !important;
}
```
