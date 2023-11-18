---
title: "rust的编程概念"
description: "rust的编程概念"
pubDate: "2023-11-8　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-6-rust001/01.png"
tags:
    - rust
    - rust 编程
    - 学习折腾
---

## 变量

声明变量

```rs
// 普通变量
let x = 5;  // 无法修改 类似常量

let mut x = 5; // 增加mut 变为可修改

```

数据类型

长度 有符号类型 无符号类型
8 位 i8 u8
16 位 i16 u16
32 位 i32 u32
64 位 i64 u64
128 位 i128 u128
arch isize usize

```rs
// 整型
let guess=22222;
// 浮点型
let x: f64 = 2.0;
// 布尔型
let t = true;
// 字符串类型
let c = 'z';
// 元组类型
let tup = (500, 6.4, 1);
let (x, y, z) = tup;
// 数组类型
let a = [1, 2, 3, 4, 5];

```

函数

```rs
// 函数
fn another_function() {
    println!("Another function.");
}
// 带参函数
fn another_function(x: i32) {
    println!("The value of x is: {}", x);
}
// 带返回值的函数
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {}", x);
}

fn plus_one(x: i32) -> i32 {
    x + 1
    //  也可以  return x+1

}


```

循环

```rs
// 循环
loop {
        println!("again!");
}
// 条件循环
let mut number = 3
while number != 0 {
    println!("{}!", number); 
    number -= 1;
}
// for 循环
let a = [10, 20, 30, 40, 50];

for element in a {
    println!("the value is: {}", element);
}

```

