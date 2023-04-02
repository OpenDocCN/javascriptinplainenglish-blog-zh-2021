# 如何在 JavaScript 中重用承诺

> 原文：<https://javascript.plainenglish.io/reusing-promises-in-javascript-392bd505f346?source=collection_archive---------6----------------------->

![](img/1be883f15027eeb05a858e87f1de123a.png)

最近，我们开始了一个项目，以提高我们的主要应用程序的性能。我们发现了一些我们经常调用的 API 调用。这些调用的结果可能会改变，但不会经常改变，所以缓存一分钟左右的结果不成问题。

所以我实现了一个非常简单的缓存，它将重用活动的承诺，并在初始解决后返回已经解决的结果。

本文将详细讨论这些代码。让我们从模拟参数化的 API 调用开始。

很简单。

现在我们需要一些变量来存储我们的承诺、结果和解决时间。我们还将创建一个新函数，我们将调用该函数来获取缓存的结果。

_cacheValues 将保存已经解析的值，_cachePromises 将保存正在进行的承诺，而 _cacheResolvedTime 将保存上次解析键承诺的时间。

现在我们将添加一个简单的 if 语句，它将成为我们缓存的基石。

如果我们已经有一个键的值，让我们返回它。如果我们有一个正在进行的承诺，返回它。如果我们没有那个键的数据，我们将触发原来的方法。这个触发器将包装它的承诺，以便我们在 resolve 上填充我们的缓存。

现在，我们将向实时功能添加时间。在我们新方法的开始，我们将添加。

如果我们解决了它，并且解决时间超过 60 秒，我们将从缓存中删除它，并继续切换我们的其余逻辑。

现在我们完成了，我们可以测试我们的代码。

你可以在这个[拨弄](https://jsfiddle.net/61pfqg43/1/)中看到控制台结果和整个代码。

如果你喜欢这篇文章，你可以在[推特](https://twitter.com/pavel_polivka)上关注我。

【https://ppolivka.com】最初发表于[](https://ppolivka.com/posts/reusing-promises-in-javascript)**。**

**更多内容请看**[***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。******