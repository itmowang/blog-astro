---
title: "类型“ImportMeta”上不存在属性“glob” "
description: "类型“ImportMeta”上不存在属性“glob”"
pubDate: "2023-11-11　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-11-viteErrorGlob/01.png"
tags:
    - vite
    - vite 的错误
    - 学习折腾
---

## 类型“ImportMeta”上不存在属性“glob”

如果直接使用import.meta.glob，vscode会报类型ImportMeta上不存在属性“glob”的错误，需要在tsconfig文件下添加类型定义vite/client

``` jsx
{
  "compilerOptions": {
    "types": ["vite/client"]
  }
}
```
