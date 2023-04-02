# 深入探究 Vue3 组合 API

> 原文：<https://javascript.plainenglish.io/a-deep-dive-into-the-vue3-composition-api-dece990fc846?source=collection_archive---------13----------------------->

## 通过示例深入研究 vue 组合 API。

![](img/01dbe29edc44b18ed1009df5033156cf.png)

Photo by [Tudor Baciu](https://unsplash.com/@baciutudor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果你过去一直使用 vue，毫无疑问你没有使用过 Options API。

API 选项使我们能够通过在组件结构中声明数据、方法、创建的和生命周期挂钩来创建 vue 组件。还有另一种方法，我们可以使用组合 API 来创建组件。组合 API 将是 vue3 的主要部分。

引入 Composition API 是为了解决在创建组件时使用 Options API 带来的限制和缺点。创建较大的复杂程序时，Options API 的一些缺点是:

*   大型组件可能变得可读性更差，因此可维护性更差。
*   Options API 中的代码重用模式有其缺点。
*   选项 API 也使得将复杂的逻辑组合在一起变得更加困难。

Composition API 使我们能够在 setup 函数中轻松地分组和创建逻辑(函数)。

有了组合 API，我们基本上可以在组件内部设置钩子。在 setup 函数中，我们将包含所有的应用程序逻辑。

然而，我们仍然可以使用 Options API 来创建 vue 应用程序，但是对于需要更复杂逻辑、更多代码重用和更多组织的更复杂的项目，强烈建议使用 composition api。

这实际上是可选的，尽管您仍然可以使用 Options API 创建令人惊叹的应用程序。

让我们创建一个简单的 vue 项目，并看看组成 api

要创建 vue 项目，请打开您的终端并运行命令

```
vue create composition-api
```

该命令将为我们创建一个名为 composition-api 的新 vue 应用程序

现在使用您最喜欢的文本编辑器打开 composition-api 文件夹。

要使用组合 api，我们需要在组件内部创建一个设置函数。

另外，请注意，setup 函数将在任何其他生命周期挂钩之前首先运行。(已创建、计算、安装)。

在 setup 函数中，我们可以编写任何普通的 JavaScript 或逻辑。

我们必须注意的唯一区别是，当我们想要呈现与我们的组件相关联的任何东西时，我们需要返回特定的函数或变量，以使它在我们的模板组件中可用。

在 *app.vue* 中，我们可以创建如下设置功能。

```
setup() {const state = {name: “John Philip”,age: 23,};*return* { state };}
```

现在，在我们的模板组件中，我们可以使用双花括号来呈现姓名和年龄，如下所示。

```
<div><h2>{{ state.name }}</h2><p>{{ state.age }}</p></div>
```

姓名和年龄将呈现在我们的页面上。

另外，要注意 vue composition-api 不会自动绑定我们的状态数据。为了确保双向状态数据绑定，我们需要使用 refs 或 reactive。

因此，任何功能、方法和其他计算属性都可以直接写在 setup 函数中。还要记住返回需要在模板组件中呈现的任何内容。

我们将制作一个简单的应用程序，显示用户输入的姓名。

首先，因为我们需要双向数据绑定，所以我们可以使用 refs 或者 reactive。在这种情况下，我们将使用反应式。

首先，我们需要一个输入和一个提交按钮来更新我们的州数据。

```
<template><div><h2>ADD NAMES</h2><input v-model="state.name" type="text " placeholder="enter name to add" /><button @click="addName">add name</button><ul v-for="(name, i) in state.names" :key="i"><li>{{ name }}</li></ul></div></template><script>*import* { reactive } *from* "vue";*export* *default* {name: "App",setup() {const state = reactive({name: "John Philip",age: 23,names: [],});function addName() {state.names.push(state.name);state.name = "";}*return* { state, addName };},};</script>
```

在上面的代码片段中，我们有一个 input 元素，用户将在其中键入名称，附加到它的是一个 v-model 指令，它将确保状态和 UI 之间的双向数据绑定。

你可以看到我们的状态是反作用的。reactive 的作用是支持状态和 UI 之间的双向数据绑定。有了它，我们可以很容易地改变我们的状态数据。

我们还有一个函数 addName。这个函数的作用是获取用户输入的姓名，并将其放入 names 数组。

然后，它将 name 对象重置为空字符串，以防止名称出现在我们的输入部分。

如果你能从上面的功能中看到，我们的组合 api 是简单、干净和可读的代码。

假设我们使用 options api 来做类似的事情，结果应该是这样的。

```
<template><img alt="Vue logo" src="./assets/logo.png" /><div><h2>ADD NAME</h2><p>{{ state.age }}</p><input v-model="state.name" type="text " placeholder="enter name to add" /><button @click="addName">add name</button><ul v-for="(name, i) in state.names" :key="i"><li>{{ name }}</li></ul></div></template><script>*export* *default* {name: "App",data() {*return* {state: {name: "John Philip",age: 23,names: [],},};},methods: {addName() {this.state.names.push(this.state.name);this.state.name = "";},},};</script>
```

如果你比较上面的两种方法，我们可以清楚地看到，与选项 api 相比，组合 api 更容易阅读。

如果你可以看到我们有相同的应用程序，包括组合 api 和选项 api。

如果您比较这两种方法，我们可以看到选项 api 有更多的代码和许多功能，而组合 api 有简单的代码和可读的代码功能。我们也可以很容易地重用代码。

你对 Composition API 有什么看法，你觉得它真的有必要，并且比 Options API 更喜欢它吗？

## **结论**

简单回顾一下，我们已经看到了如何在 Vue 3 中使用 Composition API 来代替 options api。

谢谢你把这篇文章读到这里。如果你觉得这篇文章有帮助，请不要犹豫，分享出来。