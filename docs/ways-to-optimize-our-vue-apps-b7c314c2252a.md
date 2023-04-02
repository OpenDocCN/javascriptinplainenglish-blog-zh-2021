# 优化我们 Vue 应用的方法

> 原文：<https://javascript.plainenglish.io/ways-to-optimize-our-vue-apps-b7c314c2252a?source=collection_archive---------21----------------------->

![](img/91af8ca0eaf7c9f8a06cb962f6fdf7d5.png)

Photo by [Mael BALLAND](https://unsplash.com/@mael_bld?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们开发的应用程序加载速度更快，用户会更开心。

这可以通过 Vue 应用的一些技巧来实现。

在这篇文章中，我们将看看我们可以做些什么来加快我们的 Vue 应用程序。

# 惰性加载路由组件

我们可以让我们的 Vue 路由组件仅在需要时加载。

为此，我们可以使用 JavaScript `import`函数来导入 ou 组件。

例如，我们可以写:

```
import Vue from 'vue'
import Router from 'vue-router'const Home = () => import('./routes/Home.vue');
const Settings = () => import('./routes/Settings.vue');Vue.use(Router)export default new Router({
  routes: [
    { path: '/', component: Home },
    { path: '/settings', component: Settings }
  ]
})
```

我们有通过`import`函数返回组件模块承诺的函数。

因为它不是在构建时导入的，所以只有在需要的时候才会被加载。

用户必须在开始时下载较少的代码，这样加载速度会更快。

这些块可以通过添加`webpackChunkName`评论来控制。

例如，我们可以写:

```
const Profile = () => import(/* webpackChunkName: "profile" */'./routes/Profile.vue');
const ProfileSettings = () => import(/* webpackChunkName: "profile" */'./routes/ProfileSettings.vue');
```

我们将`profile`块与`webpackChunkName`评论捆绑在一起。

# 尽量减少外部库的使用

减少库的数量也会减少包的大小，所以我们的应用程序的加载速度也会更快。

我们可以用 JavaScript 的标准库做很多事情。

例如，我们可以使用原生数组方法来代替 Lodash 的数组方法。

# 压缩和优化图像

图像可以压缩很多，所以我们应该这样做，以减少加载时间。

此外，我们可以从 CDN 加载图像，这样我们就可以从高容量服务器提供这些图像。

# 延迟加载图像

延迟加载图片意味着我们只在需要看的时候才加载它们。

这可以通过`vue-lazyload`封装轻松实现。

要安装它，我们运行:

```
npm i vue-lazyload
```

然后在`main.js`中，我们添加:

```
import Vue from 'vue'
import VueLazyload from 'vue-lazyload'Vue.use(VueLazyload)
```

注册插件。

然后我们可以加上:

```
<img v-lazy="image.src" >
```

来使用它。该插件提供了`v-lazy`指令。

# 在我们的应用中重用功能

重用功能使我们的应用程序更容易改变，因为我们只需要改变一个地方。

此外，我们编写的代码更少，因此捆绑包也更小。

因此，对于用户来说，编写速度更快，加载速度更快。

例如，使用`VueNotifications`库，我们可以编写:

```
import VueNotifications from 'vue-notifications'
import miniToastr from 'mini-toastr'miniToastr.init()function toast ({title, message, type, timeout, cb}) {
  return miniToastr[type](message, title, timeout, cb)
}const options = {
  success: toast,
  error: toast,
  info: toast,
  warn: toast
}Vue.use(VueNotifications, options)
```

创建一个`toast`函数，然后用它来显示各种祝酒词。

是一个小的通知库，我们可以用它来显示通知。

# 结论

我们可以通过一些简单的技巧轻松优化 Vue 应用的速度。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**