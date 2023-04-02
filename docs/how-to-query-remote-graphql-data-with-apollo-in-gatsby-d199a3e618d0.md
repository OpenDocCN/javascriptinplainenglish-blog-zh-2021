# 如何在 Gatsby 中用 Apollo 查询远程 GraphQL 数据

> 原文：<https://javascript.plainenglish.io/how-to-query-remote-graphql-data-with-apollo-in-gatsby-d199a3e618d0?source=collection_archive---------1----------------------->

![](img/f45f7f5eba69dc112122ac9d06fbc83a.png)

Gatsby 是一个依赖于 GraphQL 的 React 静态站点生成器。它可以将(几乎)任何来源任何数据转换为 GraphQL，允许您查询这些数据，并使用这些数据来构建静态网站；静态网站意味着巨大的安全性，惊人的性能，搜索引擎优化反应。

这是完美的，特别是如果你有一个“内容”网站，如博客、新闻网站、作品集，以及一般情况下可以在内容更新时生成的网站(Gatsby 也可以增量构建)，并且不需要在运行时访问远程数据。

但是，让我们假设您正在使用 WooCommerce 编写一个电子商务网站(是的，您可以通过 GraphQL 访问您的商店数据并构建一个超快速的静态目录)，并且您需要在显示“添加到购物车”按钮之前检查某个产品的可用性，或者您想要验证用户并跟踪会话、购物车，在您的远程 WooCommerce 上保存订单。或者你想在你的博客上添加评论，或者向认证用户显示更多的数据(或者不同的价格)。

