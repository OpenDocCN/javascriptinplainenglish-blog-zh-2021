# 使用 React Query-GET 请求发出 HTTP 请求

> 原文：<https://javascript.plainenglish.io/making-http-requests-with-react-query-get-requests-b4569b1c131e?source=collection_archive---------11----------------------->

![](img/2192d82bba01e697c8b3fb9dcfd7abbf.png)

Photo by [Sangga Rima Roman Selia](https://unsplash.com/@sxy_selia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 查询库让我们可以在 React 应用程序中轻松地发出 HTTP 请求。

在本文中，我们将了解如何使用 React Query 发出 HTTP 请求。

# 使用 useQuery 挂钩获取请求

为了发出 GET 请求，我们使用 React Query 提供的`useQuery`钩子。

例如，我们可以写:

`index.js`

```
import { StrictMode } from "react";
import ReactDOM from "react-dom";
import { QueryClient, QueryClientProvider } from "react-query";
import App from "./App";const queryClient = new QueryClient();const rootElement = document.getElementById("root");
ReactDOM.render(
  <QueryClientProvider client={queryClient}>
    <StrictMode>
      <App />
    </StrictMode>
  </QueryClientProvider>,
  rootElement
);
```

`App.js`

```
import axios from "axios";
import React from "react";
import { useQuery } from "react-query";export default function App() {
  const { isLoading, isError, data, error } = useQuery("yesNo", () =>
    axios("https://yesno.wtf/api")
  ); if (isLoading) {
    return <span>Loading...</span>;
  } if (isError) {
    return <span>Error: {error.message}</span>;
  } return <div>{JSON.stringify(data)}</div>;
}
```

我们用`QueryClientProvider`高阶组件包装我们的`App`，让我们使用 React Query 提供的钩子来发出 HTTP 请求。

然后在`App`中，我们调用`useQuery`，将请求的标识符作为第一个参数。

第二个参数具有发出 HTTP 请求的函数。

它应该返回一个带有响应数据的承诺。

钩子返回一个具有各种属性的对象。

`isLoading`是请求加载时的`true`。

当请求有错误时`isError`为`true`。

`data`有响应数据。

`error`有错误内容。

我们可以用`status`属性替换布尔属性。

例如，我们可以写:

```
import axios from "axios";
import React from "react";
import { useQuery } from "react-query";export default function App() {
  const { status, data, error } = useQuery("yesNo", () =>
    axios("https://yesno.wtf/api")
  ); if (status === "loading") {
    return <span>Loading...</span>;
  } if (status === "error") {
    return <span>Error: {error.message}</span>;
  } return <div>{JSON.stringify(data)}</div>;
}
```

如果`status`为`'loading'`，则请求正在加载。

如果`status`为`'error'`，则请求有错误。

# 查询关键字

查询键是`useQuery`的第一个参数。

它唯一地标识了正在进行的请求。

我们可以像上面的例子一样传入一个字符串。

但是如果我们需要传入更多的信息来识别请求，我们也可以传入数组键。

例如，我们可以写:

```
import axios from "axios";
import React from "react";
import { useQuery } from "react-query";export default function App() {
  const { status, data, error } = useQuery(
    ["todo", 5],
    ({ queryKey: [, id] }) => {
      return axios(`https://jsonplaceholder.typicode.com/posts/${id}`);
    }
  ); if (status === "loading") {
    return <span>Loading...</span>;
  } if (status === "error") {
    return <span>Error: {error.message}</span>;
  } return <div>{JSON.stringify(data)}</div>;
}
```

用数组键调用`useQuery`。

我们可以用第二个参数的回调中的参数的`queryKey`属性来获取密钥的内容。

我们从数组的第二个条目中获取`id`，就像我们传递它们一样。

# 结论

我们可以在 React 应用程序中使用 React Query 轻松地发出 GET 请求。

*更多内容请看*[***plain English . io***](http://plainenglish.io)