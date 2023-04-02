# 使用 vue-masonry 插件将照片磁贴添加到 Vue 应用程序

> 原文：<https://javascript.plainenglish.io/add-photo-tiles-to-a-vue-app-with-the-vue-masonry-plugin-70f8a05076c7?source=collection_archive---------20----------------------->

![](img/ee643b7ae8e46f2ebb88f93be30e9f6f.png)

Photo by [Jaz Viccarro](https://unsplash.com/@viccarrocreative?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们可以通过 vue-masonry 插件轻松地将照片网格添加到 Vue 应用程序中。

在这篇文章中，我们将看看如何添加照片瓷砖。

# 装置

我们可以通过运行以下命令来安装它:

```
npm install vue-masonry --save
```

或者添加一个`script`标签:

```
<script src="https://unpkg.com/vue-masonry@0.11.3/dist/vue-masonry-plugin-window.js"></script>
```

如果我们安装了这个包，那么我们通过编写以下代码来注册这个插件:

```
import Vue from "vue";
import App from "./App.vue";
import { VueMasonryPlugin } from "vue-masonry";
Vue.use(VueMasonryPlugin);
Vue.config.productionTip = false;new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

在`main.js`里。

如果我们加上`script`标签，那么我们写:

```
var VueMasonryPlugin = window["vue-masonry-plugin"].VueMasonryPlugin
Vue.use(VueMasonryPlugin)
```

去注册它。

# 使用

一旦我们做到了这一点，我们写道:

```
<template>
  <div id="app">
    <div v-masonry transition-duration="0.3s" item-selector=".item">
      <div v-masonry-tile class="item" v-for="n in 100" :key="n">
        <img :src="`https://picsum.photos/id/${n}/200/300`">
      </div>
    </div>
  </div>
</template><script>
export default {
  name: "App"
};
</script>
```

添加照片网格。

`v-masonry-tile`使 div 成为一个图块。

`v-masonry`使一个元素成为照片网格的容器。

`transition-duration`是过渡运行的时间长度。

`item-selector`拥有列表元素的 DOM 项目选择器。

其他道具包括`column-width`用于用数字设置列宽。

`origin-left`如果是`false`，则将组元素设置在右边而不是左边。

`origin-top`如果是`false`，则将组元素设置在底部而不是顶部。

`stamp`指定哪些元素被印在布局上。

`fit-width`设置容器的宽度以适应可用的列数。

`stagger`设置持续时间以错开项目过渡，使项目一个接一个地递增过渡。

例如，我们可以写:

```
stagger="0.03s"
```

来设置它。

`destroy-detail`是通过`masonry.destroy()`卸载砖砌体前等待的时间，单位为毫秒。

我们也可以用`this.$redrawVueMasonry(‘containerId’)`方法手动触发重绘。

`containerId`是我们想要触发重绘的块的 ID。

# 结论

我们可以使用 vue-masonry 包轻松地将照片砖石网格添加到 Vue 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**