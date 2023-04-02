# 如何用 React 路由器版本 5 添加嵌套路由？

> 原文：<https://javascript.plainenglish.io/how-to-add-nested-routes-with-react-router-version-5-20c711bcc943?source=collection_archive---------13----------------------->

![](img/6635d021336d51134822361aff74398f.png)

Photo by [Anna Sjöblom](https://unsplash.com/@sjobloma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们使用 React 创建我们的 JavaScript 应用程序，我们可能会添加一个路由解决方案，以便我们可以在访问不同的 URL 时呈现不同的组件。

React Router 是一个流行的路由库，用于此目的。

在本文中，我们将了解如何使用 React 路由器版本 5 添加嵌套路由。

# 使用 React 路由器版本 5 添加嵌套路由

我们可以在传递给`render`属性的函数中嵌套`Route`组件，从而在 React 路由器版本中嵌套路由。

为此，我们写道:

```
import React from "react";
import { BrowserRouter, Route, Link } from "react-router-dom";const FrontPage = () => <p>front page</p>;
const HomePage = () => <p>home page</p>;
const AboutPage = () => <p>about page</p>;
const Backend = () => <p>back end</p>;
const Dashboard = () => <p>dashboard</p>;
const UserPage = () => <p>user page</p>;export default function App() {
  return (
    <div>
      <BrowserRouter>
        <Link to="/">front page</Link>
        <Link to="/home">home page</Link>
        <Link to="/about">about page</Link>
        <Link to="/admin">back end</Link>
        <Link to="/admin/home">dashboard</Link>
        <Link to="/admin/users">user page</Link>
        <Route path="/" component={FrontPage} exact />
        <Route path="/home" component={HomePage} />
        <Route path="/about" component={AboutPage} /> <Route
          path="/admin"
          render={({ match: { url } }) => (
            <>
              <Route path={`${url}/`} component={Backend} exact />
              <Route path={`${url}/home`} component={Dashboard} />
              <Route path={`${url}/users`} component={UserPage} />
            </>
          )}
        />
      </BrowserRouter>
    </div>
  );
}
```

我们有`FrontPage`、`HomePage`、`AboutPage`、`Backend`、`Dashboard`和`UserPage`路由组件。

我们在定义路线时会用到。

然后在`App`中，我们添加了`BrowserRouter`组件，这样我们就可以在其中添加路线。

我们添加带有`to`属性的`Link`组件来添加到给定路线的链接。

然后我们添加`Route`组件，将 URL 路径映射到传递给`component`属性的组件。

`path`道具让我们设置路线的路径。

`exact`让我们仅在精确路径匹配时加载组件。

当我们转到给定的 URL 路径时，就会加载给定的组件。

最后一个`Route`组件将`path`设置为`'/admin'`，这是 URL 路径的第一部分。

`render`属性被设置为一个函数，该函数接受一个具有`match.url`属性的对象。

我们从对象中析构它，然后将它们传递给我们在函数中返回的`Route`组件。

这让我们用从`/admin`开始的路径映射到给定的组件。

因此，当我们转到`/admin`时，我们会看到显示的`Backend`组件。

如果我们转到`/admin/home`，我们会看到`Dashboard`组件被渲染。

如果我们转到`/admin/users`，我们会看到`UserPage`组件被渲染。

因此，当我们单击链接时，我们会看到每个组件显示的内容。

# 结论

我们可以通过嵌套的`Route`组件轻松地添加 React Router 5 的嵌套路由。