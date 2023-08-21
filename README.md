## 介绍

基于 Astro 的静态博客，主题使用沉冰浮水的 [wdssmq/blog-astro](https://github.com/wdssmq/blog-astro "wdssmq/blog-astro: 一个基于 Astro 的静态博客；")

## 使用

1、使用上面的仓库作为模板，创建一个新的仓库；

2、克隆到本地；

3、安装依赖及运行，推荐使用 pnpm；

```bash
pnpm install
# 调试开发
pnpm dev
# 构建
pnpm build
```

4、各种说明：

1. 这东西虽然可以当博客，但并没有一般博客意义上的「主题」规范，姑且仍然尝试将文件放到了 `src/theme-simple` 目录下，`src/pages` 则因为 Astro 的限制，只能放外边；
2. `src/theme-simple/config.ts`用于主题的配置选项；「是不是也放外边或者直接用 `consts.ts` 比较好」
3. `package.json` 内的 `name` 字段也可自行修改，虽然并没有什么用；
4. 文章内容路径为 `src/content`，可以符号链接或快捷方式到其他地方方便管理；
5. 内置了一个「关于」页面，路径 `src/content/pages/about.md`，**应该是不能删除，其他文件名也并不会被解析为新页面**；
6. 「文章」存放于`src/content/blog`路径内，可自行清空后新建；

## 文档

入门指南 🚀 Astro 文档：

[https://docs.astro.build/zh-cn/getting-started/](https://docs.astro.build/zh-cn/getting-started/ "入门指南 🚀 Astro 文档")

astro/examples/blog at latest · withastro/astro · GitHub：

[https://github.com/withastro/astro/tree/latest/examples/blog?on=github#astro-starter-kit-blog](https://github.com/withastro/astro/tree/latest/examples/blog?on=github#astro-starter-kit-blog "astro/examples/blog at latest · withastro/astro · GitHub")
