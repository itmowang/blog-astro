---
title: "使用rust建立一个简单的web服务器"
description: "rust开发环境安装"
pubDate: "2023-11-7　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-6-rust001/01.png"
tags:
    - rust 
    - rust 环境搭建 
    - 学习折腾
---

## 

``` rs
// main.rs

use std::io::prelude::*;
use std::net::TcpListener;
use std::net::TcpStream;
use std::fs;

fn handle_client(mut stream: TcpStream) {
    let mut buffer = [0; 1024];
    stream.read(&mut buffer).unwrap();

    let response = "HTTP/1.1 200 OK\r\nContent-Type: text/html\r\n\r\n";
    let contents = fs::read_to_string("html/index.html").unwrap();
    let response = format!("{}{}", response, contents);

    stream.write(response.as_bytes()).unwrap();
    stream.flush().unwrap();
}

fn main() {
    let listener = TcpListener::bind("127.0.0.1:3030").unwrap();
    println!("Server is listening on port 3030");

    for stream in listener.incoming() {
        let stream = stream.unwrap();
        handle_client(stream);
    }
}


```


![切图1](http://img.blog.loli.wang/2023-11-07-rust002/001.png)