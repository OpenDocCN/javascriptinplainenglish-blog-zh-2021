# Nuxt.js 入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-nuxt-js-39bcf11c7d4e?source=collection_archive---------9----------------------->

![](img/3ee6a8f2caef9bde5aa426cc5dd989a6.png)

Photo by [Myfanwy Owen](https://unsplash.com/@myfanwyo22?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Nuxt.js 是一个基于 Vue.js 的应用框架。

我们可以用它来创建服务器端渲染应用和静态站点。

在本文中，我们将了解如何开始使用 Nuxt.js。

# 装置

我们可以用`create-nuxt-app`程序创建我们的 Nuxt 应用程序。

为此，我们运行:

```
npx create-nuxt-app <project-name>
```

或者:

```
yarn create nuxt-app <project-name>
```

然后我们运行:

```
npm run dev
```

运行我们的应用程序。

# 目录结构

Nuxt 应用程序的目录结构遵循一些约定。

将`assets`文件夹作为静态资产，如样式、图像和字体。

`layouts`文件夹包含布局组件，用于在页面上布局内容。

`middlewares`文件夹有应用中间件。

中间件让我们定义可以在渲染之前运行的自定义函数。

`pages`文件夹里有视图和路线。

它应该只包含`.vue`文件。

如果不更改我们应用的配置，将无法重命名该文件夹。

`plugins`文件夹中有我们希望在实例化根 Vue 实例之前运行的 JavaScript 插件。

文件夹直接向公众提供静态文件。

`nuxt.config.js`具有 Nuxt.js 自定义配置。

# 按指定路线发送

Nuxt 通过遵循`pages`文件夹的结构自动进行布线。

例如，我们可以创建`pages/hello.vue`文件:

```
<template>
  <div class="container">hello world</div>
</template><script>
export default {};
</script>
```

然后当我们去[http://localhost:3000/hello](http://localhost:3000/hello)时，我们看到显示‘hello world’。

如果我们想在页面中接受 URL 参数，我们在文件名前添加一个`_`。

例如，我们创建一个`pages/users/_id.vue`文件，并编写:

```
<template>
  <div class="container">{{$route.params.id}}</div>
</template><script>
export default {};
</script>
```

我们从`$route.params`对象中获取 URL 参数。

我们可以用`validate`方法验证路线参数。

为了补充它，我们写道:

```
<template>
  <div class="container">{{$route.params.id}}</div>
</template><script>
export default {
  validate({ params }) {
    return /^\d+$/.test(params.id);
  },
};
</script>
```

我们添加了带有一个对象的`validate`方法，该对象的属性是`params`属性。

然后我们可以返回条件进行验证。

此外，我们可以添加一个`_.vue`文件来处理不匹配任何其他 URL 的 URL。

# 命名视图

我们可以在布局或页面中使用`<nuxt name="top"/>`或`<nuxt-child name="top"/>`来添加命名视图。

# 视图

视图定义了页面的各个部分。

Nuxt 页面的默认模板是:

```
<!DOCTYPE html>
<html {{ HTML_ATTRS }}>
  <head {{ HEAD_ATTRS }}>
    {{ HEAD }}
  </head>
  <body {{ BODY_ATTRS }}>
    {{ APP }}
  </body>
</html>
```

# 默认布局

我们可以通过编辑`layouts/default.vue`文件来改变默认布局。

默认情况下，它具有:

```
<template>
  <div>
    <Nuxt />
  </div>
</template>
```

来呈现页面。

# 自定义布局

此外，我们还可以添加自定义布局。

例如，我们可以创建一个`layouts/blog.vue`文件并写入:

```
<template>
  <div>
    <div>My blog</div>
    <Nuxt />
  </div>
</template>
```

显示标题和用于显示页面内容的`Nuxt`组件。

然后使用布局，我们可以在`pages`文件夹中创建一个名为`pages/post.vue`的文件，并添加:

```
<template>
  <div>hello world</div>
</template><script>
export default {
  layout: "blog",
};
</script>
```

我们设置了`layout`属性，以便可以选择我们想要使用的布局。

现在我们应该看到“你好世界”上方的“我的博客”标题。

# 结论

我们可以使用 Nuxt.js 创建简单的服务器端渲染应用程序。

它基于 Vue.js。

喜欢这篇文章吗？如果是这样，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**