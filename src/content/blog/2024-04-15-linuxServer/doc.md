---
title: "记一次配置小主机装Ubuntu"
description: "记一次配置小主机装Ubuntu"
pubDate: "2024-04-15  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-04-15-linuxServer/17.jpg"
tags:
    - 小主机
    - 折腾
    - 折腾小主机
---

## 因为 Switch 送人了，而在 PC 上玩模拟不痛快，就想着整个小主机装个 ubuntu 然后装模拟器给电视机用

# **预算定为 500 块**

1. 选购小主机

    在选择小主机的时候，我观察了很多，如果买现成的 ，网上大部分 cpu 大部分都是 N100 的处理器，性能偏弱，价格也在 1000 块钱左右，并且硬盘很少，内存也就给 8g，并不能满足日常生活需要，所以考虑选择自己配，看了许多配置后，选定如下配置。

    1. CPU：酷睿 i5-8500T 散片 (淘宝:357 RMB)

    2. RAM：海力士 ddr4 3200mhz *2 (咸鱼: 160 RMB)

    3. 硬盘：金士顿 m2 500G SSD (咸鱼: 210 RMB)

    4. 主机: 准系统 DELL 戴尔 7060MFF (咸鱼:330 RMB)

    合计 : 1057 RMB

    以上配置，个人感觉还是能够接受的，虽然超预算了。。。

![切图01](http://img.blog.loli.wang/2024-04-15-linuxServer/01.jpg)
![切图02](http://img.blog.loli.wang/2024-04-15-linuxServer/02.png)


2. 装配小主机

准系统的小主机装配很简单，把内存 cpu 硬盘安装好，插上电源直接用就行。

![切图03](http://img.blog.loli.wang/2024-04-15-linuxServer/03.jpg)
![切图04](http://img.blog.loli.wang/2024-04-15-linuxServer/04.jpg)
![切图05](http://img.blog.loli.wang/2024-04-15-linuxServer/05.jpg)
![切图06](http://img.blog.loli.wang/2024-04-15-linuxServer/06.jpg)
![切图07](http://img.blog.loli.wang/2024-04-15-linuxServer/07.jpg)
![切图08](http://img.blog.loli.wang/2024-04-15-linuxServer/08.jpg)

3. 点亮小主机

顺利点亮小主机，二手收的硬盘里装有一个自带的windows 11，发现上一任硬盘装的各种资料。。

![切图09](http://img.blog.loli.wang/2024-04-15-linuxServer/09.jpg)
![切图10](http://img.blog.loli.wang/2024-04-15-linuxServer/10.jpg)
![切图11](http://img.blog.loli.wang/2024-04-15-linuxServer/11.jpg)
![切图12](http://img.blog.loli.wang/2024-04-15-linuxServer/12.jpg)
![切图13](http://img.blog.loli.wang/2024-04-15-linuxServer/13.jpg)


嗯。。。 虽然离谱。给他格式化吧。


4. 给小主机装ubuntu系统

小主机装配完毕了，是时候安装linux系统了，我自己的想法是先安装图形化界面的，后面再看着办，

原本的想法 

- **分配10G的硬盘，10G的硬盘里装ios镜像，然后安装ubuntu**

因为u盘忘记放哪儿了，就准备采取上面的方案。但是试了很多次，总是出现错误。一会说不能插入网卡，等各种问题，好不容易进了安装界面，一会说不能找不到U盘。 (毕竟我也只有一块硬盘)

![切图14](http://img.blog.loli.wang/2024-04-15-linuxServer/14.jpg)
![切图15](http://img.blog.loli.wang/2024-04-15-linuxServer/15.jpg)



- **连夜买了个u盘**

因为这问题纠结太久了，夜晚比较浮躁，美团买了个u盘，用了优惠券 16g 20RMB，

使用 **Etcher** 工具少烧录了，直接uefi模式启动，顺利安装 unbuntu 

![切图16](http://img.blog.loli.wang/2024-04-15-linuxServer/17.jpg)



5. 最终结果。

我最后还是失败了。在安装模拟器的过程中，发现到生态多烂多不完善，各种工具安装不上，安装好模拟器模拟器还乱码。和服务器语言有关，切换后正常了，下载模拟器游戏也各种不方便，最后还是放弃。。。 （或许过几天我还是会继续尝试下），但是感觉除了做服务器环境，用linux的话，还是不怎么好用的。。。
