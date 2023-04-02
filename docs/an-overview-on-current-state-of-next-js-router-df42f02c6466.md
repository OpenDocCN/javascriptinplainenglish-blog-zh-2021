# Next.js 路由器现状综述

> 原文：<https://javascript.plainenglish.io/an-overview-on-current-state-of-next-js-router-df42f02c6466?source=collection_archive---------22----------------------->

## 这些关于 Next.js 路由器的提示和技巧有助于使你的 DX 更好，代码更简洁

> 最初发布于[我的博客 pavel.mineev.me](https://pavel.mineev.me/blog/nextjs-router-tips-and-tricks)

![](img/84326cb3051cb1abd5b0f9e102d662c1.png)

Photo by [Denys Nevozhai](https://unsplash.com/@dnevozhai) on Unsplash

## 放弃

Next.js 是一个动态开发的框架，许多关于它的旧文章可能会过时，因为 Next.js 向前迈出了一大步。我在 2021 年 5 月写了这篇文章，现在的版本是 10.2.3。我建议在查看示例时查看[文档](https://nextjs.org/docs/getting-started)，因为由于 API 的改进，一些提示可能已经过时。

# 发布了你可能不知道的功能

如果你长时间使用 Next.js，你的项目应该有大量的代码，你只需要按照它已经有的风格继续写。有时是因为你已经习惯了，有时是因为你把你的代码库当作代码片段和例子的目录。这就是为什么你可以跳过新的酷的东西。

## 服务器重定向和未找到状态

这些功能，以及以前的功能，都是在版本 10 中发布的，我仍然看到很多关于如何在服务器上进行重定向的问题。首先，我建议检查您是否使用现代抓取方法，因为只有它们才能获得更新和新功能。我在这里解释了为什么我们应该使用现代获取方法的其他原因。

下面是重定向或显示 404 页的一个简单方法:

## href 参数的自动解析

试着在你的项目中找到有`href`和`as`道具的`next/link`。如果你已经找到了，是时候更新链接了。因为从 10.x 版本开始，不需要同时传递两个参数。你可以去掉`href` param，把`as`重命名为`href`，也一样可以。

# 客户端路由器功能

我注意到人们经常从`useRouter`用`router.push`。如果你在`useCallback`或者`useEffect`中的函数中使用它，你必须在依赖关系中提到它，就像下面的例子。

这完全没有必要，因为这些函数不会在重新渲染时更新，但是 ESlint 规则会告诉你应该这样做。解决这个问题相当简单。只需使用`Router`中的路由功能。它使你的代码更干净、更好。😉

有时当我使用路由器时，我需要获得当前的路径名。但是`react/router`在那个字段中存储路由器的动态表示，它与路由器字段相同。我们可以用`asPath`自己创建这些参数。我在`useRouter`上创建了一个包装器，如果需要的话，我可以随时使用这些道具。

包装器为我们提供了方便的工具，我们可以在需要更新当前路线的情况下使用这些工具。

你想知道为什么`Router.replace`中的第二个参数是`null`吗？从 10.x 开始，通过自动解析，我们可以跳过该参数。

因为我们有自动解析这样的特性，所以我们可以在`next/router`中使用它，但是在它的 API 中有一点不便。因为如果你想传递`options`，你应该把动态路由传递给第一个参数，把完整路径传递给第二个参数，在早期版本中，Next.js 保留了这三个参数以向后兼容。我有一些方便的小功能，可以帮助我更轻松地使用路由器功能。

# 结论

谢谢你把文章看完。你可以在 [GitHub](https://github.com/akellbl4/nextjs-router-tips) 上找到完整代码。总有办法让好工具变得更好。小的改进会对你和你的项目有很大的帮助。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)