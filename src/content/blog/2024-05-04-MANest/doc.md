---
title: "Nestjs的微服务"
description: "使用NestJs的微服务"
pubDate: "2024-05-04  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-05-04-MANest/01.png"
tags:
    - nestjs
    - 微服务
    - RESTAPI
---

## 2024 年 5月 3日

到晚上了，QQ没人找，微信没人回。当然这么好的假日应该出去玩才对，但是我不愿意浪费这点时间给自己好好休息。偶然看到了某技术群聊微服务，很有兴趣，看资料折腾下吧。


## 使用nest的cli工具创建项目

```bash
# 全局安装nestjs的cli
npm i -g @nestjs/cli

# 安装第一个项目
nest new aa

# 启动aa项目
cd aa
pnpm run start
```

![切1](http://img.blog.loli.wang/2024-05-04-MANest/01.png)

启动访问成功

![切2](http://img.blog.loli.wang/2024-05-04-MANest/02.png)

## 创建一个 微服务项目

``` bash
# 通过cli安装一个新的项目
nest new micro-service

# 安装nestjs 微服务插件
pnpm add @nestjs/microservices
```

## 引用 @nestjs/microservices 修改main.ts

将原本启动http服务,改为启动微服务

```jsx
// main.ts

import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { Transport, MicroserviceOptions } from '@nestjs/microservices';

async function bootstrap() {
  // const app = await NestFactory.create(AppModule);

  const app = await NestFactory.createMicroservice<MicroserviceOptions>(
    AppModule,
    {
      transport: Transport.TCP,
      options: {
        port: 8888,
      },
    },
  );

  await app.listen();
}
bootstrap();

```


修改 **app.controller.ts** 改为接受Message通知，

```jsx
// app.controller.ts

import { Controller, Get } from '@nestjs/common';
import { AppService } from './app.service';
import { MessagePattern } from '@nestjs/microservices';

@Controller()
export class AppController {
  constructor(private readonly appService: AppService) {}

  @MessagePattern('sum')
  sum(numArr: Array<number>): number {
    return numArr.reduce((total, item) => total + item, 0);
  }
}

```


## 改造 aa 项目，让他能够连接微服务

```bash
# 安装微服务依赖
pnpm add @nestjs/microservices

```

进入 app.module.ts 注册**微服务**那个项目,指定TCP端口为8888，让他直到我们的微服务项目端口是8888

```jsx
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { ClientsModule, Transport } from '@nestjs/microservices';

@Module({
  imports: [

    ClientsModule.register([
      {
        name: 'MICRO_SERVICE',
        transport: Transport.TCP,
        options: {
          port: 8888,
        },
      },
    ]),

  ],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}

```

![切2](http://img.blog.loli.wang/2024-05-04-MANest/03.png)

这样就注册完了。 然后在 **aa** 项目中注册客户端代理**clientProxy**


```jsx
//app.controller.ts

import { Controller, Get, Query, Inject } from '@nestjs/common';
// import { AppService } from './app.service';
import { ClientProxy } from '@nestjs/microservices';
import { Observable } from 'rxjs';

@Controller()
export class AppController {
  constructor(@Inject('MICRO_SERVICE') private serviceClient: ClientProxy) {}

  @Get()
  server(@Query('num') str): Observable<number> {
    const numArr = str.split(',').map((item) => parseInt(item));

    return this.serviceClient.send('sum', numArr);
  }
}

```


重启下微服务，查看结果

访问 aa 服务的看看是否有进行一个累加的计算 http://localhost:3000/?num=1,2,3

能够正常进行的互相传递接收，微服务配置成功

![切2](http://img.blog.loli.wang/2024-05-04-MANest/04.png)
![切2](http://img.blog.loli.wang/2024-05-04-MANest/05.png)




## 总结

照葫芦画瓢整的，虽然能够理解，但是目前没有合适的东西能让我启用这一套，当作学习记录一下吧


[神说要有光 - 掘金](https://juejin.cn/post/7207637337571901495?searchId=202405032014240A690D4981415C621CB4)

[我的github - nestjs 微服务demo](https://github.com/itmowang/nest-microservices-demo)
