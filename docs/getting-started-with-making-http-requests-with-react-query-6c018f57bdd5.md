# 开始使用 React Query 发出 HTTP 请求

> 原文：<https://javascript.plainenglish.io/getting-started-with-making-http-requests-with-react-query-6c018f57bdd5?source=collection_archive---------15----------------------->

![](img/bbb0d679b79259a8ea7d51e8c9c1df7d.png)

Photo by [Hermes Rivera](https://unsplash.com/@hermez777?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 查询库让我们可以在 React 应用程序中轻松地发出 HTTP 请求。

在本文中，我们将了解如何使用 React Query 发出 HTTP 请求。

# 装置

我们可以通过运行以下命令来安装该库:

```
npm i react-query
```

或者:

```
yarn add react-query
```

我们还安装了 Axios HTTP 客户端库，让请求变得更容易。

为此，我们运行:

```
npm i axios
```

# 入门指南

然后，我们可以通过编写以下代码使用 API 进行查询:

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
  const { isLoading, error, data } = useQuery("yesNo", () =>
    axios("https://yesno.wtf/api")
  ); if (isLoading) return "Loading..."; if (error) return "An error has occurred: " + error.message; return <div>{JSON.stringify(data)}</div>;
}
```

我们将我们的`App`组件包装在`QueryClientProvider`组件周围，让我们使用它的钩子来发出请求。

然后在`App`中，我们使用`useQuery`钩子发出一个 GET 请求。

第一个参数是查询的字符串标识符。

第二个参数的作用是让我们发出请求。

`isLoading`状态表示当请求为真时正在加载。

`error`状态为真时表示发生了错误。

`data`已响应数据。

# 提出发布请求

要发出 POST 请求，我们可以使用`useMutation`钩子。

为此，我们写道:

```
import axios from "axios";
import React from "react";
import { useMutation, useQueryClient } from "react-query";export default function App() {
  const queryClient = useQueryClient();
  const mutation = useMutation(
    (data) => axios.post("https://jsonplaceholder.typicode.com/posts", data),
    {
      onSuccess: () => {
        queryClient.invalidateQueries("todos");
      }
    }
  ); return (
    <div>
      <button
        onClick={() => {
          mutation.mutate({
            title: "foo",
            body: "bar",
            userId: 1
          });
        }}
      >
        Add Todo
      </button>
    </div>
  );
}
```

我们保持`index.js`和前面的例子一样。

我们调用`useQueryClient`钩子来获取查询客户机。

`useMutation`让我们通过传入一个回调来发出请求，这个回调通过用我们想要的 URL 和请求体调用`axios.post`来返回一个承诺。

第二个参数有一个对象，该对象有一个在请求成功时运行的`onSuccess`回调。

我们用请求清除资源的标识符调用`queryClient.invalidaQueries`。

# 结论

我们可以使用 React 查询库轻松地发出 HTTP 请求。

*更多内容请看*[***plain English . io***](http://plainenglish.io)