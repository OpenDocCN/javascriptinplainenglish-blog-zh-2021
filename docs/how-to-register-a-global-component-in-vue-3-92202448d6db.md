# 如何在 Vue 3 中注册一个全局组件

> 原文：<https://javascript.plainenglish.io/how-to-register-a-global-component-in-vue-3-92202448d6db?source=collection_archive---------11----------------------->

![](img/a3a2df4e33d866845563fe60e4d5b173.png)

Photo by [Kyle Glenn](https://unsplash.com/@kylejglenn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望向 Vue 3 应用程序添加组件，这些组件在整个应用程序中都可用。

在这种情况下，全局组件适用于此目的。

在本文中，我们将看看如何向 Vue 3 注册一个全局组件。

# 在 Vue 3 中注册一个全局组件

要用 Vue 3 注册全局组件，我们可以使用`app.comnponent`方法。

例如，我们可以写:

`main.js`

```
import { createApp } from "vue";
import App from "./App.vue";
import HelloWorld from "./components/HelloWorld.vue";const app = createApp(App);
app.component("hello-world", HelloWorld);
app.mount("#app");
```

`App.vue`

```
<template>
  <div>
    <hello-world />
  </div>
</template><script>
export default {
  name: "App",
};
</script>
```

`components/HelloWorld.vue`

```
<template>
  <div class="hello">hello world</div>
</template><script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
};
</script>
```

在`main.js`中，我们导入`HelloWorld`组件并将其传递给`app.component`方法。

第一个参数是组件名。

第二个参数是组件本身。

然后在`App.vue`中，我们通过添加带有给定组件名的标签来使用组件。

然后在`HelloWorld.vue`中，我们给模板添加一些内容。

只有当我们使用 kebab-case 作为标记名时，组件名才起作用，因为我们用 kebab-case 标记名定义了它。

我们可以在任何其他组件中使用`hello-world`组件，因为我们已经对它进行了全局注册。

# 结论

我们可以用 Vue 3 的`app.component`方法轻松注册一个全局组件。

*更多内容请看*[***plain English . io***](http://plainenglish.io)