案例是无限的，一般来说，有些时候你需要访问远程和最新的数据，并在你的静态 Gatsby 页面中组合结果，在这些时候你会在你的 Gatsby 项目中需要 [Apollo Client](https://www.apollographql.com/docs/) 。

# 阿波罗基础

要访问 Apollo 的“功能”,您可以将应用程序包装在一个提供者中(带有客户端属性，如 GraphQL URL ),然后在您的页面中，您可以访问几个挂钩(主要是 useQuery)来查询数据。因为我们使用 Gatsby，所以我们将使用`gatsby-browser.js`和`gatsby-ssr.js`来包装使用`wrapRootElement`函数的代码，这样项目中的任何页面和任何组件都可以查询或改变远程 GraphQL 源，允许您在静态页面中拥有“活”数据。

# 我们将创造什么

我们将构建一个紧凑的(无用的)天气应用程序，它将从我在 Heroku 上找到的 GraphQL API 请求数据并显示结果，我们还将添加一个下拉列表来选择一个城市，我们将实现 Apollo 的`refetch()`功能，以始终获得最新数据。您还可以克隆本教程的[库。](https://github.com/popeating/gatsby-apollo)

# 先决条件

要理解这一点，您至少需要对 React JS、Gatsby(及其文件结构)、一点 GraphQL(以及如何查询它)有基本的了解

# 盖茨比项目

## 初始化项目

我们从一个空白项目开始，我将我的项目命名为 gatsby-apollo，除了 sass 之外，我没有安装任何插件(但是你可以省略它或者选择另一种样式方法)。让我们从以下内容开始:

```
npm init gatsby
```

设置完成后，进入项目的文件夹以完成模块的安装。

我们需要几个模块，*同构获取*，它是获取函数的一个[多填充器](https://en.wikipedia.org/wiki/Polyfill_(programming)):

```
npm install — save isomorphic-fetch
```

最后是 Apollo 客户端和 graphql 库

```
npm install @apollo/client graphql
```

此时，您可以用如下空白模板替换文件 *pages/index.js* 的内容:

运行以下命令并访问`http://localhost:8000`

```
gatsby develop
```

您应该会看到一个只有“Hello World”的空白页面。

## 定义阿波罗提供者

我们现在要定义将包装我们的应用程序的 Apollo 提供者和客户端。

在您的`src`文件夹中，创建一个名为`apollo`的新文件夹(或者您可以随意命名)，在这个文件夹中，我创建了两个文件`client.js`，它们定义了 Apollo 客户端属性，比如我们将要查询的 URL、获取命令、缓存类型等等。这是一个基本示例，但是客户端可能会更复杂，有时您希望从响应中读取一些报头，或者您希望[在您的请求](https://www.apollographql.com/docs/react/networking/authentication/#header)中发送一个无记名身份验证令牌:

另一个文件是`provider.js`,它将把我们的应用程序包装在 Apollo provider 中，将客户端暴露给所有的子元素:

此时，您需要使用 Gatsby 浏览器 API 和 Gatsby 服务器呈现 API，在提供 HTML 内容时(通过浏览器和 SSR)对其进行操作，并用 ApolloProvider 包装根元素。

在项目的根目录下创建`gatsby-browser.js`和`gatsby-ssr.js`文件，并在这两个文件中添加以下代码行(如果您需要关于这些 API 的更多信息，可以在 Gatsby 中找到:[https://www . Gatsby js . com/docs/reference/config-files/Gatsby-SSR/# wrapRootElement](https://www.gatsbyjs.com/docs/reference/config-files/gatsby-ssr/#wrapRootElement)):

这就是所有的配置，如果你重新加载你的应用程序，它应该没有改变，但如果没有错误，这意味着你的索引页面现在包装在 ApolloProvider 中，可以访问我们之前定义的客户端配置。

## 第一次查询

让我们回到 index.js，用一个基本查询来试试是否一切都如预期的那样工作:

我们现在从 Apollo 导入了 useQuery 钩子，我们定义了一个基本的查询(我不会详细描述这个查询和它的数据，你可以在这里找到它的端点和文档:【https://graphql-weather-api.herokuapp.com/)
然后我们使用钩子将查询传递给它(它可以接受更多的参数，稍后会更详细一点)，它返回一个加载布尔值、一个错误对象和一个数据对象。根据结果，我们可以在页面上打印不同的内容，例如，加载状态、结果或错误

如果一切正常，我们可以开始构建动态查询并格式化结果。

我们修改查询以获得几个参数`location`和`unit`并返回相关数据:

我们将发送给查询的参数和结果存储在状态中:

现在我们可以执行传递参数的查询，这一次我们向 *useQuery* 添加了一个 *refetch* 属性，因为我们希望在参数改变时重新提取数据(否则 Apollo 将缓存结果)。

正如您所看到的，useQuery 钩子像以前一样有查询引用(W_Q)和一个配置对象。在这个对象中，我们指定了变量数据(来自我们的状态组件)、用于在 refect 时更新组件的*notifyOnNetworkStatusChange*参数，以及一个 *onCompleted* 方法，该方法将在数据加载后执行回调；在这种情况下，设置天气状态和日期状态(将时间戳转换为可读日期)。

现在，我们在 state 组件中几乎拥有了一切，所以剩下的就是将数据放入我们的接口，并处理城市和单位的更新，以触发 *refetch():*

我们定义了几个函数(稍后将绑定到 select)来更新两个状态，这些更新将触发 useEffect 中的 refetch()。

对于渲染部分，这只是一个基本的页面，可能没有优化，有很多重复，一些基本的检查。

页面根据*位置*状态显示天气，一旦选择的位置发生变化，位置状态就会更新并触发重新提取(位置是一个 useEffect 依赖项)，重新提取后页面会重新呈现。

## 后续步骤

至此，您已经有了一个关于如何使用 Apollo 在静态项目中检索和使用动态数据的完整示例；将您的“客户机”连接到 GraphQL 数据源，您就可以开始工作了。

当然，这是一个基本的例子，但是 GraphQL 也可以用 useMutation 钩子‘写’到一个源；Apollo 客户端也可以比我们在这里创建的更复杂，允许处理会话、身份验证令牌等等。
一个经典的例子是使用 JWT 的认证:你使用登录突变进行认证，GraphQL 将向你发回一个令牌，你获取该令牌并将其存储在某个地方(例如 LocalStorage)，在将来的请求中，你可以将该令牌(如果存在的话)包含在客户端报头中，这样 GraphQL 服务器就知道该请求来自一个授权用户。例如，用户可以通过认证访问他们的愿望清单或订单历史，他们的*待办事项*，等等。

## 免费公共图表

有很多免费的 GraphQL API 可以连接到 Apollo 上玩，例如[星球大战 API](https://graphql.org/swapi-graphql) 或 [GitHub API](https://developer.github.com/v4/explorer/) ，如果你在 [Datastax 上有一个无服务器数据库，也可以通过 GraphQL](https://docs.datastax.com/en/astra/docs/using-the-astra-graphql-api.html) 访问。此外，Apollo 提供了一个工具来[创建 GraphQL 模式，并用您数据源](https://www.apollographql.com/docs/intro/platform/#1-build-your-graph-with-apollo-server)填充它。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)