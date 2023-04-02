# 使用 JSON —通过 React 使用 Fetch API

> 原文：<https://javascript.plainenglish.io/working-with-json-using-fetch-api-with-react-3223b67d1e7a?source=collection_archive---------16----------------------->

![](img/a352ee04697ebb8fb23e41538325b882.png)

Photo by [Jeremy Perkins](https://unsplash.com/@jeremyperkins?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JSON 代表 JavaScript 对象符号。

这是一种流行的数据交换格式，有许多用途。

在本文中，我们将了解如何将 JSON 与 React 和 Fetch API 结合使用。

# 用 React 发出 HTTP 请求

React 是一个视图库，所以它不附带任何进行 HTTP 请求的方法。

为此，我们必须使用自己的 HTTP 客户端库。

今天，大多数现代浏览器都带有 Fetch API。

我们可以把它和`useEffect`挂钩一起使用。

要使用它，我们可以写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [answer, setAnwser] = useState(); const getAnswer = async () => {
    const res = await fetch("https://yesno.wtf/api");
    const answer = await res.json();
    setAnwser(answer);
  }; useEffect(() => {
    getAnswer();
  }, []);
  return <div className="App">{JSON.stringify(answer)}</div>;
}
```

使用`fetch`函数向端点发出 GET 请求。

它返回一个解析为数据的承诺，然后我们调用`json`从 JSON 获取数据。

然后我们调用`setAnswer`来设置`answer`状态。

第二个参数中的空数组意味着我们只在组件挂载时运行回调。

此外，我们可以通过编写以下代码将`getAnswer`函数移动到它自己的钩子中:

```
import React, { useEffect, useState } from "react";const useAnswer = () => {
  const [answer, setAnwser] = useState(); const getAnswer = async () => {
    const res = await fetch("https://yesno.wtf/api");
    const answer = await res.json();
    setAnwser(answer);
  }; useEffect(() => {
    getAnswer();
  }, []);
  return answer;
};export default function App() {
  const answer = useAnswer();
  return <div className="App">{JSON.stringify(answer)}</div>;
}
```

我们将所有逻辑从 API 端点转移到它自己的钩子上。

然后，我们可以保持我们的组件非常干净，没有副作用。

要使用 Fetch API 发出 POST 请求，我们可以编写:

```
import React, { useEffect, useState } from "react";const makeRequest = async (data) => {
  const res = await fetch("https://jsonplaceholder.typicode.com/todos", {
    method: "POST",
    mode: "cors",
    cache: "no-cache",
    credentials: "same-origin",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify(data)
  });
  const response = await res.json();
  return response;
};export default function App() {
  const submit = async () => {
    const res = await makeRequest({
      title: "delectus aut autem",
      completed: false
    });
    console.log(res);
  }; return (
    <>
      <button onClick={submit}>add todo</button>
    </>
  );
}
```

我们添加了`makeRequest`函数，该函数使用 URL 调用`fetch`，向 an 对象发出带有请求选项的请求。

`method`属性是请求方法。

`mode`是请求模式。`'cors'`提出跨来源请求。

`cache`设置为`'no-cache'`禁用缓存。

`credentials`设置 cookies 的来源。

`headers`拥有我们想要发送的 HTTP 请求头。

`body`有 HTTP 请求体。

当我们点击“添加待办事项”按钮时，然后`submit`函数使用`makeRequest`函数发出请求。

然后返回响应数据，并从控制台日志中记录从`makeRequest`函数返回的承诺。

# 结论

我们用 Fetch API 在 React 应用程序中发出 HTTP 请求。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**