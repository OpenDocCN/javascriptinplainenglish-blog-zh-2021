# 对应用路由和 Wouter 做出反应-重定向、默认路由和基本路径

> 原文：<https://javascript.plainenglish.io/react-app-routing-with-wouter-redirect-default-route-and-base-path-3198d436e25a?source=collection_archive---------12----------------------->

![](img/7608ccf3a90dc2c2dbf5175be4fc8b47.png)

Photo by [Lisa Fotios](https://unsplash.com/@fotios_photos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Wouter 是一个库，允许我们根据 URL 加载 React 组件。

在本文中，我们将了解如何使用 Wouter 向 React 应用程序添加路由。

# `Redirect`

我们可以通过`setLocation`功能重定向到另一个路由组件。

例如，我们可以写:

```
import React from "react";
import { Route, Router, useLocation } from "wouter";const InboxPage = () => {
  return (
    <div>
      <p>inbox</p>
    </div>
  );
};
export default function App() {
  const [, setLocation] = useLocation(); return (
    <div>
      <a href="#" onClick={() => setLocation("/about")}>
        About
      </a>
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

我们调用`useLocation`钩子返回`setLocation`功能。

然后，我们在`onClick`处理程序中调用它，以转到`/about`路线。

# 匹配动态段

我们可以使用`useRoute`钩来匹配动态路由段。

例如，我们写道:

```
import React from "react";
import { Link, Route, Router, useRoute } from "wouter";const InboxPage = () => {
  return (
    <div>
      <p>inbox</p>
    </div>
  );
};const UserPage = () => {
  const [, params] = useRoute("/users/:name");
  return <div>Hello, {params.name}!</div>;
};export default function App() {
  return (
    <div>
      <Router>
        <Link href="/users/foo">Users</Link>
        <Route path="/about">
          <p>About Us</p>
        </Route>
        <Route path="/users/:name" component={UserPage}></Route>
        <Route path="/inbox" component={InboxPage} />
      </Router>
    </div>
  );
}
```

在`UserPage`中，我们用路由模式调用`useroute`钩子，从`params`ojet 中获取`name`参数。

在`Route`的`path`道具中，我们有`:name`占位符来添加占位符。

我们也可以匹配`/foo?/:bar*`模式来添加通配符`bar`占位符。

`/foo/baz?`有可选的`baz`占位符。

并且`/foo/bar+``bar`为一段或多段也支持匹配。

# 基本路径

我们可以用`Router`组件的`base`道具添加一条基本路径。

例如，我们写道:

```
import React from "react";
import { Link, Route, Router, useRoute } from "wouter";const InboxPage = () => {
  return (
    <div>
      <p>inbox</p>
    </div>
  );
};const UserPage = () => {
  const [, params] = useRoute("/users/:name");
  return <div>Hello, {params.name}!</div>;
};export default function App() {
  return (
    <div>
      <Router base="/app">
        <Link href="/users/foo">Users</Link>
        <Route path="/about">
          <p>About Us</p>
        </Route>
        <Route path="/users/:name" component={UserPage}></Route>
        <Route path="/inbox" component={InboxPage} />
      </Router>
    </div>
  );
}
```

将基本路径设置为`/app`。

# 默认路由

我们可以通过添加`Route`组件来添加默认路线，而不需要添加`path`道具。

例如，我们写道:

```
import React from "react";
import { Route, Switch } from "wouter";export default function App() {
  return (
    <div>
      <Switch>
        <Route path="/about">
          <p>About Us</p>
        </Route>
        <Route>Not Found</Route>
      </Switch>
    </div>
  );
}
```

添加`Not Found`路线。

默认路由应该总是最后一个，所以在显示未找到的路由之前可以检查其他模式。

# 结论

我们可以添加重定向，匹配动态路由段，设置基本路径，并在我们的反应应用程序中添加默认路由。

*多内容见于* [***中***](https://plainenglish.io/)