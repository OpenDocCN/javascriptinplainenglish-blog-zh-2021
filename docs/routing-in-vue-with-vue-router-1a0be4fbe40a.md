# 使用 Vue 路由器在 Vue 中路由

> 原文：<https://javascript.plainenglish.io/routing-in-vue-with-vue-router-1a0be4fbe40a?source=collection_archive---------2----------------------->

![](img/d1f2ac6be47249b660856ff2b8f4e84a.png)

正如我在上一篇关于 React 中路由的文章中提到的，许多前端框架都是单页面应用程序。这意味着，由于每次用户在“页面”之间移动时，您不会向服务器发出 GET 请求，因此站点的 URL 不会自动更改。 [Vue Router](https://router.vuejs.org/) 可以让你为 Vue 应用程序做客户端路由，根据用户在页面上看到的内容改变 URL。

有几种方法可以将 Vue 路由器添加到 Vue 应用程序中。如果您正在下载 HTML 中带有`script`标签的 vue，您也可以为 Vue 路由器添加`script`:

```
<script src="/path/to/vue.js"></script>        // *for vue in general*
<script src="/path/to/vue-router.js"></script>   // *for vue-router*
```

您也可以使用 npm 将其安装到项目中，如下所示:

```
// ♥ > npm install vue-router
```

但是在这篇文章中，我将讨论如何在一个以 vue-cli 开始的项目中使用 vue-router。您可以使用以下命令安装或添加它:

```
// ♥ > vue add router
```

但是在运行这个命令时要小心，因为它将覆盖您的 *App.vue* 文件，所以要么在您开始工作之前计划添加 vue-router，要么在添加之前备份您的 *App.vue* 文件。这个命令是将 vue-router 添加到项目中的最简单的方法，但是它并没有真正解释当您运行这个命令时会发生什么，所以我将向您简要介绍添加的每一项内容，以及它所做的更改。

首先，它更改了几个文件，显然是 *App.vue* ，还有 *main.js* 。在 *main.js* 中，它从 react-router 导入`router`，并将其添加到应用程序的主 Vue 实例中，因此您可以在应用程序的顶层使用它。差异以粗体显示如下:

```
import Vue from 'vue'
import App from './App.vue'
**import router from './router'**

Vue.config.productionTip = false

new Vue({
  **router,**
  render: h => h(App),
 }).$mount('#app')
```

在 *App.vue* 中，它在`App`的模板中添加了一个名为`router-view`的东西，因此应用程序将在`App`组件中显示与 URL 中的路线相匹配的组件:

```
<template>
  <div id="app"> **<router-view/>**
  </div>
</template>
```

最后，它添加了名为*路由器*和*视图*的文件夹。在*视图的*文件夹中，它生成了一些基本的例子。vue 文件， *About.vue* 和 *Home.vue* ，因此您可以通过在不同页面之间导航来查看 vue 路由器的运行情况。 *router* 文件夹只有一个文件， *index.js* ，这里存放了你使用 vue-router 需要的大部分东西。该文件负责创建一个新的`VueRouter`,并将其导出用于应用程序的其余部分。您唯一需要注意的是路线列表，因为这是您将在应用程序中定义所有您想要的路线的地方。 *index.js* 文件如下所示:

```
import Vue from 'vue'
import VueRouter from 'vue-router'Vue.use(VueRouter)const routes = [
  // *this is where you put all your routes*
]const router = new VueRouter({
  mode: 'history',
  base: process.env.BASE_URL,
  routes
})export default router
```

定义路由有几种方法，但主要的方法是在文件顶部导入要使用的组件，并创建一个对象添加到路由列表中，如下所示:

```
const routes = [
  {
    path: '/',
    name: 'Home',
    component: Home
  },
  {
    path: '/about',
    name: 'About',
    component: About
  }
]
```

在页面上的这些路线之间导航的方式是使用`router-link` s。在`vue add router`对 *App.vue* 文件所做的更改中，他们在`router-view`上方添加了一个基本的导航栏，但我更喜欢让`NavBar`成为它自己的组件。要使用`router-link`，你只需要给每一个人传递一条路径就可以了:

```
<div id="nav">
  <router-link to="/">Home</router-link>
  <router-link to="/about">About</router-link>
</div>
```

但有时，您希望根据登录的用户或您正在查看的单个项目的 id 来选择不同的路径。这就是动态路由的用武之地。当定义路线路径时，动态部分由`:`表示。对于这个例子，假设我们有一个应用程序，可以让你看到书籍列表，当你点击一本书时，你可以转到单本书的页面。这条路线大概是这样的:

```
{
  path: '/books/:book_id',
  name: 'Book',
  component: Book
}
```

要在`router-link`中使用这个路径，您只需要向它传递一个动态路径。例如:

```
computed: {
  path: function () {
    return `/books/${this.book.id}`
  }
}
```

一旦进入 Book 组件，就可以通过使用`$route.params.id`来访问 route 中定义的 id。

使用 vue-router 时要考虑的一件事是，因为你不再引用你在`App`组件中使用的组件，你必须以不同的方式传递道具。如果您想让 vue-router 树中的某个组件访问`App`中的一些数据，那么您必须将它传递给`router-view`。这样，路由器中使用的任何组件都可以访问您从`App`传递的内容，只要您在需要使用它的组件中将它定义为一个 prop。

我要讲的最后一件事是以编程方式改变页面的路径。例如，一旦用户提交了表单，比如当他们登录时，您可能希望将他们重定向到不同的页面。方法是在表单提交时触发的事件中使用`$router.push()`。您应该将您希望用户重定向到的任何路径传递给`push`函数。

至此，我已经介绍了在 Vue 应用程序中使用 Vue 路由器的基础知识。确保在任何应用中都有良好的路由无疑是最佳实践。没有路线，用户就无法保存喜爱的页面，或者即使刷新应用程序也无法从同一个页面开始。如今，一个好的应用程序几乎需要一个导航栏来浏览应用程序。所以，每当你用 Vue 做项目的时候，添加 Vue 路由器让你的应用更容易访问是个好主意。