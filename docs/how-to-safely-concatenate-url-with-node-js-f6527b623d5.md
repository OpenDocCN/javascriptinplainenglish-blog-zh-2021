# 如何用 Node.js 安全地连接 URL

> 原文：<https://javascript.plainenglish.io/how-to-safely-concatenate-url-with-node-js-f6527b623d5?source=collection_archive---------2----------------------->

## 学习一种用 Node.js 安全连接 URL 的方法。

![](img/c6f6fb6e7869f68539e0a9d74e09e895.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/programming?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

最近，在我的一个项目中，我有几个 URL，需要一个函数来连接它们并构造一个完整的 URL。

我想构建的完整 URL 的例子:`https://github.com/weikangchia/gitcg`

1.  baseUrl: `https://github.com`
2.  路径 1(此存储库的用户):`weikangchia`
3.  路径 2(存储库的名称):`gitcg`

最初，我使用 ES6 模板文字方法来构造完整的 URL。

然而，我意识到这种方法并不安全。如果我的任何路径碰巧包含一个斜杠，我的`fullUrl`就会有一个双斜杠并成为一个无效的 URL。

在谷歌搜索了一段时间后，我尝试使用了两个 Node.js 模块:

1.  [Url](https://nodejs.org/api/url.html#url_url)
    提供 Url 解析和解析工具的模块。它提供了两个处理 URL 的 API:一个是特定于 Node.js 的遗留 API，另一个是实现 web 浏览器使用的相同的 WHATWG URL 标准的新 API。
2.  [Path](https://nodejs.org/api/path.html)
    一个模块，提供了处理文件和目录路径的工具。

而且，成功了！我感觉这种方式是比较安全的用 Node.js 串联 URL 的方式之一，这种方式只使用 Nodejs.js 中的内置模块，所以处理 CVE 和维护我们生产代码的作业比较少。

现在我们有了。我希望你已经发现这是有用的。感谢您的阅读。如果你喜欢这篇文章，记得关注我的更多更新！

如果你认为用 Nodejs 连接 URL 有更好的方法，请在下面留下你的评论。

如果你还不是灵媒会员，并且想成为灵媒会员，[点击这里](https://weikangchia.medium.com/membership)。

[](https://weikangchia.medium.com/membership) [## 用我的推荐链接加入媒体-伟康

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

weikangchia.medium.com](https://weikangchia.medium.com/membership) 

*更多内容看* [***说白了. io***](http://plainenglish.io/)