# 使用 Wouter 活动链接、尾随斜线和嵌套路径反应应用程序路由

> 原文：<https://javascript.plainenglish.io/react-app-routing-with-wouter-active-links-trailing-slash-and-nested-paths-d13856a930a?source=collection_archive---------14----------------------->

![](img/975f0081dd77e34b5799796ae1fc6ebb.png)

Photo by [Marty Southwell](https://unsplash.com/@martysouthwell?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Wouter 是一个库，允许我们根据 URL 加载 React 组件。

在本文中，我们将看看如何使用 Wouter 向 React 应用程序添加路由。

# 活动链接

我们可以通过检查从`useRoute`属性返回的`isActive`变量来设置活动链接。

例如，我们可以写:

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
};const ActiveLink = (props) => {
  const [isActive] = useRoute(props.href); return (
    <Link {...props}>
      <a className={isActive ? "active" : ""}>{props.children}</a>
    </Link>
  );
};export default function App() {
  return (
    <div>
      <style>
        {`.active {
            font-weight: bold
          }`}
      </style>
      <Router>
        <ActiveLink href="/users/foo">Users</ActiveLink>
        <ActiveLink href="/about">About</ActiveLink>
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

我们有`ActiveLink`组件，它用当前 URL 调用`useRoute`钩子，并返回一个带有`isActive`变量的数组。

`isActive`为`true`表示当前 URL 的链接处于活动状态。

# 尾随斜线

我们可以用自定义的 URL 匹配器让 Wouter 匹配一个带斜杠的路由。

例如，我们可以写:

```
import React from "react";
import { Route, Router } from "wouter";
import makeMatcher from "wouter/matcher";
import { pathToRegexp } from "path-to-regexp";const customMatcher = makeMatcher((path) => {
  let keys = [];
  const regexp = pathToRegexp(path, keys, { strict: true });
  return { keys, regexp };
});export default function App() {
  return (
    <div>
      <Router matcher={customMatcher}>
        <Route path="/foo">foo</Route>
        <Route path="/foo/">/foo/</Route>
      </Router>
    </div>
  );
}
```

我们用回调函数调用`makeMatcher`来返回一个对象，该对象的`strict`设置为`true`。

这将确保带结尾和不带结尾但其他方面相同的 URL 被视为不同。

# 嵌套路径

我们可以通过设置基本路径来添加嵌套路径。

例如，我们可以写:

```
import React from "react";
import { Link, Route, Router, useLocation, useRouter } from "wouter";const NestedRoutes = (props) => {
  const router = useRouter();
  const [parentLocation] = useLocation(); const nestedBase = `${router.base}${props.base}`;
  if (!parentLocation.startsWith(nestedBase)) return null; return (
    <Router base={nestedBase} key={nestedBase}>
      {props.children}
    </Router>
  );
};export default function App() {
  return (
    <div>
      <Router>
        <Route path="/about">about</Route>
        <NestedRoutes base="/dashboard">
          <Link to="/users" />
          <Route path="/users">users</Route>
        </NestedRoutes>
      </Router>
    </div>
  );
}
```

我们创建了使用`base`属性来设置基本路径的`NestedRoutes`组件。

在此基础上，我们通过组合`router.base`和`props.base`来创建基本路径，从而创建了`nestedBase`变量。

然后我们将`base`属性的值设置为`nestedBase`来设置嵌套路由的基本路径。

# 结论

我们可以检查哪个链接是活动的，添加尾部斜杠匹配，以及带有 Wouter 的嵌套路径。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)