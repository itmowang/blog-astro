---
title: "rust开发环境安装以及Cargo"
description: "rust开发环境安装"
pubDate: "2023-11-6　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-6-rust001/01.png"
tags:
    - rust 
    - rust 环境搭建 
    - 学习折腾
---


## 我正在学习准备rust 

学习资源：

```
    官方文档 
    https://doc.rust-lang.org/book/
    第三方中文文档
    https://rustwiki.org/zh-CN/book/
```

## 安装

根据官网提供的exe 安装进行下一步就好

### hello world! 

建立一个 **project** 文件夹 创建文件 main.rs 文件

``` bash
# main.rs

fn main() {
    println!("Hello, world!");
}

```

保存文件 在命令行中输入命令

``` bash

rustc main.rs

# 会自动生成 main.exe main.pdb 文件 exe 是主要可执行文件 pdb是调试信息文件 方便调试

./main.exe

# Hello, world!

```


### Rust 是预编译语言

Rust 是一门预编译(ahead-of-time compiled)语言，这意味着你可以编译一个程序，将编译后的可执行文件给别人，即使他们没有安装 Rust 也可以运行程序。


### Cargo 

使用 Cargo 创建一个新项目

查看cargo的版本

```bash
cargo --version
# cargo 1.73.0 (9c4383fb5 2023-08-26)
```

创建项目

``` bash
cargo new hello_cargo
# Created binary (application) `hello_cargo` package
cd hello_cargo
```

目录结构

src 目录内有个 main.rs 作为主入口

Cargo.toml 为 Cargo的配置文件

``` bash
# Cargo.toml
[package]
name = "hello_cargo"
version = "0.1.0"
edition = "2021"

[dependencies]
```

### 构建并运行 Cargo 项目

``` bash
cargo build # 构建项目
cargo run # 一步构建并运行项目
cargo check # 检查项目是否可以编译通过
```


看来可以开始Rust之旅了