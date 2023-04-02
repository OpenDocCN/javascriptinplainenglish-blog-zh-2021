# 如何在 JavaScript 中从字符串中提取基本 URL？

> 原文：<https://javascript.plainenglish.io/how-to-extract-the-base-url-from-a-string-in-javascript-74a12733a4c8?source=collection_archive---------8----------------------->

![](img/3dc3af34552b2bf806474d21aee68c69.png)

Photo by [Samuel Branch](https://unsplash.com/@simply_samuel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 JavaScript 从字符串中提取基本 URL。

在本文中，我们将研究用 JavaScript 从字符串中提取基本 URL 的方法。

# 创建一个锚元素，并从创建的元素中获取基本 URL 部分

我们可以创建一个锚元素，并从创建的元素中获取基本 URL 部分。

例如，我们可以写:

```
const a = document.createElement("a");
a.href = "http://www.example.com/article/2020/09/14/this-is-an-article/";
const baseUrl = `${a.protocol}//${a.hostname}`
console.log(baseUrl)
```

我们用`document.createElement`创建`a`元素。

然后我们将其`href`设置为我们想要从中提取基本 URL 的 URL。

然后结合`protocol`和`hostname`属性得到`baseURL`。

因此，我们看到`baseURL`就是`‘http://www.example.com’`。

# 创建一个 URL 对象，并从创建的元素中获取基本 URL 部分

从 URL 获取基本 URL 的另一种方法是创建一个`URL`实例，并从对象中提取基本 URL 部分。

例如，我们可以写:

```
const url = new URL("http://www.example.com/article/2020/09/14/this-is-an-article/")
const baseUrl = `${url.protocol}//${url.hostname}`
console.log(baseUrl)
```

我们传入完整的 URL 作为`URL`构造函数的参数。

然后我们可以像以前一样，通过组合`protocol`和`hostname`来获得基本 URL。

`baseURL`同上。

# 结论

我们可以通过创建一个锚元素或者使用`URL`构造函数，用 JavaScript 从字符串中提取基本 URL。

*多内容于* [*中*](http://plainenglish.io/)