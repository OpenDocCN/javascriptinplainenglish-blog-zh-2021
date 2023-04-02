# 如何强制 Vue.js 重新渲染一个组件

> 原文：<https://javascript.plainenglish.io/how-to-force-vue-js-to-reload-or-re-render-a-component-58236b9ccb84?source=collection_archive---------9----------------------->

![](img/3cdb36830dfa19a6d1aa9822044c3bb9.png)

Photo by [Daniel DiNuzzo](https://unsplash.com/@ddinuzzo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候我们想强制一个 Vue.js 组件重新加载或者重新渲染一个组件。

在本文中，我们将了解如何强制 Vue.js 组件重新加载或重新呈现组件。

# forceUpdate 方法

一种强制组件重新渲染的方法是使用`forceUpdate`方法。

例如，我们可以写:

```
<template>
  <div id="app">
    <button @click="forceUpdate">force update</button>
  </div>
</template><script>
export default {
  name: "App",
  methods: {
    forceUpdate() {
      this.$forceUpdate();
    },
  },
};
</script>
```

在我们的组件中调用`$forceUpdate`方法。

然而，当我们更新任何反应性属性时，就会进行重新渲染，因此强制重新渲染组件的更好方法是更新反应性属性。

# 更改组件的关键属性

我们可以改变组件的`key`道具，让组件重新渲染。

这是因为属性应该设置为反应属性作为其值。

和反应属性的改变将使组件重新渲染。

例如，我们可以写:

`App.vue`

```
<template>
  <div id="app">
    <HelloWorld :key="key" />
    <button @click="forceUpdate">reload</button>
  </div>
</template><script>
import HelloWorld from "./components/HelloWorld";export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      key: 0,
    };
  },
  methods: {
    forceUpdate(name) {
      this.key++;
    },
  },
};
</script>
```

`components/HelloWorld.vue`

```
<template>
  <div class="hello">hello world</div>
</template>
<script>
export default {
  name: "HelloWorld",
};
</script>
```

我们有带有被设置为`key`反应属性的`key`属性的`HelloWorld`组件。

我们有`forceUpdate`方法，当我们点击 reload 按钮时调用它。

`key`反应属性更新，这将强制`App`组件中的所有内容重新渲染，包括`HelloWorld`组件。

只要`key`的值改变，就会重新渲染。

# 结论

我们可以使用`$forceUpdate`方法或者更新组件的`key`属性来强制重新渲染或重新加载组件。

*更多内容看* [***说白了. io***](http://plainenglish.io)