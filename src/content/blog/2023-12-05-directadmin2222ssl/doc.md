---
title: "Directadmin 2222 开启 SSL "
description: "Directadmin 2222 开启 SSL"
pubDate: "2023-12-05　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-12-05-directadmin2222ssl/01.png"
tags:
    - Directadmin
    - SSL
    - Directadmin 开启 SSL
---


太久没管理IDC.LA 网站了，这次上去，发现所有服务器面板的SSL都挂了。

    真不是个合格的网站管理者

#### 先启动LetsEncrypt

1. 在directadmin.conf中启用letsencrypt = 1选项，顺便先把ssl=0改为 ssl=1 ，使DA 2222使用SSL协议

2. 重启、build 相关组件

``` bash
echo “action=directadmin&value=restart” >> /usr/local/directadmin/data/task.queue; /usr/local/directadmin/dataskq d2000

cd /usr/local/directadmin/custombuild
./build rewrite_confs

cd /usr/local/directadmin/custombuild
./build update
./build letsencrypt
```

#### 为DA开启

先获得域名证书，设定跳转，使其生效。

``` bash
/usr/local/directadmin/scripts/letsencrypt.sh request_single us1.yunloli.com 4096

/usr/local/directadmin/directadmin set ssl_redirect_host us1.yunloli.com
service directadmin restart
```


### 相关资料

https://help.directadmin.com/item.php?id=15

https://help.directadmin.com/item.php?id=648

https://help.directadmin.com/item.php?id=629