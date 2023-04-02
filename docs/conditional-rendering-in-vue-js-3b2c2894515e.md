# Vue.js 中的条件渲染

> 原文：<https://javascript.plainenglish.io/conditional-rendering-in-vue-js-3b2c2894515e?source=collection_archive---------26----------------------->

## 了解 Vue.js 中的条件渲染

![](img/0205c81932fba2d9ae1728628fdd9b7b.png)

Photo by Denis Irgin

Vue.js 捆绑了一些惊人的功能。令人惊讶的特性之一是条件渲染，它允许我们在特定条件下渲染模板。

假设我们有这样一种情况，我们只想在满足特定条件时呈现某个块或模板，这就是条件呈现派上用场的地方。

Vue.js 甚至通过引入一个我们可以轻松实现的指令来有条件地呈现元素或块，使之变得简单。

Vue.js 中的条件渲染可以用 ***v-if，v-else，*** 和 ***v-else-if*** 指令实现。

我们可以用来有条件地渲染对象的另一个指令是 ***v-show*** 指令。

条件渲染的用例

*   显示或隐藏块。
*   在应用程序之间切换。
*   实现权限。

让我们来看一个场景，当用户完成一个阶段时，我们希望呈现一些文本块。

以下面的代码片段为例

```
 <template> <div>
     <div v-if=”name” class=”pt-30">
        <h2>Name value is {{ name }}</h2>
     </div>
 </div></template>
 <script>export default {
 data() {
 return { name: “john”,
 }; },
};
</script>
<style scoped>
</style> 
```

从上面的代码片段来看，如果 name 值是 truthy，那么 div 将被呈现到 components 块中。

我们可以类似地使用 v-else 进行回退，以防条件计算不为真。

```
<template>
 <div> <div v-if=”name” class=”pt-30">
          <h2>Name value is {{ name }}</h2>
    </div> <div v-else class=”pt-30">
          <h2>Name value is Unfilled</h2>
    </div> </div>
</template>
 <script>export default {
 data() {
 return {
 name: “john”,
 };
 },
};
</script>
<style scoped>
</style>
```

在代码片段中，我们添加了 v-else 指令，以防条件不正确。

如果您希望根据不止一个条件而是各种特定条件有条件地呈现元素，该怎么办？

Vue.js 支持你。你可以实现使用 ***v-else-if*** 指令来代替。
***v-else-if***指令充当 else if 语句。当您想要基于各种条件有条件地呈现元素时，这个指令就派上了用场。

## **出发前**

感谢您到目前为止阅读了这篇文章。如果你觉得它有帮助，请不要犹豫，让我知道在评论部分和分享。

## **更多阅读:**

[](/setting-up-nuxt-js-and-tailwind-css-the-right-way-40247f56064f) [## 正确设置 Nuxt.js 和 Tailwind CSS

### 了解如何无缝设置 Nuxt.js 和 Tailwind。

javascript.plainenglish.io](/setting-up-nuxt-js-and-tailwind-css-the-right-way-40247f56064f) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)