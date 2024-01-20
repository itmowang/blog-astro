---
title: "TS 中的 Pick 和 Omit"
description: "TS 中的 Pick 和 Omit"
pubDate: "2024-01-18  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-01-18-tspickomit/bg.png"
tags:
    - Pick
    - Omit
    - Typescript
    - 前端进阶
---

### Pick （选取）

官方介绍 : `通过从 interface 中选取属性集 Keys  来构造类型指定的Type。`

示例

```tsx
// 原接口
interface Todo {
  title: string,
  description: string,
  date: string
}

// 构建的新接口 只选取目标接口中的title 和 date
type TodoNewPreView = Pick<Todo, "title" | "date">

const Todo: TodoNewPreView = {
  title: "魔王のBlog",
  date: "2023-01-01",
}

```

证明我们从 Todo 这个接口中选取了 `title` 和 `date` 这两个属性,形成了新的类型接口

![切图1](http://img.blog.loli.wang/2024-01-18-tspickomit/01.png)
![切图2](http://img.blog.loli.wang/2024-01-18-tspickomit/02.png)



### Omit （排除,省略）

`Omit` 和 `Pick` 是相反的,是这个接口中使用的过程中,有不想使用的参数,可以进行屏蔽掉

![切图3](http://img.blog.loli.wang/2024-01-18-tspickomit/03.png)

可以看到,我们这里Todo这个类型接口,有个必须接收的`username`这个参数,如果我们需要用到这个类型,并且不想改变原有的使用类型的话,就需要使用Omit

![切图4](http://img.blog.loli.wang/2024-01-18-tspickomit/04.png)


总结,`Pick` 和 `Omit` 都是比较Ts中比较实用的工具,使用和利用好会给自己带来更大的收获



### 相关文档

[typescriptlang](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)