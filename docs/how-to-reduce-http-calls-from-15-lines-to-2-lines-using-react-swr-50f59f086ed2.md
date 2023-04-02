# 如何使用 React SWR 将 HTTP 调用从 15 行减少到 2 行

> 原文：<https://javascript.plainenglish.io/how-to-reduce-http-calls-from-15-lines-to-2-lines-using-react-swr-50f59f086ed2?source=collection_archive---------3----------------------->

## 用更少的代码大幅改善用户体验。

![](img/803e0294e68ecaa2419eac306de56cdb.png)

Photo by [Wendy van Zyl](https://www.pexels.com/@wendy-van-zyl-312082?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/brown-book-page-1112048/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

如果您是 React 开发人员，您一定希望有一个库来管理所有的 API 调用。

我说的不是`fetch`或者`Axios`。而是一个管理所有加载状态、预取、缓存、分页、验证等的库。

我有好消息告诉你。今天我们将探索一个名为 [SWR](https://swr.vercel.app/) 的包。其中承认自己为`React Hooks for Data Fetching`。

让我们看看这个库能为我们做什么，以及我们什么时候可以使用它。

# 步骤 1:安装依赖项

你可以通过输入来安装它

```
yarn add swr
```

# 步骤 2:创建一个提取器函数

您可以使用各种 fetcher 函数，无论是 REST 还是 GraphQL。

> 提取器函数可以只是本机提取函数的包装。如果你愿意，可以使用 axios

针对 REST 端点的带有`fetch` API 的典型提取器函数可以是

```
**const** fetcher = (...args) => fetch(...args).then(res => res.json())
```

如果你想去 T4，那就去吧

```
**const** fetcher = url => axios.get(url).then(res => res.data)
```

# 第三步:使用 SWR 的时间

让我们在组件内部使用神奇的`useSWR`钩子

normal use of useSWR hook

这个`useSWR`钩子接受两个参数。一个是键(在我们的例子中是`/api/product/123`)，第二个是`fetcher`函数。

这个钩子的作用是返回数据中的产品细节。但是现在你想知道它是如何有用的，因为我们可以通过直接在组件内部调用`axios`或`fetch`来做同样的事情。

好吧，让我给你看看。

# 步骤 4:如何减少代码？

在一个典型的应用程序中，我们通常像下面这样进行 API 调用。我们通常关心三件事。实际的`data`、`loading`状态，以及`error`状态(如果有)。

## 以前

manual data fetching

但是在`useSWR`钩子的帮助下，我们能做的就是

## 在...之后

power of swr

所以我们能够减少很多代码！这太好了！

# 步骤 5:全局错误处理

如果您不够聪明，处理任何应用程序中的 API 错误都可能是一项痛苦的任务。SWR 有一个非常好的功能，让你得到保障，减少更多的麻烦！

它导出一个名为`SWRConfig`的上下文，该上下文可以对所有钩子进行全局控制。在下面的例子中，我们为所有的钩子定义了一个公共的获取函数，并且添加了全局错误处理程序。

global handler with swr

所以现在你不必在使用`useSWR`的任何地方处理错误。一旦你开始使用它，它就非常强大和方便。

# 第 6 步:预填充数据

如果你想通过提供一些默认数据使页面具有即时交互性，SWR 也有这个选项。

当 useSWR 挂钩在后台获取数据并在数据加载完成后显示更新的数据时，您可以提供一些预先存在的数据(从缓存或其他地方)。

```
useSWR('/api/data', fetcher, { fallbackData: prefetchedData })
```

这里我们将`fallbackdata`属性定义为预先填充的数据。当您使用`NextJS`并在`getStaticProps`中生成一些数据时，这种技术特别有用。这样一切都变得超级快。

# 第七步:突变

SWR 的一个局限是它不直接支持突变。然而，我们可以通过使用一个名为`mutate`的便利函数来实现类似的事情。

突变所做的是提供手动调用 API 的能力。例如当你想提交一个表格或什么的时候。

这使得每个 API 调用都非常集中，有助于保持应用程序的整洁。

# 你应该什么时候使用它？

我已经展示了这个强大的库的基础。你可以用它走很长的路。还有更多类似缓存、变异等功能。它可以很好地覆盖 95%的用例。

然而，`SWR`的主要替代品是提供比 SWR 更多功能的`[react-query](https://react-query.tanstack.com/)`。

我推荐使用`react-query`,因为它涵盖了所有可能的场景。但是它有一个缺点。react-query 的包大小几乎是 SWR 的 3 倍。这非常重要。

![](img/0436324b2b8b34e35750bbc3974f2bb7.png)![](img/7cd1390ad2e5e23fec5434f095a54798.png)

SWR vs React Query Bundle size

所以如果你正在构建一个小的应用程序，并且不需要很多复杂的特性，那么你应该选择 SWR。对于其他场景，我建议使用 react-query。

今天到此为止。祝您愉快！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) 联系我

[](/45-npm-packages-to-solve-16-react-problems-a9ab18946224) [## 45 个 NPM 软件包解决 16 个 React 问题

### 关于如何选择完美的 npm 包的深入指导

javascript.plainenglish.io](/45-npm-packages-to-solve-16-react-problems-a9ab18946224) [](/the-greatest-react-developer-i-ever-met-1e58df22bb71) [## 我见过的最伟大的 React 开发者

### 我们有分歧，但仍然…

javascript.plainenglish.io](/the-greatest-react-developer-i-ever-met-1e58df22bb71) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)