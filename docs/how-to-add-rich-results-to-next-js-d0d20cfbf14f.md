# 如何给 Next.js 添加丰富的结果

> 原文：<https://javascript.plainenglish.io/how-to-add-rich-results-to-next-js-d0d20cfbf14f?source=collection_archive---------15----------------------->

![](img/122eb73a6136c49390bfc43da5ec74dd.png)

How to add rich results to next js

> 现在你已经启动并运行了 Next.js 应用程序，离添加 Google rich 结果只有一步之遥了，本指南将告诉你如何做到这一点！

让我们面对现实吧，你已经非常努力地让你的 Next.js 博客或网站达到现在的位置。然而，你觉得有什么东西不见了，嗯，这可能是谷歌丰富的结果。

我们有一个简单的指南，告诉你如何设置你的 Next.js 应用程序来兼容 google rich results。我们将这篇文章分成两个部分，**操作方法**和**一些让你开始运行的提示**。事不宜迟，我们开始吧！

## 如何添加谷歌丰富的结果

拥有一个 Next.js 富结果兼容网站的第一步是知道在哪里添加富结果。

添加丰富结果的**最好的**地方是在实际的文章内容上。请不要试图将 Next.js 丰富的结果添加到您的主页中。这是不可行的，因为如果你仔细想想，它没有多大意义。

因此，在不影响您的 Next.js SEO 的情况下，您可以简单地通过利用 Next.js 页面的 head 部分来添加您想要的 google rich 结果。所以，你会这样做:

```
<Head>{/* Some other code may come here */}<script type="application/ld+json" dangerouslySetInnerHTML={{__html:`
    {
        "@context": "https://schema.org",
        "@type": "NewsArticle",
        "headline": "${yourArticleTitle}",
        "image": [ "image one url", "image two url", "image three url"  ],
        "datePublished": "${yourArticlePublishedOn}",
        "dateModified": "${yourArticleUpdatedOn}"
    }
`}}></script></Head>
```

这基本上就是你需要的全部。

最好理解上面的代码:

**type = " application/LD+JSON "**

您需要指定脚本标记中的内容属于这种类型。 ***ld+json*** 是一种使用 json 轻松编码链接数据的优雅方式。

**dangerouslysettinnerhtml**

这听起来很可怕，但我们需要找到一种方法来将文本添加到我们的 JSX 脚本标签中，这就是我们将如何做。

**@上下文**

这是要用到的上下文，在这个例子中，我们用[**https://schema.org**](https://schema.org)

**@类型**

这是我们丰富结果的类型，在这种情况下，我们使用 NewsArticle。有许多@type 选项，所以请随意尝试最适合您需求的选项。

**标题**

这是这个富文本将出现的标题，我们将它作为文章标题。

**图像**

这是要使用的图像数组。需要记住的重要一点是，提供的图片应该与你的网站托管的图片来自同一个方案。

举个例子:如果你的网站是在 **HTTPS** 托管的**，那么你的图片也应该从 **HTTPS** 提供。否则，你会得到臭名昭著的不同方案的错误，你的谷歌丰富的结果可能无法正确呈现。**

**发布日期**

这只是你的文章发表的日期。它应该采用兼容的 ISO 日期格式。

**修改日期**

这是你文章最后一次更新的时间。它还应该与 ISO 日期格式兼容。这可能与发布日期的值相同，这取决于您如何处理文章更新。

这基本上概括了一切。接下来的事情就是简单地更新你的网站，瞧！

## 一些提示

作为临别礼物，这里有一些免费的建议:

*   对图片和你的网站总是使用相同的方案。也就是说，HTTP 是对 HTTP，HTTPS 是对 HTTP。
*   请记住根据您的内容指定正确的@type，因为不同的类型需要不同的内容。
*   日期格式很重要。
*   图像数组应该是兼容的 JSON 数组。不要使用单引号来指定数组中的图像 URL。

此外，值得注意的是，尽管现在有了 Next.js 丰富的结果集，但这并不是解决您网站上任何 Next.js SEO 问题的一次性解决方案。

有了 Next.js 丰富的结果，你所做的只是增强你页面上的内容如何被感知，这可能会提高你的 SEO 排名，**但是**我再次强调，这不会改善你网站上存在的任何 Next.js SEO 问题。

## 结论

这个简单的指南为您提供了一种将 Google-rich 结果添加到 Next.js 应用程序的方法。

好了，现在就这样。

**编码快乐！**

> 有没有兴趣学习 **Next.js** ？在我的网站上查看类似的精彩文章:[对代码的狂热> Next.js](https://bingeoncode.com/category/next-js)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)