# 用 async/await 解决回调问题

> 原文：<https://javascript.plainenglish.io/get-rid-of-callback-hell-with-async-await-f21f1b5e3364?source=collection_archive---------12----------------------->

## Promise 改变了我们对 JavaScript 中回调的看法。它还改变了我们编写回调的方式，并为回调地狱提供了一个很好的解决方案🤯

![](img/96a9bc9fe8cddc3a7019e68197a96b2e.png)

Photo by [Jeremy Bishop](https://unsplash.com/@jeremybishop?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/waves?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在本文中，我将解释如何使用 async/await 编写更易于阅读和理解的代码。

用例—从一个 API 端点按书名搜索一本书，这个 API 端点有该书的 ISBN、书名和价格，另一个 API 端点检查该书是否有库存，然后点击另一个 API 端点检查其价格，连接所有响应，然后将其发送到前端。

首先，让我们假设一个 API，当按书名搜索时，它返回一本书。在这个例子中，我正在搜索一本名为《孙子兵法》的书。这个 API 响应返回具有名称、作者和 ISBN 的 book 对象。

然后使用`getBookByName`承诺调用 getBookByName 方法

一旦找到书的详细信息，让我们通过调用另一个承诺来检查这本书是否有货。在这个承诺中，我将返回股票& ISBN 详细信息。

然后通过传递从响应中收到的 ISBN 来调用`getBookByName`方法中的`checkIfBookExists`方法。`checkIfBookExists`将图书 ISBN 作为参数。

如果图书库存存在，`checkIfBookExists` API 返回库存数量和 ISBN。之后，让我们通过使用`BooksRun API`来检查图书的定价，BooksRun API 通过 ISBN 返回图书的价格。该响应包含任何书籍的新价格、旧价格和租金🤘

如果图书的库存大于 0，则调用`getTheBookPrice`。让我们查一下那本书的价格

在真实的场景中，会有空检查和 API 调用🤭在上面的代码示例中，有很多回调，`then`并且我试图避免编写 catch😂。现在用`async/await`重写整个例子👇

使用 async/await 使代码看起来更干净，可读性更好，调试也更容易👍

完整的代码片段供参考👇

感谢您花时间阅读这篇文章！🙏

*更多内容请看*[***plain English . io***](http://plainenglish.io/)