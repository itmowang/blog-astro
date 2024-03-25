---
title: "Windows情况下，Vite配置https证书"
description: "Windows情况下，Vite配置https证书"
pubDate: "2024-03-25  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-03-25-vite-https/13.png"
tags:
    - vite
    - Windows情况下，Vite配置https证书
    - 前端进阶
---

# 出现问题 

和往常一样，工作日工作没做完，默默地的周六来公司加班修改项目代码，周末写没人打扰写代码真的是太爽了！，感觉一切顺顺利利没什么问题。下班走的时候还心里想像 **我写的代码就是诗** 

直到周一，同事问我开发环境有BUG，我还在想我写的代码怎么可能会有Bug，迅速查看问题，发现问题

```jsx
crypto.randomUUID()
```

![切图1](http://img.blog.loli.wang/2024-03-25-vite-https/01.png)

我只是生成个UUID，有什么问题？？？

本地开发环境下看上去也没问题啊，我对我同事产生了质疑，我以为是他浏览器的问题，但是我发现开发环境没问题，发现localhost环境地址上确实没问题，内网地址上确实这个问题，

打开MDN 翻看API兼容程度，以及正常的使用操作

tips
![切图2](http://img.blog.loli.wang/2024-03-25-vite-https/02.png)

我明白了问题所在，但是又不想使用第三方库，考虑在本地配置下Https


## vite 修改 

Vite 默认使用的是http 需要修改下

``` bash
# vite.config.ts
server: {
    https:true
}
```

``` bash
# package.json
"scripts":{
    "dev": "vite --host"
}
```

## mkcert

**mkcert** 是一个创建自签名证书的工具

``` bash
# 全局安装mkcert
npm install -g mkcert
```

编写相应的sh脚本,方便初始化证书

```sh
#!/bin/bash

DIR="./cert"

echo "开始执行portmax cert脚本"

if [ ! -e $DIR ]
then 
     mkdir -p $DIR
fi

cd $DIR

mkcert create-ca 

mkcert create-cert --domains localhost 127.0.0.1 192.168.0.61
```
![切图3](http://img.blog.loli.wang/2024-03-25-vite-https/03.png) 

##  windows 安装证书

打开 cert文件夹 ，双击ca.crt 和 cert.crt , 点开后选择 **"安装证书"**

![切图4](http://img.blog.loli.wang/2024-03-25-vite-https/04.png) 
![切图5](http://img.blog.loli.wang/2024-03-25-vite-https/05.png) 


但是看我们生成的证书 windows 还是不受信任的，我们需要将此证书启用信任



### windows 将CA证书启用信任

使用 " win+R " 打开运行对话框。输入 "mmc" 然后回车

选择 左上角 "文件"，选择管理或删除管理单元

![切图6](http://img.blog.loli.wang/2024-03-25-vite-https/06.png) 

在 **"管理或删除管理单元"** 选择证书，并**添加证书**，回到**mmc**控制台

![切图7](http://img.blog.loli.wang/2024-03-25-vite-https/07.png) 

![切图8](http://img.blog.loli.wang/2024-03-25-vite-https/08.png) 

选择 **受信任的根证书颁发机构**，然后选择**证书**, 右键选择**任务**， 导入我们项目文件里的证书


![切图9](http://img.blog.loli.wang/2024-03-25-vite-https/09.png) 

![切图10](http://img.blog.loli.wang/2024-03-25-vite-https/10.png) 

接下来就重回上面的步骤 双击ca.crt 和 cert.crt ，然后点击安装证书，可以看到当前证书是受信任的了，导入选择 **本地计算机**

![切图11](http://img.blog.loli.wang/2024-03-25-vite-https/11.png) 



### vite中验证证书是否生效

修改 vite.config.ts

```tsx
server: { 
 https: {
   cert: fs.readFileSync(path.join(__dirname, 'keys/cert.crt')),
   key: fs.readFileSync(path.join(__dirname, 'keys/cert.key')),
 },
}

```



![切图12](http://img.blog.loli.wang/2024-03-25-vite-https/12.png)


验证成功

![切图13](http://img.blog.loli.wang/2024-03-25-vite-https/13.png)
![切图14](http://img.blog.loli.wang/2024-03-25-vite-https/14.png)


### 后续。

虽然可以本地可以https了，但是去同事那边访问，也要去他那边导入证书 这样会显得很麻烦，因为是开发环境，做不了什么很好的操作，所以还是不用浏览器的生成 UUID的API了 。

还有，如果是为了本地测试，并且是Vite的话，完全没必要使用 **mkcert** , 有相关的Vite插件。

  [vite-plugin-basic-ssl](https://github.com/vitejs/vite-plugin-basic-ssl) 



### 相关资料
  [vite-plugin-basic-ssl](https://github.com/vitejs/vite-plugin-basic-ssl) 
  [mkcert](https://www.npmjs.com/package/mkcert#create-a-certificate) 
