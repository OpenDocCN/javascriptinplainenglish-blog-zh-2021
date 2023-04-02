# 停止直接使用 Fetch API——SWR 要好得多

> 原文：<https://javascript.plainenglish.io/stop-using-fetch-api-directly-swr-is-way-better-588976ef6782?source=collection_archive---------0----------------------->

## 是时候开始在你的 React 应用中使用 SWR 了

![](img/12b391896948a6aa5a65aaa5827a629e.png)

Photo by [Ben White](https://unsplash.com/@benwhitephotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

常见的数据获取实践，如**获取 API** 或 **Axios 库**在 React 中运行良好。它们可以用来非常容易地发送和获取数据。

但是缓存/数据分页/自动重新验证或请求重复数据删除呢？所有这些都需要我们来处理，因为 Fetch 和 Axios 都没有提供这样的功能。在本文中，让我们来看看 **SWR** ，这是一个令人惊叹的 React 钩子库，它将 React 中的数据获取提升到了另一个层次。

# SWR 是什么？

**SWR** 代表`**stale-while-revalidate**`，由 [HTTP RFC 5861](https://tools.ietf.org/html/rfc5861) 推广的一种 HTTP 缓存失效策略。基本上，它通过 3 个主要步骤执行数据提取:

1.  首先返回缓存的数据(*陈旧*)
2.  发送获取请求(*重新验证*)
3.  返回最新的数据

SWR 是一个由 Vercel 开发的快速轻量级软件包。SWR 是构建在获取 API 之上的一层，它在数据获取之上提供了额外的特性。一些特性包括缓存、自动重新验证、分页等。

# 为什么你需要用 SWR？

## 1.内置缓存和实时体验

使用 SWR，用户首先看到缓存的(*陈旧的*)数据，请求被**自动**缓存。React 组件将不断地自动更新最新的数据，从而确保 UI 总是快速和反应性的。

## 2.自动重新验证

SWR 确保用户能够看到最新的数据。即使打开了多个选项卡，当选项卡被重新聚焦时，数据也将始终保持同步。这同样适用于窗口。你可以在下面的链接中查看它是如何工作的:

*演示:*[*swr.vercel.app/docs/revalidation*](https://swr.vercel.app/docs/revalidation)

SWR 还可以按特定的时间间隔重新验证数据，以确保多个会话拥有相同的同步数据。

另一个很酷的特性是，如果用户离线，一旦他重新连接，SWR 将自动重新验证数据，并将更新的数据传递给组件。

## 3.页码

SWR 的另一个有用的特性是它支持分页和无限加载数据。SWR 提供了一个名为`**useSWRInfinite**`的简单钩子来处理分页，而不是让用户编写自己的逻辑来对用 Fetch 或 Axios 接收的数据进行分页。

## SWR 的其他好处

您应该在 React 应用程序中使用 SWR 的其他原因包括:

*   相关提取
*   智能错误重试
*   分页和滚动位置恢复
*   反应悬念
*   局部变异(乐观用户界面)
*   快速页面导航
*   间隔轮询
*   SSR / ISR / SSG 支持
*   焦点的重新验证
*   网络恢复的再验证
*   打字稿和反应原生就绪
*   支持从 REST 和 GraphQL APIs 获取数据

# 例子

让我们来看看如何在 React 应用程序中使用 SWR。

## 步骤 1:安装软件包

```
npm install swr
```

## 步骤 2:导入使用 SWR

```
import useSWR from 'swr'
```

`useSWR`钩子返回两个值:`data`和`error`。它接受一个`key`(通常是请求的 URL 或 graphQL 查询)作为第一个参数，接受一个`fetcher`函数作为第二个参数。

这里有一个如何使用它的例子:

```
const { data, error } = useSWR('/api/123', fetcher)
```

## 步骤 3:编写一个 fetcher 函数

`fetcher`函数可以是异步函数，您可以使用任何数据读取库来编写该函数。这里，我们将使用基本的 Fetch API 编写我们的`fetcher`函数。在 React 组件中，我们可以像这样创建函数:

```
import useSWR from 'swr'function App () {
  // Fetcher function
  const fetcher = (...args) => fetch(...args).then(res => res.json())
  //...
}
```

## 步骤 4:获取数据

在这个例子中，我们将使用 [JSONPlaceholder API](https://jsonplaceholder.typicode.com/) 来获取一些模拟数据。

当获取`data`(`undefined`)时，我们可以显示加载消息，如果返回`error`，我们可以显示错误消息。

```
import useSWR from 'swr'function App () {  
   // Fetcher function
   const fetcher = (...args) => fetch(...args).then(res => res.json())// SWR implementation
  const { data, error } = useSWR('https://jsonplaceholder.typicode.com/posts/1', fetcher) if (error) return <div>Failed to load</div>
  if (!data) return <div>Loading</div> // render data here
}
```

## 第五步:显示数据

模拟数据采用以下格式:

```
{
   "userId": 1,
   "id": 1,
   "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
   "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

一旦获取了数据，我们就可以呈现它。我们最后的组件看起来会像这样:

我们可以运行`npm start`来测试我们的应用程序，它应该在加载屏幕后显示这样的数据。

![](img/9b4ad82fdcb478cdc4b7009748db9f05.png)

Output screen

# 结论

我们可以通过缓存、分页和自动重取来充分利用 SWR 的潜力，因为它们可以极大地改善用户体验。它也非常轻量级，可以很容易地被采用。

我希望我已经向您简要介绍了 SWR，以及如何在 React 应用程序中实现它。所以，让我们努力充分利用 SWR，打造一个令人敬畏的 UX。

编码快乐！

# 参考

[](https://swr.vercel.app/docs/getting-started) [## 入门- SWR

### 在 React 项目目录中，运行以下命令:或者使用 npm:对于使用 JSON 数据的普通 RESTful APIs，首先您…

应用程序](https://swr.vercel.app/docs/getting-started) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。*