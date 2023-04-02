# 使用 Next.js 了解静态站点生成

> 原文：<https://javascript.plainenglish.io/understand-static-site-generation-with-next-js-22e86efda38c?source=collection_archive---------8----------------------->

## 充分利用静态站点生成。

![](img/c0097a015ad3b5848d299530a8cd30f8.png)

Image by [Mudassar Iqbal](https://pixabay.com/users/kreatikar-8562930/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3461405) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&utm_medium=referral&utm_campaign=image&utm_content=3461405)

我们都爱 Next.js 的服务器端渲染能力。但是我们经常不能利用静态一代的魅力。

如果设计得当，我们几乎可以预先生成网站的每个页面，因此，我们的网站就像一个静态网站。快速和搜索引擎友好。

但是使用 Next.js 可以预生成的页面数量是有限制的。今天，我们将尝试理解 Next.js 中静态站点生成的不同用例。

# 静态生成是如何工作的

静态生成意味着我们将在服务器端预先生成页面，当用户请求页面时，我们将向他们发送回实际的 HTML 文件。这是 Next.js 和 React 的主要区别，React 只支持客户端生成。

为了用 Next.js 静态生成页面，我们需要使用两个函数。

1.  `getStaticPaths` - >提前知道所有可能的路线
2.  `getStaticProps` - >生成页面所需的道具

假设您想要预先生成您个人网站的所有博客帖子。网址看起来有点像`/blog/{blogId}`

在这种情况下，代码将如下所示。

你应该已经熟悉语法了，所以我不想详细说明。我们将重点理解静态生成的不同方法。

# 问题是

主要问题是我们可以预先生成的页面数量是有限制的。你可以在`[vercel website](https://vercel.com/docs/concepts/limits/overview)`上查看。一般是 8000 页。

现在根据情况，我们必须做出明智的决定，决定我们将采取哪种方法。并且生成基于`fallback`属性的作品。

有 3 个可能的值。

1.  `false`
2.  `true`
3.  `blocking`

让我们讨论一下使用这些不同值的场景。

# 你有一个动态内容较少的小网站

如果你正在建立一个投资组合页面，随着时间的推移，你的页面很有可能会非常相似，并且它们也会在 8000 页的限制内。

在这些场景中，您必须指定 fallback = `false`

当您将回退定义为`false`时，您基本上是在告诉 Next.js 只提供静态页面。所以它就像一个静态网站。

尽管有一些暗示。

1.  如果任何用户想要访问任何未预先生成的路线，他们将会看到 404 页面。Next.js 不会尝试在运行时构建这个页面。
2.  如果你改变网站的任何内容(意味着增加一些新的路线)，你必须重新部署整个应用程序。
3.  一般来说，这将确保不会出现不需要的路由。这种方法会让你的网站看起来像一个静态网站。

# 拥有大量动态内容的大型网站

如果你有一个可能有大量页面的网站，你想给用户一个页面的框架(为了良好的用户体验)。那你应该用`fallback` = `true`。

现在，如果任何用户请求一个不是静态生成的页面，服务器不会用 404 页面响应。相反，

*   它将立即返回一个没有道具的版本(在这个阶段，我们的工作是展示骨架版本)
*   它会尝试在后台为页面获取合适的道具(就像`getServerSideProps`)。

现在的问题是，如何理解何时显示框架，何时显示实际页面？

为此，我们利用了 Next.js 的`router`。在您的组件中，您将尝试了解页面是否具有所需的可用属性，并基于此显示页面的适当版本。

这是动态生成静态页面的好方法。

好的一面是，一旦用户请求了一个页面并生成了该页面，服务器将缓存该页面以供后续请求使用。这是非常好和有效的！

# 动态内容，但没有框架

如果你有一个网站，其中大部分页面都是预先生成的，你不想为显示非预先生成页面的框架而烦恼，那么你将使用`fallback` = `blocking`

现在，当任何用户请求一个页面时，除了一个空白页面(或加载程序)，他们什么也看不到。服务器只有在后台获得合适的道具后才会响应。

# 最后的话

尝试理解`fallback`属性的不同值，以便充分利用 Next.js 的静态生成功能。

今天到此为止。祝您愉快！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) 联系我

*更多内容请看*[***plain English . io***](http://plainenglish.io/)

[](/how-to-handle-different-environments-in-a-next-js-application-8dc4aef6ad9b) [## 如何在 Next.js 应用程序中处理不同的环境

### 关于 Next.js 中的环境变量，您需要知道的一切

javascript.plainenglish.io](/how-to-handle-different-environments-in-a-next-js-application-8dc4aef6ad9b)