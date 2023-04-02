# 使用 Wouter 对应用程序路由做出反应—路由更改、开关和链接

> 原文：<https://javascript.plainenglish.io/react-app-routing-with-wouter-route-changes-switches-and-links-4ea147eda432?source=collection_archive---------17----------------------->

![](img/ede728b6bb904004e2c1da1b4d610ef4.png)

Photo by [Hanson Lu](https://unsplash.com/@hansonluu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Wouter 是一个库，允许我们根据 URL 加载 React 组件。

在本文中，我们将看看如何使用 Wouter 向 React 应用程序添加路由。

# 用用户路由器观察路由器变化

我们可以使用`useRouter`钩子来观察`router`对象的变化。

例如，我们写道:

```
import React, { useEffect } from "react";
import { Link, Route, Router, useRouter } from "wouter";const InboxPage = () => {
  return (
    <div>
      <p>inbox</p>
    </div>
  );
};export default function App() {
  const router = useRouter(); useEffect(() => {
    console.log(router);
  }, [router]); return (
    <div>
      <Link href="/inbox">
        <a>Inbox</a>
      </Link>
      <Router>
        <Route path="/about">
          <p>About Us</p>
        </Route>
        <Route path="/users/:name">
          {(params) => <div>Hello, {params.name}!</div>}
        </Route>
        <Route path="/inbox" component={InboxPage} />
      </Router>
    </div>
  );
}
```

我们使用`useEffect`钩子来观察`router`的变化。

`router`有`hook`属性，默认是`useLocation`钩子。

此外，我们可以向`router`对象添加我们自己的属性，以便在路由之间传递数据

# `Route Component`

我们可以使用`Route`组件来定义路线。

例如，我们写道:

```
import React, { useEffect } from "react";
import { Link, Route, Router, useRouter } from "wouter";const InboxPage = () => {
  return (
    <div>
      <p>inbox</p>
    </div>
  );
};export default function App() {
  return (
    <div>
      <Link href="/inbox">
        <a>Inbox</a>
      </Link>
      <Router>
        <Route path="/about">
          <p>About Us</p>
        </Route>
        <Route path="/users/:name">
          {(params) => <div>Hello, {params.name}!</div>}
        </Route>
        <Route path="/inbox" component={InboxPage} />
      </Router>
    </div>
  );
}
```

我们添加`Route`组件并设置`path`属性来定义路线。

`:name`是一个 URL 参数占位符。

我们可以从`params`参数中得到它的值。

# 链接组件

`Link`组件允许我们添加链接，以便导航到不同的页面。

例如，我们写道:

```
import React, { useEffect } from "react";
import { Link, Route, Router, useRouter } from "wouter";const InboxPage = () => {
  return (
    <div>
      <p>inbox</p>
    </div>
  );
};export default function App() {
  return (
    <div>
      <Link href="/about">
        <a>About</a>
      </Link>
      <Router>
        <Route path="/about">
          <p>About Us</p>
        </Route>
        <Route path="/users/:name">
          {(params) => <div>Hello, {params.name}!</div>}
        </Route>
        <Route path="/inbox" component={InboxPage} />
      </Router>
    </div>
  );
}
```

添加一个链接，当我们单击它时可以转到“关于”页面。

# `Switch Component`

`Switch`组件允许我们将独占路由添加到 React 应用程序中。

它确保一次只渲染一条路线。

例如，我们写道:

```
import React from "react";
import { Link, Route, Switch } from "wouter";const AllOrders = () => {
  return (
    <div>
      <p>all orders</p>
    </div>
  );
};const Orders = ({ params }) => {
  return (
    <div>
      <p>orders {params.status}</p>
    </div>
  );
};export default function App() {
  return (
    <div>
      <Link href="/orders/all">
        <a>All</a>
      </Link>
      <Switch>
        <Route path="/orders/all" component={AllOrders} />
        <Route path="/orders/:status" component={Orders} />
      </Switch>
    </div>
  );
}
```

我们将`Route`组件放在一个`Switch`中，这样我们只有`AllOrders`或`Orders`组件，而不会两者都放在一起。

在`Orders`中，我们从`params`道具中获取 URL 参数。

# 结论

我们可以添加专用路线，并在我们的 React 应用程序中使用 Wouter 观察路由器的变化。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)