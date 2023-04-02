# 如何配合 Vuex 使用 Axios

> 原文：<https://javascript.plainenglish.io/how-to-use-axios-with-vuex-7133510dc290?source=collection_archive---------5----------------------->

![](img/c82a48c0956a114f0cc9aea6d51c95c7.png)

Photo by [Dan Meyers](https://unsplash.com/@dmey503?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuex 是 Vue 应用程序的状态管理库。

这是 Vue 应用程序状态管理的最受欢迎的选择。

在本文中，我们将了解如何使用带有 Vuex 的 Axios HTTP 客户端。

# 运行带操作的异步代码

我们可以在动作内的 Vuex 存储中运行异步代码。

要添加动作，我们只需将`action`属性添加到传递给`Vuex.Store`构造函数的对象中。

例如，我们可以写:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import Vuex from "vuex";Vue.config.productionTip = false;
Vue.use(Vuex);const store = new Vuex.Store({
  state: {
    count: 0
  },
  mutations: {
    increment(state) {
      state.count++;
    }
  },
  actions: {
    increment(context) {
      context.commit("increment");
    }
  }
});new Vue({
  store,
  render: (h) => h(App)
}).$mount("#app");
```

用`increment`方法添加`actions`属性。

`context.commit`方法提交了我们想要改变状态的突变。

然后我们可以用`this.$store.dispatch`方法在组件中分派动作:

`App.vue`

```
<template>
  <div id="app">
    <button @click="increment">increment</button>
    <p>{{count}}</p>
  </div>
</template><script>
export default {
  name: "App",
  computed: {
    count() {
      return this.$store.state.count;
    }
  },
  methods: {
    increment() {
      this.$store.dispatch("increment");
    }
  }
};
</script>
```

因为动作中可以包含异步代码，所以我们可以只在动作方法中添加我们想要的异步代码。

代码可以更新状态。

为了使用 Axios 在我们的操作中发出请求，我们编写:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import Vuex from "vuex";
import axios from "axios";Vue.config.productionTip = false;
Vue.use(Vuex);const store = new Vuex.Store({
  state: {
    post: {}
  },
  mutations: {
    setPost(state, data) {
      state.post = data;
    }
  },
  actions: {
    async getPost(context, { id }) {
      const { data } = await axios.get(
        `https://jsonplaceholder.typicode.com/posts/${id}`
      );
      context.commit("setPost", data);
    }
  }
});new Vue({
  store,
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div id="app">
    <button @click="getPost">get post</button>
    <p>{{post}}</p>
  </div>
</template><script>
export default {
  name: "App",
  computed: {
    post() {
      return this.$store.state.post;
    }
  },
  methods: {
    getPost() {
      this.$store.dispatch("getPost", { id: 1 });
    }
  }
};
</script>
```

不同之处在于，我们用`getPost`异步方法向 API 发出请求。

然后一旦我们有了结果，我们调用`context.commit`提交`setPost`变异来更新状态。

在`setPost`突变方法中，我们获取`data`参数的值，然后将其设置为`state.post`的值，以更新`post`状态。

在`App.vue`中，我们以同样的方式用`this.$store.dispatch`方法调度`getPost`动作。

只是我们添加了一个带有`id`属性的对象，将其作为第二个参数传递给`getPost`动作方法。

在`post`计算属性中，我们返回`this.$store.state.post`属性的值。

现在，当我们单击 get post 按钮时，我们应该看到通过`post` computed 属性从`post`状态显示的 post 数据。

# 结论

我们可以将 Axios 与 Vuex 一起使用，只要我们将 Axios 代码放在 Vuex store 操作中。

一个动作方法可以有异步代码，但是变异不能。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**