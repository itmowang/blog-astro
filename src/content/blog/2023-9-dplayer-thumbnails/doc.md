---
title: "问答：DPlayer关键帧预览图生成思路 "
description: "问答：DPlayer关键帧预览图生成思路"
pubDate: "2023-9-26　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-9-dplayer-thumbnails/01.png"
tags:
    - DPlayer 
    - 学习折腾
    - 关键帧预览
---

## 起因
  网友学习java工作了，公司领导给了个需求，要播放视频同事鼠标悬停到进度条位置有预览效果

  类似
  ![切图1](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/01.png)

  网友深思熟虑的考虑播放器使用 **DPlayer** ，但是把官网上的Demo复制下来，放上自己的视频后，发现预览图都是白屏。

![切图2](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/02.png)

我看了下 **DPlayer** 文档后，发现是有个属性 **thumbnails** 专门存放时间帧的预览图。给出的建议是自己去通过视频工具去切时间帧的图片。

### 重新理解需求

发现他的需求并没有描述清楚，常常因为需求没有描述清楚而导致做一些多余的事情

![切图3](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/03.png)

嗯.... 他是java工程师，在工作中前端的活也要干。。但是居然想着前端切图，，，前端一个弱语言单线程，就算依赖Web Workers 也很不好吧。应用层并不适合处理视频这种场景。

### 进一步建议和最后的方案

看见 **DPlayer** 作者有个库**DPlayer-thumbnails**，专门处理视频预览图片的，是基于"fluent-ffmpeg"这个库来写的，可惜是Node的，他是java不太适用。但是ffmpeg 连 Node都有相关的库，java这么好的生态会没有? 毕竟不是java 慢慢引导下吧。

![切图4](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/04.png)
![切图5](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/05.png)
![切图6](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/06.png)
![切图7](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/07.png)
![切图8](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/08.png)

最终结束。。。虽然没帮到什么实际上的，至少思路给引导了下。我想应该足够了


### 后续

后一天问了下网友情况，如何生成 ，他打算的方案是循环生成图片再去拼接，我看官方写的插件Node版本的也是这样的，后来发现他的能力并不能做到相关的操作

``` bash
ffmpeg -y -i "test.mp4" -frames 1 -vf "thumbnail=n=100,scale=-1:320,tile=4X6:padding=10:color=white" thumbnail.png
```

![切图9](http://img.blog.loli.wang/2023-9-dplayer-thumbnails/09.png)