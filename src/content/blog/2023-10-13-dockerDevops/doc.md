---
title: "docker 配置 nginx 环境"
description: "docker 配置 nginx 环境"
pubDate: "2023-10-13　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-10-13-dockerDevops/01.png"
tags:
    - docker 
    - 学习折腾
    - docker 容器
---

如果是windows环境下，记得安装上 ubuntu ，然后安装好docker Desktop

   ![切图1](http://img.blog.loli.wang/2023-10-13-dockerDevops/01.png)

##  搜索nginx镜像

``` bash

打开ubuntu的命令行。

 docker search nginx # 搜索nginx镜像
 
 NAME: 镜像仓库源的名称
 DESCRIPTION: 镜像的描述
 OFFICIAL: 是否为 docker 官方发布
 stars: 类似 Github 里面的 star
 AUTOMATED: 自动构建。
``` 

 ![切图2](http://img.blog.loli.wang/2023-10-13-dockerDevops/02.png)

## 拉取最新NGINX Docker镜像 

``` bash

docker pull nginx:latest # latest 代表最新版本的意思 同样也可以在这里制定版本

```

 ![切图3](http://img.blog.loli.wang/2023-10-13-dockerDevops/03.png)

 ## 查看镜像

``` bash 
 docker images # 查看所有已经拉取和自己的镜像
```
![切图4](http://img.blog.loli.wang/2023-10-13-dockerDevops/04.png)

## 使用执行镜像创建一个新的容器

``` bash 

docker run -it nginx

语法：docker run [OPTIONS] IMAGE [COMMAND] [ARG…]

OPTIONS说明：
-a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项；
-d: 后台运行容器，并返回容器ID；
-i: 以交互模式运行容器，通常与 -t 同时使用；
-P: 随机端口映射，容器内部端口随机映射到主机的端口
-p: 指定端口映射，格式为：主机(宿主)端口:容器端口
-t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用；
–name="nginx-lb": 为容器指定一个名称；
–dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致；
–dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致；
-h “mars”: 指定容器的hostname；
-e username=“ritchie”: 设置环境变量；
–env-file=[]: 从指定文件读入环境变量；
–cpuset="0-2”" or --cpuset="0,1,2": 绑定容器到指定CPU运行；
-m :设置容器使用内存最大值；
–net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型；
–link=[]: 添加链接到另一个容器；
–expose=[]: 开放一个端口或一组端口；
–volume , -v: 绑定一个卷


# 使用指令

docker run -it --name="testNgx" nginx

```

![切图5](http://img.blog.loli.wang/2023-10-13-dockerDevops/05.png)

可以看到我们这里有了新的我们创建的容器。可以对容器启动关闭销毁等快捷的操作。

当然 我们是nginx 要配置个ip和端口，方便本地测试

## 实践测试

写上第二个测试 ，可以看到我们正常创建了个新的容器，并8080端口映射了80端口

```  bash
# 指令
docker run --name nginx-test -p 8080:80 -d nginx
```

![切图6](http://img.blog.loli.wang/2023-10-13-dockerDevops/06.png)

![切图7](http://img.blog.loli.wang/2023-10-13-dockerDevops/07.png)

![切图8](http://img.blog.loli.wang/2023-10-13-dockerDevops/08.png)

改变docker nginx的conf配置改为自己的配置就可以啦

