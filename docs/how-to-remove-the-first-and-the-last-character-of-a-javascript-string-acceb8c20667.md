# 如何删除 JavaScript 字符串的第一个和最后一个字符？

> 原文：<https://javascript.plainenglish.io/how-to-remove-the-first-and-the-last-character-of-a-javascript-string-acceb8c20667?source=collection_archive---------21----------------------->

![](img/0d364bc00d10f8ad3cf13f854713fbf2.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望删除 JavaScript 字符串的第一个和最后一个字符。

在本文中，我们将研究如何删除 JavaScript 字符串的第一个和最后一个字符。

# 使用 String.prototype.substring 方法

我们可以使用 JavaScript 字符串的`substring`方法来返回起始和结束索引之间的字符串。

包括开始索引，但不包括结束索引。

为了使用它，我们写:

```
const str = "/installers/";
const result = str.substring(1, str.length - 1);
console.log(result);
```

分别用起始和结束索引调用`substring`。

`str.length — 1`是结束索引，因为我们只想返回到倒数第二个字符的字符串。

因此`result`就是`'installers'`。

# 使用 String.prototype.slice 方法

我们还可以使用 JavaScript 字符串的`slice`方法返回起始和结束索引之间的字符串。

例如，我们可以写:

```
const str = "/installers/";
const result = str.slice(1, -1);
console.log(result);
```

用我们希望包含在`result`中的`str`的开始和结束索引来调用`slice`。

Index -1 是字符串的最后一个索引，不像`substring`一样包含在返回的字符串中。

因此，`result`与上例相同。

# 结论

我们可以使用 JavaScript string `slice`或`substring`方法在给定的开始和结束索引中提取一个字符串。

无论使用哪种方法，返回的字符串中都不包含索引末尾的字符。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)