# Vue 3 的新功能和变化指南

> 原文：<https://javascript.plainenglish.io/vue-3-breaking-changes-and-new-features-72e62515fda4?source=collection_archive---------9----------------------->

![](img/93467a5b1959a1a38bb35d0136911f48.png)

Vue 3 团队为开发者发布了一个 alpha 版本，这样他们就可以使用 Vue 3 提供的一些特性。

它不能用于生产。但是学习新特性和找出应该解决的错误总是好的。

> Vue.js 是最好最简单的客户端 JavaScript 框架之一，开发曲线较低。

## Vue 3 突破性变化

如果您计划从 Vue 2 迁移到 Vue 3，您应该知道 Vue 3 中的重大变化。让我们开始吧。

**1。创建 Vue 应用程序**

要现在创建 Vue 应用程序，我们将不会创建 Vue 对象的实例；相反，我们将使用一个特殊的`createApp()`函数。

下面是我们如何在 Vue 2 中创建 Vue.js 应用程序:

```
new Vue({
 el: “#app”
});
```

相反，在 Vue 3 中，我们这样做:

```
const app = Vue.createApp(/* app config */);

app.mount(“#app”);
```

**2。数据属性**

在 Vue 2 中，我们能够将数据用作方法和对象。但是在 Vue 3 中，数据选项应该总是一个方法。

```
const app = Vue.createApp({
 template: “<div> {{ msg }} </div>”,
 data() {
    return { msg: “Hello World!” };
 },
});

app.mount(“#app”);
```

**3。注册全局组件和模块**

全局组件、指令和第三方模块现在应该用 *app* 挂载，而不是用 *Vue* 实例挂载。新的是我们可以指定我们用 *emit* 属性发出的方法，但是这是可选的。

在 Vue 2 中注册一个全局组件:

```
Vue.component(‘home-button’, {
 template: ‘<button @click=”incrementVal”>Increment</button>’,
 methods: {
   incrementVal() {
     this.$emit(‘increment’);
   },
 },
});
```

在 Vue 3 中注册一个全局组件:

```
const app = Vue.createApp(/* app config */);app.component(‘home-button’, {
 emits: ["increment"],
 template: ‘<button @click=”incrementVal”>Increment</button>’,
 methods: {
   incrementVal() {
     this.$emit(‘increment’);
   },
 },
});app.mount(“#app”);
```

**4。过渡类**

另一个小的更新是 Vue Transition 类的变化。

Vue 2 中的过渡类:

```
.v-enter,
.v-leave-to {
  opacity: 0;
}

.v-leave,
.v-enter-to {
  opacity: 1;
}
```

Vue 3 中的过渡类:

```
.v-enter-from,
.v-leave-to {
  opacity: 0;
}

.v-leave-from,
.v-enter-to {
  opacity: 1;
}
```

**5。Vue 路由器**

Vue 路由器的初始化和配置在 Vue 3 中已经更改。

在 Vue 2 中使用 Vue 路由器:

```
import VueRouter from 'vue-router';Vue.use(VueRouter);const router = new VueRouter({
    mode: 'history',
    routes: routes
 })new Vue({
  router: router,
  render: (h) => h(App),
}).$mount('#app');
```

在 Vue 3 中使用 Vue 路由器:

```
import { createRouter, createWebHistory } from 'vue-router';const router = createRouter({
  history: createWebHistory(),
  routes:routes
});const app = createApp(App);app.use(router);router.isReady().then(() => {
  app.mount('#app');
});
```

**6。路由器视图转换**

路由器视图过渡结构现在在 Vue 3 中有所不同。

Vue 2 中的路由器视图转换:

```
<transition name="route" mode="out-in">
      <router-view></router-view>
</transition>
```

Vue 3 中的路由器视图转换:

```
<router-view v-slot="slotProps">
      <transition name="route" mode="out-in">
        <component :is="slotProps.Component"></component>
      </transition>
</router-view>
```

7。安装 Vuex 存储器

安装 Vuex 商店在 Vue 3 中也有所不同。

在 Vue 2 中安装商店:

```
import Vuex from 'vuex';
Vue.use(Vuex);const store = new Vuex.Store({
  state() {
    return { };
  },
  mutations: { },
  actions: { },
  getters: { }
});new Vue({
  store: store,
  render: (h) => h(App),
}).$mount('#app');
```

在 Vue 3 中安装商店:

```
import { createStore } from 'vuex';const store = createStore({
  state() {
    return { };
  },
  mutations: { },
  actions: { },
  getters: { },
});const app = createApp(App)app.use(store);app.mount('#app');
```

## Vu 3 中的新功能

![](img/02ab940b3da4f87fb53eaab9fd9aec62.png)

**1。瞬间移动**

Teleport 提供了一种简单的方法来控制在 DOM 中的哪个父节点下呈现一段 HTML。

考虑这个 HTML 结构:

```
<div>
    <Modal/>
</div>
```

我们希望将这个`<Modal/>`放在`<body></body>`或其他元素中。传送来了:

```
<div>
  <teleport to="body">
    <Modal/>
  <teleport/>
</div>
```

您仍然可以进行交互并将道具传递给组件。

**2。碎片**

在 Vue 2 中，不支持多根组件，当用户无意中创建了多根组件时，会发出警告。因此，许多组件被封装在一个`<div>`中来修复这个错误。

```
<template>
  <div>
    <header>...</header>
    <main>...</main>
    <footer>...</footer>
  </div>
</template>
```

但是在 Vue 3 中，组件现在可以有多个根节点！然而，这确实需要开发人员明确定义属性应该分布在哪里。

```
<template>
  <header>...</header>
  <main>...</main>
  <footer>...</footer>
</template>
```

**结论**

Vue 3 速度快了 55%，内存使用率下降到 54%。这是通过使用 Typescript 完全重写 DOM 实现实现的。

如果你打算升级到 Vue 3，你应该聘请专家或[联系我](https://www.linkedin.com/in/engrmafzaalch)。

谢谢你。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)