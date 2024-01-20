---
title: "TS 中的常用类型 (经常需要使用的)"
description: "TS 中的常用类型 (经常需要使用的)"
pubDate: "2024-01-20  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-01-18-tspickomit/bg.png"
tags:
    - TS 中的常用类型
    - Typescript
    - 前端进阶
---

### 前言

本篇介绍的是 Typescript 中经常使用的一些类型,这些类型一般都是做一个项目中经常需要用上的.

### Required<Type>

将类型`非必填`改为`必填`

```tsx
interface Todo {
    username?: string;
    age?: number;
    address?: string;
}

// 正常使用情况
const todo: Todo = {};

// 整个类型都必须填写
const todoa: Required<Todo> = {};

// 配合Pick(选取) 选取单个属性必须填写
const todob: Required<Pick<Todo, "username">> = {};
```

![切图1](http://img.blog.loli.wang/2024-01-20-typescriptUitls/01.png)

### Readonly<Type>

将类型改为`只读`,类型中所有属性都无法被重新分配

```tsx
interface Todo {
    title: string;
}
// todo 改为了只读属性
const todo: Readonly<Todo> = {
    title: "魔王Blog - 一个前端程序员的个人博客",
};

// 如果重新分配将会报错
todo.title = "魔王Blog - 一个前端程序员的个人博客";
```

![切图2](http://img.blog.loli.wang/2024-01-20-typescriptUitls/02.png)

### Record<Keys, Type>

构建一个`对象类型` ,属性键名为`Keys`,属性值为`Type`

```tsx
// 简单实用 对象结构为 key value 并且类型都为string
const value: Record<string, string> = {
    name: "魔王",
    age: "18",
    address: "地狱",
};

interface Info {
    name: string;
    age: number;
    address: string;
}

type CityName = "北京" | "上海" | "广州" | "深圳";

// 复杂实用 对象结构为 key value 并且类型都为Info 且key只能为CityName
const info: Record<CityName, Info> = {
    北京: {
        name: "魔王",
        age: 18,
        address: "地狱",
    },
    上海: {
        name: "魔王",
        age: 18,
        address: "地狱",
    },
    广州: {
        name: "魔王",
        age: 18,
        address: "地狱",
    },
    深圳: {
        name: "魔王",
        age: 18,
        address: "地狱",
    },
};
```

![切图3](http://img.blog.loli.wang/2024-01-20-typescriptUitls/03.png)

### Pick(选取,选择) 看上一篇文章

https://blog.loli.wang/blog/2024-01-18-tspickomit/doc/index.html

### Omit(排除) 上一篇文章

https://blog.loli.wang/blog/2024-01-18-tspickomit/doc/index.html

### Exclude<UnionType, ExcludedMembers> (排除联合类型中指定类型)

Exclude 是一个工具类型,用于`排除` `联合类型`指定的类型,得到新的类型

```tsx
// 原始联合类型
type CityName = "北京" | "上海" | "广州" | "深圳";

// 通过Exclude排除类型 '北京' | '上海'  得到新的联合类型
type City = Exclude<CityName, "北京" | "上海">;

// 如果实用原有的联合类型已排除过的 会报错
const city: City = "北京";

// 如果使用未排除的联合类型 会正常
const cityName: CityName = "北京";
```

![切图4](http://img.blog.loli.wang/2024-01-20-typescriptUitls/04.png)

如果联合类型比较复杂 是对象类型的,也同样

```tsx
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; x: number }
  | { kind: "triangle"; x: number; y: number };
 
type T3 = Exclude<Shape, { kind: "circle" }>
```

### ReturnType<Type>

构造一个由 `function` 的返回的数据组成的`类型`, 用来指定函数返回的数据类型为什么格式

```tsx
// 指定返回值类型为 string
type Fun = ReturnType<() => string>

// 正常写法
function fn(): Fun {
  return "123"
}

// 错误写法
function fn2(): Fun {
  return 123
}

// 指定返回值类型为对象
type Fun2 = ReturnType<()=>{
  name:string,
  age:number
}>

// 正常写法
function fn3(): Fun2 {
  return {
    name:"123",
    age:123
  }
}


```


![切图5](http://img.blog.loli.wang/2024-01-20-typescriptUitls/05.png)


### 字符串操作类型

#### Uppercase<StringType> 

用于将字符串类型的所有字符转换为大写。

```tsx
type UppercaseString = Uppercase<'hello'>; // 类型为 'HELLO'
```

#### Lowercase<StringType>
用于将字符串类型的所有字符转换为小写。


```tsx
type LowercaseString = Lowercase<'WORLD'>; // 类型为 'world'
```


#### Capitalize<StringType>

用于将字符串类型的首字母转换为大写。

```tsx
type CapitalizedString = Capitalize<'typescript'>; // 类型为 'Typescript'
```

#### Uncapitalize<StringType>

用于将字符串类型的首字母转换为小写。

```tsx
type UncapitalizedString = Uncapitalize<'JavaScript'>; // 类型为 'javaScript'

```


#### 相关参考文档



### 相关文档

[typescriptlang](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)