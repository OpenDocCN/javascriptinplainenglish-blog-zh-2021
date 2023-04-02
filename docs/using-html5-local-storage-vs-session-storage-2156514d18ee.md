# 使用 HTML5 本地存储与会话存储

> 原文：<https://javascript.plainenglish.io/using-html5-local-storage-vs-session-storage-2156514d18ee?source=collection_archive---------11----------------------->

![](img/6392b6003932a0e87b942ea815f1ca52.png)

Photo by [Carson Masterson](https://unsplash.com/@carsonmasterson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对于现代浏览器，至少提供了两种用于少量文本数据的客户端存储。

一个是本地存储，另一个是会话存储。

它们在我们的 JavaScript web 应用程序中有不同的用途。

在本文中，我们将看看它们之间的区别。

我们还会看看如何在 JavaScript 代码中使用它们。

# 本地存储和会话存储之间的差异

本地存储和会话存储服务于不同的目的。

本地存储允许我们存储数据，直到它们被删除。

他们留在这个领域。

和将来对该站点的所有访问都是可用的。

会话存储更改仅适用于每个选项卡。

所做的更改只有在该选项卡关闭后才可用。

一旦关闭，存储的数据将被删除。

# 使用本地存储

要使用本地存储，我们可以调用`localStorage`方法中的方法来获取和设置数据。

要添加数据，我们调用`localStorage.setItem`方法，该方法分别接受一个字符串键和相应的值。

键和值都应该是字符串。

如果它们不是字符串，那么它们将被转换成字符串。

为了得到数据，我们用这个键调用`localStorage.getItem`。

它返回对应于给定键的值。

并且为了清除所有本地存储数据，我们调用`localStorage.clear`。

要用给定的键删除本地存储项，我们调用`localStorage.removeItem`。

例如，我们可以这样使用它:

```
localStorage.setItem('foo', 'bar')
console.log(localStorage.getItem('foo'))
```

`'foo'`是键，`'bar'`是对应的值。

我们可以通过编写以下内容来删除带有`removeItem`的项目:

```
localStorage.setItem('foo', 'bar')
localStorage.removeItem('foo')
console.log(localStorage.getItem('foo'))
```

`getItem`应该返回`null`，因为我们用键`'foo'`删除了条目。

我们可以调用`clear`来清除所有本地存储条目:

```
localStorage.setItem('foo', 'bar')
localStorage.clear()
```

# 使用会话存储

要操作会话存储，我们只需用`sessionStorage`移除`localStorage`。

所以我们可以写:

```
sessionStorage.setItem('foo', 'bar')
console.log(sessionStorage.getItem('foo'))
```

使用`setItem`将项目添加到会话存储器中

`'foo'`是键，`'bar'`是相应的值。

我们可以通过编写以下内容来删除带有`removeItem`的项目:

```
sessionStorage.setItem('foo', 'bar')
sessionStorage.removeItem('foo')
console.log(sessionStorage.getItem('foo'))
```

`getItem`应该会返回`null`，因为我们删除了带有关键字`'foo'`的条目。

我们可以调用`clear`来清除所有的会话存储条目:

```
sessionStorage.setItem('foo', 'bar')
sessionStorage.clear()
```

# 结论

我们可以使用本地存储或会话存储来存储少量的文本数据。

本地存储数据在被删除之前会一直保存，并在整个站点中可用。

会话存储数据仅在当前选项卡中可用，并在选项卡关闭后被删除。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*