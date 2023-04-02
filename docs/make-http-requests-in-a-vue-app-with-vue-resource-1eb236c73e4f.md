# 使用 vue-resource 在 Vue 应用程序中发出 HTTP 请求

> 原文：<https://javascript.plainenglish.io/make-http-requests-in-a-vue-app-with-vue-resource-1eb236c73e4f?source=collection_archive---------11----------------------->

![](img/4ef616b54f25f2c6da486ac7db5632cc.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

vue 资源库是 Vue 应用程序的一个有用的 HTTP 客户端库。

对于提出请求来说，它是 Axios 的一个很好的替代品。

在本文中，我们将了解如何使用它通过 Vue 应用程序发出 HTTP 请求。

# 装置

我们可以通过运行以下命令来安装该库:

```
yarn add vue-resource
```

或者

```
npm install vue-resource
```

它也可以包含在脚本标签中:

```
<script src="https://cdn.jsdelivr.net/npm/vue-resource@1.5.1"></script>
```

# 提出请求

要发出请求，我们通过编写以下内容在`main.js`中注册插件:

```
import Vue from "vue";
import App from "./App.vue";
import VueResource from "vue-resource";Vue.use(VueResource);
Vue.config.productionTip = false;new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

然后，为了提出请求，我们写:

```
<template>
  <div id="app">{{response}}</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      response: {}
    };
  },
  async beforeMount() {
    const { bodyText } = await this.$http.get(
      "https://api.agify.io//?name=michael"
    );
    this.response = JSON.parse(bodyText);
  }
};
</script>
```

我们调用`this.$http.get`向一个端点发出 get 请求。

要发出 post 请求，我们可以写:

```
<template>
  <div id="app">{{response}}</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      response: {}
    };
  },
  async beforeMount() {
    const { bodyText } = await this.$http.post(
      "https://jsonplaceholder.typicode.com/posts",
      {
        title: "foo",
        body: "bar",
        userId: 1
      }
    );
    this.response = JSON.parse(bodyText);
  }
};
</script>
```

我们只是将请求体传递给第二个参数。

# 获得回应

我们可以从`headers`属性获得响应头:

```
"<template>
  <div id="app">{{response}}</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      response: {}
    };
  },
  async beforeMount() {
    const response = await this.$http.post(
      "https://jsonplaceholder.typicode.com/posts",
      {
        title: "foo",
        body: "bar",
        userId: 1
      }
    );
    console.log(response.headers.get("Expires"));
    this.response = JSON.parse(response.bodyText);
  }
};
</script>
```

我们将头键传递给`get`方法来获取它的值。

# 得到一个斑点

我们可以用`this.$http.get`方法得到一个斑点。

我们所要做的就是将`responseType`设置为`'blob'`:

```
"<template>
  <div id="app"></div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      response: {}
    };
  },
  async beforeMount() {
    const response = await this.$http.get(
      "https://picsum.photos/id/23/200/300",
      { responseType: "blob" }
    );
    const blob = await response.blob();
    console.log(blob);
  }
};
</script>
```

# 截击机

我们添加了一个拦截器来设置所有请求的请求头。

我们可以通过编写以下内容来全局设置请求头:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import VueResource from "vue-resource";Vue.use(VueResource);
Vue.config.productionTip = false;
Vue.http.interceptors.push((request) => {
  request.headers.set("X-CSRF-TOKEN", "TOKEN");
  request.headers.set("Authorization", "Bearer TOKEN");
});new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div id="app">{{response}}</div>
</template>
<script>
export default {
  name: "App",
  data() {
    return {
      response: {}
    };
  },
  async beforeMount() {
    const { bodyText } = await this.$http.post(
      "https://jsonplaceholder.typicode.com/posts",
      {
        title: "foo",
        body: "bar",
        userId: 1
      }
    );
    this.response = JSON.parse(bodyText);
  }
};
</script>
```

我们用`Vue.http.interceptors.push`方法来用`request.headers.set`方法修改请求。

# 结论

我们可以使用 vue 资源库在 Vue 应用程序中发出请求。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**