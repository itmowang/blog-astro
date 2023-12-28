---
title: "现代化 CSS 框架"
description: "新生代 CSS 框架"
pubDate: "2023-12-27  23:27:24"
heroImage: "http://img.blog.loli.wang/2023-12-27-newcss/01.png"
tags:
    - CSS
    - tailwindcss
    - unocss
---

### 什么是原子化 css

原子 CSS 是一种 CSS 架构方法，它有利于小型、单一用途的类，其名称基于视觉功能。

原子化 CSS 是一种 CSS 的架构方式，它倾向于小巧且用途单一的 class，并且会以视觉效果进行命名。

例如 `.mt-10` 代表 `margin-top: 10px`，`.bg-red` 代表 `background-color: red`。

```css
.mt-10 {
  margin-top: 10px;
}
.bg-red {
  background-color: red;
}
```

### 为什么要使用原子化 css

原子化 CSS 有助于减少 CSS 的大小，因为它只使用了少量的 class，而不是大量的 class 和大量的 style 引入。优化了 CSS 的大小，也就优化了 CSS 的加载速度。

### 常用的 css 框架选择

- [Tailwind CSS](https://tailwindcss.com/)
- [UnoCSS](https://unocss.dev/)
- [Tachyons](https://tachyons.io/)
  ....

### 参考

- [重新构想原子化 CSS-antfu] https://antfu.me/posts/reimagine-atomic-css-zh
