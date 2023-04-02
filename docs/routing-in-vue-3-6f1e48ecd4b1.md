# Vue 3 中的路由

> 原文：<https://javascript.plainenglish.io/routing-in-vue-3-6f1e48ecd4b1?source=collection_archive---------9----------------------->

## 举例说明 Vue 3 中的路由

![](img/317431df75e940c660872b35ce19a302.png)

Photo by [Pakata Goh](https://unsplash.com/@pakata?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇文章中，我们将学习如何在 Vue 3 中处理路由。Vue 3 中的路由与我们在 Vue 2 中的路由略有不同。除此之外，大部分功能和我们处理卷轴、导航卫士等事情的方式保持不变。

我们将学到什么。

*   从头开始设置路由
*   命名路线
*   处理错误 404(未找到)页面
*   从 Vue CLI 安装

## **从零开始**

要安装 Vue 3，我们可以根据您的首选软件包管理器来完成

## Npm

```
 npm i -g @vue/cli 
```

## 故事

```
 yarn global add @vue/cli 
```

我们现在可以创建我们的 Vue 3 应用程序了。

在终端上运行以下命令

```
 vue create vue-routing 
```

请选择默认的 Vue 3 预览。

将使用文件夹 vue-routing 创建一个 Vue 3 应用程序

现在，我们将目录更改到文件夹中，并使用您最喜欢的文本编辑器打开它。

```
 cd routing-vue 
```

这将改变我们的目录到我们的应用程序文件夹

如果您使用可视代码，请运行命令

```
 code . 
```

该命令将使用 visual studio 打开应用程序文件夹。

## **安装 Vue 3 路由器**

vue 有 Vue 路由器包，处理 Vue 中的路由。为了将这个包安装到我们的应用程序中，我们运行下面的命令。

```
 npm i vue-router@next 
```

该命令将把 vue-router 安装到我们的 Vue 3 应用程序中。

## 设置路由

在我们的应用程序文件夹中，我们将创建一个路由器文件，并将其命名为 router.js

在这个文件中，我们将处理所有的应用程序路由功能。

```
 *import* { createWebHistory, createRouter } *from* ‘vue-router’;*import* Contact *from* ‘./components/Contact’;*import* Home *from* ‘./components/Home’;*import* Notfound *from* ‘./components/Notfound’;const routes = [{ path: ‘/’, name: “Home”, component: Home },{ path: ‘/contact’, name: “Contact”, component: Contact },{ path: ‘/:catchAll(.*)’, name: “Notfound”, component: Notfound }];const router = createRouter({history: createWebHistory(),routes*// shorthand routes:routes*});*export* *default* router; 
```

从 vue-router 我们将需要两个重要的功能，即创建网页历史和创建路由器。

**createWebHistory** —将路由模式设置为历史。

创建路由器 —创建我们的路由器

然后，我们可以创建路由器，它将是一个对象数组。在对象中，我们需要指定可选的路径、组件和名称。

**路径** —将指定我们想要直接到达的路径。例如，'/contact '将指向 localhost:8080/contact。

**组件** —当路径中指定的路线匹配时，这将是我们想要呈现的组件。

**名称** —这是可选的，但是我们可以在组件匹配相同组件的情况下使用它。

设置路线后，我们可以继续设置路线功能。

```
 const router = createRouter({history: createWebHistory(),routes*// shorthand routes:routes*}); 
```

我们设置 history 来创建 WebHistory()。之前，我们可以设置模式:历史。

我们现在可以设置路线，这是路线的简写:路线

## 处理 404 未找到的路线

要在我们的路由中设置 404 未找到的页面，我们可以设置路径来捕捉所有未找到的页面。

为此，我们设置如下所示的路径。

```
 { path: ‘/:catchAll(.*)’, name: “Notfound”, component: Notfound } 
```

这也适用于动态创建的页面。

现在我们已经设置了路由功能。记得导出路由器。

## 让应用程序使用 Vue 路由器

现在，在 main.js 文件中，我们将导入路由器文件，并在 createApp 中使用它。

我们可以将我们的应用程序流划分如下。

```
 *import* { createApp } *from* ‘vue’*import* App *from* ‘./App.vue’*import* router *from* ‘./routes.js’const app = createApp(App)*//tell app to use router file before we mount*app.use(router)app.mount(‘#app’)const app = createApp(App)//tell app to use router file before we mountapp.use(router)app.mount(‘#app’) 
```

我们可以类似地将这些链接在一起，如下所示。

```
 *import* { createApp } *from* ‘vue’*import* App *from* ‘./App.vue’*import* router *from* ‘./routes.js’createApp(App).use(router).mount(‘#app’) 
```

现在，在我们的 app.vue 文件中，我们可以设置我们希望应用程序在哪里呈现组件。

这是我们通常使用的

```
 <router-view></router-view> 
```

为了提供在应用程序中导航的链接，我们使用。

请注意，我们还提供了一个 to，这将指定用户将被定向到的 URL。

```
 <router-link to=”/contact”>Contact</router-link> 
```

## **从 Vue CLI 安装**

我们也可以在应用程序中启用 Vue 路由，而无需处理很多事情。

在使用 Vue CLI 创建应用程序期间，在项目创建期间提供的提示上选择 vue-router，Vue 将为我们完成所有路由功能。

几乎和我们做过的差不多。

## 更多阅读

[](https://medium.com/javascript-in-plain-english/a-deep-dive-into-the-vue3-composition-api-dece990fc846) [## 深入探究 Vue3 组合 API

### 通过示例深入研究 vue 组合 API。

medium.com](https://medium.com/javascript-in-plain-english/a-deep-dive-into-the-vue3-composition-api-dece990fc846) 

## 结论

我们所学内容的回顾:

*   从头开始设置路由
*   命名路线
*   处理错误 404(未找到)页面
*   从 Vue CLI 安装

谢谢你坚持到现在。我希望你已经了解了一些关于 Vue 3 中路由的知识。

如果你觉得这篇文章有帮助，请不要犹豫，与他人分享。