# 使用 vue-infinite-scroll 为 Vue 应用添加无限滚动

> 原文：<https://javascript.plainenglish.io/add-infinite-scrolling-to-a-vue-app-with-vue-infinite-scroll-cd7cc75121e?source=collection_archive---------4----------------------->

![](img/c1d573a17595965316a32702b910db68.png)

Photo by [Mark Rasmuson](https://unsplash.com/@mrasmuson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无限滚动是指用户可以不断滚动以获取新数据并将其追加到页面底部。

在本文中，我们将看看如何使用 vue-infinite-scroll 插件为 Vue 应用程序添加无限滚动。

# 安装

我们可以通过运行以下命令来安装它:

```
npm install vue-infinite-scroll --save
```

# 使用

安装好之后，我们就可以使用了。

首先，我们在`main.js`中注册插件:

```
import Vue from "vue";
import App from "./App.vue";
import infiniteScroll from "vue-infinite-scroll";
Vue.use(infiniteScroll);
Vue.config.productionTip = false;new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

这将全局注册它。

我们也可以通过书写以下内容在本地注册:

```
import infiniteScroll from 'vue-infinite-scroll'
new Vue({
  directives: {infiniteScroll}
})
```

然后我们可以用它来写:

```
<template>
  <div id="app">
    <div v-infinite-scroll="loadMore" infinite-scroll-disabled="busy" infinite-scroll-distance="10">
      <div v-for="n in num" :key="n">
        <img :src="`https://picsum.photos/id/${n}/300/150`">
      </div>
    </div>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      num: 10,
      busy: false
    };
  },
  methods: {
    loadMore() {
      this.busy = true;
      setTimeout(() => {
        this.num += 50;
        this.busy = false;
      }, 1000);
    }
  }
};
</script>
```

`v-infinite-scroll`指令使 div 成为一个无限滚动的容器。

我们将它设置为`loadMore`方法，以便我们移动。

`infinite-scroll-distance`是相对于屏幕底部的百分比距离。

`loadMore`方法将在屏幕距离内滚动屏幕。

`infinite-scroll-disabled`让我们在某些条件为`true`时禁用无限滚动。

当我们加载更多数据时，我们显示无限滚动。

# 结论

我们可以用 vue 无限滚动插件给 Vue 应用添加无限滚动。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**