---
title: "TS 中 keyof 和 typeof"
description: "TS 中 keyof 和 typeof"
pubDate: "2024-01-21  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-01-18-tspickomit/bg.png"
tags:
    - keyof
    - typeof
    - Typescript
    - 前端进阶
---

### keyof

`keyof` 是一个类型操作符, 用于获取一个类型所有的键值(属性名的)联合类型

```tsx
interface Todo {
  name:string,
  age:number,
  address:string
}

// 通过keyof 获取类型的key
type todoKeys = keyof Todo

// 获得类型的key
const todoKeys:todoKeys = 'name'

// todoKeys的类型为 'naem' | 'age' | 'address'

```



## typeof 

`typeof` 是一个是一个类型查询操作符,用于获取一个值,或者表达式,用于获取已有数据的数据类型

```tsx
const todo = {
  title: 'Todo',
  dataIndex: 'todo',
  key: 'todo',
}

// 等于复制了 todo 的类型
type TodoType = typeof todo

```


![切图1](http://img.blog.loli.wang/2024-01-20-typeofkeyof/01.png)