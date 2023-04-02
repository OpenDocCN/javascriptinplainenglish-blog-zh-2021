# 如何使用 React 路由器创建公共和私有路由

> 原文：<https://javascript.plainenglish.io/how-to-create-public-and-private-routes-using-react-router-54ca2b3f2870?source=collection_archive---------1----------------------->

使用 React 路由器在 React 应用程序中编写公共和私有路由的步骤

![](img/15185055c1d056e77a2f30670e527952.png)

Photo by [Bram Naus](https://unsplash.com/@bramnaus?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/internet?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在开发带身份验证的 React 应用程序时，我们可能需要公共和私有路由。我们先来看看它们是什么。

# 公共路线

公共路由有登录、注册、忘记密码、重置密码。简单来说，这些路线都可以在登录 app 前访问。

# 私人路线

私人路线因应用程序而异，例如仪表板、用户资料、应用程序设置、主页等。简单来说，这些路由只有登录后才能访问。

公共和私有路由的约束条件是，公共路由在登录后不应被访问，私有路由在登录前不应被访问。

在本文中，我们将看到这是如何实现的——如何使用 [react-router](https://reactrouter.com/web/guides/quick-start) 为您的 react 应用程序创建公共和私有路由。我们开始吧

# 公共路线

首先，让我们创建一个`PublicRoute.js`组件来处理公共路线情况，如下所示

从上面的代码中可以看到，公共路由组件接收了 3 个道具，如`children`、`isAuthenticated`和`…rest`。如果用户通过了身份验证，他将被重定向到主屏幕，如果他没有通过身份验证(登录)，他只能访问公共路由。

# 私人路线

私有路由组件类似于公共路由，唯一的变化是重定向 URL 和身份验证条件。如果用户未通过身份验证，他将被重定向到登录页面，并且只有通过身份验证(登录)后，用户才能访问通过身份验证的路由。

# 受保护的路线

受保护的路由组件用于映射所有已验证的路由，如下所示

在 routes.js 中，已验证的路由定义如下

# 集成路线

现在，让我们将路由组件集成到 App.js 中，如下所示

这里，我们用`<PublicRoute />` 组件包装了非认证路由，用`<PrivateRoute />`组件包装了认证路由。我们已经使用了**悬念**来增加组件的延迟加载。

现在我们已经配置了私有和公有路由。如果不匹配，将呈现`<NoFoundComponent />`。

# 结论

公共和私有路由也将限制在注销后使用浏览器后退按钮访问以前访问过的路由。我希望你已经发现这是有用的。感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)