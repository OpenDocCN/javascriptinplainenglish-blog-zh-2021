# Vue.js 中的选项 API 与组合 API—权威指南

> 原文：<https://javascript.plainenglish.io/option-api-vs-composition-api-in-vue-js-a-definitive-guide-2a04a398b3ce?source=collection_archive---------2----------------------->

## 我们应该使用哪一个？逐步比较。

![](img/6788a9db0fb12a22c81db7652868a246.png)

Photo by [Alvaro Reyes](https://unsplash.com/@alvarordesign?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue.js 3 与组合 API 捆绑在一起，可以用来代替选项 API。

以前版本的 Vue.js 使用 Options API 来构建和开发 Vue.js 应用程序。

Options API 有一些限制，而 Composition API 的引入就是为了解决这些限制。

在本文中，我们将逐步比较 Options API 和 Composition API，并了解使用它们的各种方法。

为了更好地理解和明确比较这两者，我们将使用这两者构建一个简单的应用程序，并比较应用程序的结构。

## **选项 API**

我们将构建一个简单的名称应用程序。这个应用程序将接受一个输入，我们为它提供一个名称，然后它将这个名称呈现到页面上。就这么简单。

## **样本代码:**

```
<template>
<img alt=”Vue logo” src=”./assets/logo.png” />
<div>
<h2>MY NAME</h2><p>{{ state.age }}</p><input v-model=”state.name” type=”text “ placeholder=”enter name to add” /><button [@click](http://twitter.com/click)=”addName”>add name</button><ul v-for=”(name, i) in state.names” :key=”i”><li>{{ name }}</li></ul></div></template><script>
export default {
name: “App”,data() {return {state: {name: “John Philip”,age: 23,names: [],},};},methods: {addName() {
this.state.names.push(this.state.name);this.state.name = “”;},},};
</script>
```

当使用 Options API 时，我们将所有的应用程序结构按其应有的方式组合在一起。

从上面的代码片段中，我们得到了保存应用程序状态的应用程序数据。我们还有一个 addName 方法，它将根据用户输入的信息更新我们的状态。

在模板组件上，我们已经附加了必要的指令，并将其与 UI 同步，这样每当状态发生变化时，我们都可以获得状态的更新版本。

## **成分 API**

假设我们要构建相同的应用程序，但是这次使用复合 API。我们的应用程序结构如下所示。

**样本代码**

```
<template>
<div>
<h2>MY NAME</h2><input v-model=”state.name” type=”text “ placeholder=”enter name to add” /><button [@click](http://twitter.com/click)=”addName”>add name</button><ul v-for=”(name, i) in state.names” :key=”i”><li>{{ name }}</li></ul>
</div>
</template><script>
import { reactive } from “vue”;export default {name: “App”,setup() {const state = reactive({name: “John Philip”,age: 23,names: [],});function addName() {state.names.push(state.name);state.name = “”;
}
return { state, addName };
},};
</script>
```

如果你检查一下，你会发现我们从 Vue 引入了 reactive。Reactive 负责双向数据绑定。这提供了组件 UI 和状态之间的同步。我们可以使用 ref 或 reactive，以满足您的开发要求。

## **小对比**

如果我们比较两者的应用程序结构，我们肯定会注意到 Composition API 为应用程序结构提供了更简单、更干净、更可读的代码。对于 Options API，生命周期挂钩之类的东西会降低代码的可读性。

尽管两者都可以用来开发应用程序，但是对于需要大量功能和组织的更复杂的应用程序，组合 API 是最好的选择。

与 Options API 相比，Composition API 还提供了简单的代码重用。

也就是说，你觉得两者中哪一个更舒适、更容易使用？我仍然试图根据我正在开发的应用程序来使用这两者。

## **最终想法**

感谢您阅读本文到目前为止。希望对你有帮助。请不要犹豫与他人分享这篇文章。

## **更多阅读:**

[](/all-you-need-to-know-about-javascript-object-notation-json-a3290231019a) [## 关于 JavaScript 对象表示法(JSON ),您需要知道的是

### 了解关于 JSON 的一切

javascript.plainenglish.io](/all-you-need-to-know-about-javascript-object-notation-json-a3290231019a) [](/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99) [## JavaScript 算法和数据结构挑战——Fizz Buzz

### JavaScript 中的 Fizz Buzz challenge 黑客团队的一个编程挑战的解决方案。

javascript.plainenglish.io](/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)