# Vue 3 中的异步组件加载

> 原文：<https://javascript.plainenglish.io/asynchronous-component-loading-in-vue-3-f8cd0860da23?source=collection_archive---------12----------------------->

## 使用 defineAsyncComponent 在 Vue 3 中异步加载

![](img/4881830328b14c92a11383f74db71cc2.png)

Photo by [Alex Kulikov](https://unsplash.com/@burntime?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue3 即将推出令人惊叹的功能。Vue 3 附带了一个延迟加载特性。

我们可以利用这一惊人的特性来提高我们的 vue 应用和优化的性能。

为了异步加载组件，我们将从静态导入转移到异步语法。

用静态导入语句加载的同步组件将被添加到现有的应用程序包中。

如果不使用代码分割，那么应用程序核心会变得更大，影响我们应用程序的整体性能。

为了在 vue3 中异步加载组件，我们需要首先从 vue 导入一个 defineAsyncComponent，它将负责异步加载组件。

举个例子，我们想要异步加载一个名为 *Profile.vue* 的组件

为了延迟加载组件，我们将首先从 vue 导入 defineAsyncComponent，如下所示

```
import {defineAsyncComponent} from “vue”
```

导入它将使 defineAsyncComponent 在我们的组件中可用。

然后，我们可以如下继续并延迟加载组件

```
const Profile = defineAsyncComponent (()=> import(“@/components/Profile))
```

这将把组件加载到一个单独的块中。

如果您现在导航到 network 选项卡，您可以看到我们的配置文件组件现在被加载到一个单独的块中。

我们如何识别大块？

Webpack 附带了一个神奇的注释，我们可以利用这个神奇的注释给我们的组件块命名。

```
const Profile = defineAsyncComponent (()=> import(/* webpackChunkName: “profile” */“@/components/Profile))
```

如果您现在导航到 network 选项卡，您将看到我们的块已经被提供了一个名称 profile。如果没有提供，webpack 将自动为块生成一个名称。

我们可以更进一步，为可能需要一段时间才能完全加载的组件创建自定义加载消息。

对于可能需要大量时间才能完全呈现到页面中的组件，将显示此加载消息。

我们还可以包括时间延迟。

要显示自定义加载消息，我们需要执行以下操作。

```
const Profile = defineAsyncComponent (loader: ()=> import(/* webpackChunkName: “profile” */“@/components/Profile),loadingComponent: Loading,delay:200)
```

使用 vue 暂停边界时，您可以指定 suspentible:false 以防止暂停显示暂停错误边界。

我还写了一篇关于 vue2 中组件异步加载的文章，你也可以看看。

## **结论**

简单回顾一下，我们已经看到了如何使用 defineAsyncComponent 在 vue3 中异步导入组件，以及它如何提高 vue 应用程序的性能和优化。

谢谢你把这篇文章读到这里。如果你觉得这篇文章有帮助，请不要犹豫，分享出来。