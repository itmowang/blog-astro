---
title: "原型链的理解"
description: "原型链的理解"
pubDate: "2023-9-23　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-9-23-prototype/01.png"
tags:
    - 原型链 
    - 学习折腾
    - prototype
---

## 起因
  程序媛妹妹问我面试题，怎么好好的解释原型链(或许她问的什么是原型链)，嘛！毕竟写vue都要理解这玩意捏。

## 理解
  每一个对象都有自己的原型链，有自己的内置对象，有自己的prototype 和 proto 。

  **prototype** 显式原型，指向一个构造函数
  ** __proto__ ** 隐式原型，是对象的属性

  如果想从对象中查找某个值，如果没有找到他们就会从原型实例，向上查找，直到找到Object.prototype 为止。

  示例解释
  
``` jsx

 Object.prototype.abc = 222;

 // 建立构造函数1
 function Test1Fun() {}

 // 构造函数中写入原型
 Test1Fun.prototype.test = "111";

 // 建立构造函数2
 function Test2Fun() {}
  
 // 将Test2Fun的原型对象指向一个Test1Fun的实例，实现原型链继承
 Test2Fun.prototype = new Test1Fun();

// 创建一个Test2Fun的实例对象testObj
 var testObj = new Test2Fun();

//  从原型链中查找 test 
 console.log(testObj.test);
//  从原型链中查找 abc
 console.log(testObj.abc);

```

是否发现vue中 Vue是一个构造函数，我们经常在上面挂载原型，在所有地方都能方便使用

![切图1](http://img.blog.loli.wang/2023-9-23-prototype/01.png)
