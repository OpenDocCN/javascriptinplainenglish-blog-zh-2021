# 如何使用 Vue 3 暂记组件和创建异步组件

> 原文：<https://javascript.plainenglish.io/how-to-use-the-vue-3-suspense-component-and-create-async-components-77a6c617df4c?source=collection_archive---------12----------------------->

![](img/9ba26668b0246a7c540e8a558c626c99.png)

Photo by [Andy Li](https://unsplash.com/@andasta?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为了只在需要的时候加载组件，我们可以异步加载组件。

我们还可以使用`Suspense`组件来呈现组件，组件加载时会显示回退消息。

在本文中，我们将看看如何创建异步组件并使用`Suspense`组件来呈现它们。

# Vue 3 暂记组件和创建异步组件

Vue 3 `Suspense`有`default`插槽来呈现我们想要的动态组件。

`fallback`插槽让我们显示组件加载时呈现的回退消息。

我们可以用`defineAsyncComponent`函数定义异步组件。

要一起使用它们，我们可以编写以下代码:

`main.js`

```
import { createApp, defineAsyncComponent } from "vue";
import App from "./App.vue";const sleep = (ms) => new Promise((resolve) => setTimeout(resolve, ms));const app = createApp(App);
const HelloWorldAsync = defineAsyncComponent(async () => {
  await sleep(2000);
  return import("./components/HelloWorld.vue");
});app.component("hello-world", HelloWorldAsync);app.mount("#app");
```

`App.vue`

```
<template>
  <Suspense>
    <template #default>
      <hello-world />
    </template>
    <template #fallback>
      <div>Loading...</div>
    </template>
  </Suspense>
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

在`main.js`文件中，我们有`sleep`函数来模拟加载组件的延迟。

然后我们用`createApp`函数创建 Vue app。

接下来，我们调用`defineAsyncComponenty`函数，该函数接受返回解析组件的承诺的函数。

我们调用`sleep`来添加 2000 ms 的延迟。

然后我们返回带有组件的承诺，这是通过带有组件路径的`import`函数得到的。

然后我们用`app.component`方法注册组件。

接下来，在`App.vue`中，我们添加带有`default`槽的`Suspense`组件，该槽具有我们想要显示的主要内容。

而`fallback`槽中的内容是在`default`槽中的组件加载时显示的。

`HelloWorld.vue`有我们想要显示的内容。

因此，我们应该看到“正在加载…”消息显示 2 秒钟，然后看到“hello world”显示。

# 结论

我们可以将 Vue 3 `Suspense`组件与异步组件一起使用，以异步方式动态加载组件。

组件让我们在加载异步组件时向用户显示加载消息。

*更多内容请看*[***plain English . io***](http://plainenglish.io)