---
title: "关于帮网友解决linux安装Nginx，并配置SSL这回事"
description: "关于帮网友解决linux安装Nginx这回事"
pubDate: "2024-04-30  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-04-30-linuxnginx/01.png"
tags:
    - linux安装Nginx
    - Nginx
    - Linux
---

## 忙碌的一天

前天非常忙碌，客户那边问题挺多的，忙了一天解决了大部分事情。5:30分的时候，一网友问出了奇怪的问题。

![切01](http://img.blog.loli.wang/2024-04-30-linuxnginx/01.png)

浅想一下
```他或许是想问这个Nginx配置前端来配置好，还是后端配置好。```

![切01](http://img.blog.loli.wang/2024-04-30-linuxnginx/02.png)

哦。。原来是NGINX让他来配置了，而他这边有点问题

远程帮忙看了下，用的 **腾讯云** , 并且自带Nginx，尝试直接配置反向代理。


``` bash

#user  nobody;
worker_processes  1;


events {
    worker_connections  1024;
}


http {
    include       mime.types;
    default_type  application/octet-stream;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

   server {
    listen 443 ssl;
    server_name your-domain.com;
 
    ssl_certificate ./ssl/nxesp.cn_bundle.crt; # SSL证书文件路径
    ssl_certificate_key ./ssl/nxesp.cn_bundle.key; # SSL证书密钥文件路径
 
    # SSL配置
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;
 
    # 指定加密套件（Suites）
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384';
    ssl_prefer_server_ciphers on;
 
    location / {
        proxy_pass https://your-backend-server; # 后端服务器地址
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}

```

看上去 配置没有问题，但是腾讯云上自带的nginx没有ssl套件，所以需要手动安装。我觉着太麻烦了。。直接重装吧

1. 卸载nginx 

```bash 

killall nginx

yum remove nginx

rm -rf /usr/local/nginx
```


2. 安装nginx

``` bash
yum install nginx

#测试启动
systemctl start nginx
```
访问相应端口 安装成功


2. 配置SSL

SSL文件放入到 /etc/nginx/conf/ssl/ (我个人喜欢新建一个ssl文件夹存放ssl文件，这样方便直接./去调用),将我们的原有配置复制到新的配置文件中

```bash
 server {
    listen 443 ssl;
    server_name your-domain.com;
 
    ssl_certificate ./ssl/nxesp.cn_bundle.crt; # SSL证书文件路径
    ssl_certificate_key ./ssl/nxesp.cn_bundle.key; # SSL证书密钥文件路径
 }
```

3. 检测 Nginx 配置文件

```bash
cd /etc/nginx/

# 检查配置文件语法是否正确
nginx -t

# 重启Nginx
systemctl restart nginx
```

正常后，会显示类似下面的信息：

```bash
 nginx success .... （具体不记得）
```


![切03](http://img.blog.loli.wang/2024-04-30-linuxnginx/03.png)


嗯 看上去没问题了~


#### Centos 常用NGinx命令

```bash

# 启动nginx
systemctl start nginx

# 停止nginx
systemctl stop nginx

# 重启nginx
systemctl restart nginx

# 查看nginx状态
systemctl status nginx

# 配置nginx开机自启动
systemctl enable nginx

# 配置nginx开机不启动
systemctl disable nginx

# 查看nginx日志
cat /var/log/nginx/error.log

# 查看nginx进程
ps -ef | grep nginx

# 查看nginx配置文件
cat /etc/nginx/nginx.conf

# 检查配置文件语法是否正确
nginx -t
```