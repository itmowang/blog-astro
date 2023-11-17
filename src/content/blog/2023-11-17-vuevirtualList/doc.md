---
title: "简单虚拟列表 + 无限滚动"
description: "简单虚拟列表 + 无限滚动"
pubDate: "2023-11-17　23:27:24"
heroImage: "http://img.blog.loli.wang/2023-11-17-vuevirtualList/1.gif"
tags:
    - 虚拟列表
    - 虚拟列表无限滚动
    - 学习折腾
---

## 为什么要有虚拟列表这个东西

很多时候前端被迫被逼着接收上百条，上千条，上万条数据（因为需求的缘故），没有相关经验的前端会直接直接赋值渲染上去。
但是这样子操作是有很大的弊端的。轻则让浏览器卡顿，重则浏览器崩溃。更严重的老板直接过来骂人。

也就是说，我们不能一股脑的直接赋值，要有合理的方案。

1. 后端给出分页 (是最好的处理方式 有什么东西是不能让后端给前端压力的呢)
2. 前端将数据切成小块 进行分页 (但是可能业务被迫需要更加直观的展示不让使用分页)
3. 前端通过搜索去过滤数据再渲染 (可以存入到缓存里,读取缓存内的数据,但是会有过滤后还是有大量数据的问题，和缓存有大小问题等限制，是不合理的方案)
4. 虚拟列表 (通过滚动条只渲染可见部分，随着滚动加载最新的数据，非常合理的方式)

通过以上解释，虚拟列表是最佳合理的方案，实例：

``` vue
<template>
  <div id="app">
    <div
      class="virtual-list-container"
      ref="listContainerRef"
      @scroll="handleScroll"
    >
      <div class="list-phantom">
        <div
          class="list-item"
          v-for="(item, index) in state.visibleItem"
          :key="index"
        >
          虚拟化列表数据 {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="tsx" setup>
import { ref, reactive, onMounted } from "vue";

let state = reactive({
  visibleItem: [] as any,
  visibleItemCount: 20, // 可见区域显示多少条
  count: 800000, // 需要生成的数据总条数
});

// 数据生成函数
const genertteItems = (count: number): any[] => {
  const items: any = [];
  Array.from({ length: count }).forEach((item, index: number) => {
    items.push({ id: index, name: `${index}名称` });
  });
  return items;
};

// 关键代码
// 通过ref获取带有滚动条的dom
const listContainerRef = ref<any>(null);

// 滚动事件
const handleScroll = () => {
  // 滚动容器
  const container = listContainerRef.value;
  // 获取容器当前至容器顶部距离多远
  const scrollTop = container?.scrollTop || 0;
  // 获取容器可视区域总高度
  const scrollHeight = container?.scrollHeight || 0;
  // 获取容器的总高度
  const containerHeight = container?.clientHeight || 0;
  // 如果滚动距离加上可是高度大于总高度 说明到了容器底部
  if (scrollTop + containerHeight >= scrollHeight) {
    // 滚动到底部加载更多数据
    loadMoreData();
  }
};

// 加载更多函数
const loadMoreData = () => {
  const startIndex = state.visibleItem.length;
  const endIndex = startIndex + state.visibleItemCount;
  const newItems = genertteItems(state.count).slice(startIndex, endIndex);
  state.visibleItem = [...state.visibleItem, ...newItems];
};

onMounted(() => {
  handleScroll(); // 确保组件挂载后初始化一次数据\
});
</script>

<style lang="less">
.list-item {
  height: 80px;
  border: 1px solid red;
}
.virtual-list-container {
  overflow-y: auto;
  height: 400px; /* 容器高度 */
  position: relative;
}
.list-phantom {
  position: absolute;
  width: 100%;
  pointer-events: none;
}
</style>

```

实现效果

![切图1](http://img.blog.loli.wang/2023-11-17-vuevirtualList/1.gif)
