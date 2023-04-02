# 如何在 Nuxt.js 中创建自定义错误页面

> 原文：<https://javascript.plainenglish.io/how-to-create-custom-error-pages-in-nuxt-js-3c8192bc0ae5?source=collection_archive---------6----------------------->

## 在 Nuxt.js 中创建自定义错误页面，用例子解释。

![](img/7b89cf8852bc2c3685853aa2cd0254d8.png)

Image by [Wallpaper Cave](https://www.google.com/url?sa=i&url=https%3A%2F%2Fwallpapercave.com%2Fvuejs-wallpapers&psig=AOvVaw1CfFE7si_DT74OauCC-nMj&ust=1625503004734000&source=images&cd=vfe&ved=0CAsQjhxqFwoTCPjJ6OrsyfECFQAAAAAdAAAAABAD)

Nuxt.js 是一个 Vue.js 框架，附带了许多捆绑在一起的特性。开箱即用，我们可以在服务器端呈现的站点和静态站点之间进行选择。

为现代前端应用开发应用时，Nuxt.js 有很多超能力。好了，关于 Nuxt.js 已经说得够多了。现在，让我们进入主题，看看如何在 Nuxt.js 中创建自定义错误页面。

就像我们上面说过的，Nuxt.js 有很多特性，其中一个特性是访问未配置的页面和组件时的错误处理。

就像任何其他默认错误处理配置一样，我们可能会被迫在某个时间点为我们的应用程序上未配置的页面和其他错误定制创建我们的定制错误处理页面。

要创建自定义错误页面，请导航到 Nuxt.js 应用程序根目录下的 layouts 目录。

创建一个文件，命名为 **error.vue** 。

**注意**:用 **error.vue** 以外的名字创建的文件不会被 Nuxt.js 拾取来显示自定义错误页面。

创建文件后，现在您可以进入文件内部，并根据您想要的设置来设置样式。但是在你这样做之前，我们需要配置一些东西，以便于用 Nuxt.js 识别。

您应该设置 **error.vue** 文件，如下面的代码片段所示。

```
<template><div><div<h1 class=”font-mono text-white z-50 text-6xl”>{{ error.statusCode }} It Seems you are lost?</h1><nuxt-linkto=”/”>Take Me Home</nuxt-link></div></template><script>*export* *default* {props: [“error”],layout: “error”,};</script><style scopped></style>
```

现在，如果您尝试转到一个尚未在 Nuxt.js 应用程序中配置的路由，您将被定向到我们创建的页面。

感谢您将这篇文章看完。我希望它对你有所帮助，如果你有，请不要犹豫，分享它。

## **更多阅读:**

[](/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99) [## JavaScript 算法和数据结构挑战——Fizz Buzz

### JavaScript 中的 Fizz Buzz challenge 黑客团队的一个编程挑战的解决方案。

javascript.plainenglish.io](/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99) [](/all-you-need-to-know-about-javascript-object-notation-json-a3290231019a) [## 关于 JavaScript 对象表示法(JSON ),您需要知道的是

### 了解关于 JSON 的一切

javascript.plainenglish.io](/all-you-need-to-know-about-javascript-object-notation-json-a3290231019a) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)