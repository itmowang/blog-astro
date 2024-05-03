---
title: "使用Nestjs + prisma 构建 REST API"
description: "使用nestjs + prisma构建REST API"
pubDate: "2024-05-03  23:27:24"
heroImage: "http://img.blog.loli.wang/2024-05-03-prismaNestApi/14.png"
tags:
    - nestjs
    - prisma
    - RESTAPI
---

## 2024 年 5月 3日

难得的51假期,5天假期，本应该是好好去玩的一天，可惜没有什么地方可以去，并且还报了驾校正在练车，正好今天没有安排，正好熟悉下nestjs吧。


### 使用nest cli 安装nest空项目

```bash
# 创建空的 nest 项目
npx @nestjs/cli new <项目名>
```
![切01](http://img.blog.loli.wang/2024-05-03-prismaNestApi/01.png)

启动正常

![切03](http://img.blog.loli.wang/2024-05-03-prismaNestApi/02.png)

### 安装prisma, 并初始化

```bash
# 安装prisma
pnpm install -D prisma

# 初始化prisma
npx prisma init
```
会增加一个prisma 的文件夹， 里面的schenma.prisma 是我们的数据库配置文件

![切03](http://img.blog.loli.wang/2024-05-03-prismaNestApi/03.png)
![切04](http://img.blog.loli.wang/2024-05-03-prismaNestApi/04.png)


### 本地安装mysql

比较常规，每个人情况不一样，我在这里使用的mysql


### 配置env环境变量

在初始化prisma的时候，会生成一个env的配置文件，使用env文件配置环境变量,如果你是用的其他的数据库参考文档
https://www.prisma.io/docs/orm/reference/connection-urls

我这里使用的是mysql，先修改指定数据库然后修改env配置

```jsx
// prisma/schema.prisma
datasource db {
  provider = "mysql"
  url      = env("DATABASE_URL")
}
```

```bash
DATABASE_URL="DATABASE_URL="mysql://prisma:123456@localhost:3306/prisma"
```

### 增加数据模型

此处是定义了一个 Article的表 内有相关字段，以及字段代表的类型

```jsx
// prisma/schema.prisma

model Article {
  id          Int      @id @default(autoincrement())
  title       String   @unique
  description String?
  body        String
  published   Boolean  @default(false)
  createdAt   DateTime @default(now())
  updatedAt   DateTime @updatedAt
}
```


### 第一次执行
当你定义好数据模型后 我们需要执行一次指令 让数据库和prisma同步, 你也可以记录到package.json中的script指令中

```bash
# 指令
npx prisma migrate dev --name "init"
```

![切05](http://img.blog.loli.wang/2024-05-03-prismaNestApi/05.png)

![切06](http://img.blog.loli.wang/2024-05-03-prismaNestApi/06.png)


执行成功后，这里可以看到我们的数据库内自动生成了，我们刚刚设置的模型。每次修改我们的数据库模型都要去生成一遍。


### 增加默认数据填充数据库

创建一个为 **prisma/seed.ts** 的文件，

```jsx

// prisma/seed.ts

import { PrismaClient } from '@prisma/client';

// initialize Prisma Client
const prisma = new PrismaClient();

async function main() {
  // create two dummy articles
  const post1 = await prisma.article.upsert({
    where: { title: 'Prisma Adds Support for MongoDB' },
    update: {},
    create: {
      title: 'Prisma Adds Support for MongoDB',
      body: 'Support for MongoDB has been one of the most requested features since the initial release of...',
      description:
        "We are excited to share that today's Prisma ORM release adds stable support for MongoDB!",
      published: false,
    },
  });

  const post2 = await prisma.article.upsert({
    where: { title: "What's new in Prisma? (Q1/22)" },
    update: {},
    create: {
      title: "What's new in Prisma? (Q1/22)",
      body: 'Our engineers have been working hard, issuing new releases with many improvements...',
      description:
        'Learn about everything in the Prisma ecosystem and community from January to March 2022.',
      published: true,
    },
  });

  console.log({ post1, post2 });
}

// execute the main function
main()
  .catch((e) => {
    console.error(e);
    process.exit(1);
  })
  .finally(async () => {
    // close Prisma Client at the end
    await prisma.$disconnect();
  });


```

在package.json中添加, 该命令使用 npx prisma db seed 的时候会自动执行，这样数据库内就会自动增加2条数据

```bash
npx prisma db seed
```

``` jsx
 "prisma": {
    "seed": "ts-node prisma/seed.ts"
 }
```

![切06](http://img.blog.loli.wang/2024-05-03-prismaNestApi/07.png)
![切08](http://img.blog.loli.wang/2024-05-03-prismaNestApi/08.png)

### 创建 Prisma 服务

nest提供了一个直接使用cli生成模块和服务的指令

```bash
npx nest generate module prisma
npx nest generate service prisma
```


### 设置 swagger

Swagger是一个使用 API 规范记录 API 的工具。 Nest 有一个专门用于 Swagger 的模块。

```bash
# 安装@nestjs/swagger 和  swagger-ui-express
pnpm install --save @nestjs/swagger swagger-ui-express
```

在 **main.ts**中初始化 swagger

```jsx
import { NestFactory } from '@nestjs/core';
import { AppModule } from './app.module';
import { SwaggerModule, DocumentBuilder } from '@nestjs/swagger';

async function bootstrap() {
  const app = await NestFactory.create(AppModule);

  const config = new DocumentBuilder()
    .setTitle('Median')
    .setDescription('The Median API description')
    .setVersion('0.1')
    .build();

  const document = SwaggerModule.createDocument(app, config);
  SwaggerModule.setup('api', app, document);

  await app.listen(3000);
}
bootstrap();

```


我们启动一下,可以看到 **/api** 加上路径后，swagger访问正常



![切08](http://img.blog.loli.wang/2024-05-03-prismaNestApi/09.png)


### 生成 REST 资源

可以看到swagger虽然正常了 但是我们目前还没有任何的接口去供我们查阅api。

```bash
# 快速生成REST资源
npx nest generate resource
```
使用指令可以快速帮我们生成**REST**资源，供我们修改使用，重新启动一下。可以看到出现了我们需要的REST接口资源


![切10](http://img.blog.loli.wang/2024-05-03-prismaNestApi/10.png)




### 连接prisma 进行CURD

可以看到我们的api资源对应的，都是 **@Body(),@Query()** 等装饰器来生成这个API。

![切11](http://img.blog.loli.wang/2024-05-03-prismaNestApi/11.png)

但是要让 **Swagger** 访问到我们的**prsima** 进行**CURD**操作还需要一定的步骤,进入到我们的articles.module.ts文件，引入Prisma的模型.

```jsx
// src/articles/articles.module.ts

import { Module } from '@nestjs/common';
import { ArticlesService } from './articles.service';
import { ArticlesController } from './articles.controller';
import { PrismaModule } from 'src/prisma/prisma.module';

@Module({
  controllers: [ArticlesController],
  providers: [ArticlesService],
  imports: [PrismaModule],
})
export class ArticlesModule {}

```

将 **PrismaService**注入到**ArticlesService** 中, 并且使用他来访问数据库，需要增加一个构造函数


```jsx
// src/articles/articles.service.ts
import { Injectable } from '@nestjs/common';
import { CreateArticleDto } from './dto/create-article.dto';
import { UpdateArticleDto } from './dto/update-article.dto';
import { PrismaService } from 'src/prisma/prisma.service';

@Injectable()
export class ArticlesService {
  constructor(private prisma: PrismaService) {}
    //   ...CURD
}

```



### 更改一个测试接口用来测试

我只需要简单写一个接口，查询出表**article**所有数据。看看是否成功 。

```jsx
// src/articles/articles.service.ts

import { Injectable } from '@nestjs/common';
import { CreateArticleDto } from './dto/create-article.dto';
import { UpdateArticleDto } from './dto/update-article.dto';
import { PrismaService } from 'src/prisma/prisma.service';

@Injectable()
export class ArticlesService {
  constructor(private prisma: PrismaService) {}
  create(createArticleDto: CreateArticleDto) {
    return 'This action adds a new article';
  }

  findAll() {
    return this.prisma.article.findMany({});
  }

  findOne(id: number) {
    return `This action returns a #${id} article`;
  }

  update(id: number, updateArticleDto: UpdateArticleDto) {
    return `This action updates a #${id} article`;
  }

  remove(id: number) {
    return `This action removes a #${id} article`;
  }
}


```

![切12](http://img.blog.loli.wang/2024-05-03-prismaNestApi/12.png)
![切13](http://img.blog.loli.wang/2024-05-03-prismaNestApi/13.png)
![切14](http://img.blog.loli.wang/2024-05-03-prismaNestApi/14.png)


### 相关文章

[Prsima 官网](https://www.prisma.io/blog/nestjs-prisma-rest-api-7D056s1BmOL0#introduction)

[Github编写的示例DEMO](https://github.com/itmowang/prisma-nest-mysql-demo)
