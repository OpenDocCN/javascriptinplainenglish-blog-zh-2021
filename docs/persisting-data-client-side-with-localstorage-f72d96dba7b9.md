# 使用本地存储在客户端保存数据

> 原文：<https://javascript.plainenglish.io/persisting-data-client-side-with-localstorage-f72d96dba7b9?source=collection_archive---------18----------------------->

![](img/1a8de465dc4f3aab87a4b166d675e5e8.png)

Photo by [JOSHUA COLEMAN](https://unsplash.com/@joshstyle?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是 localStorage？

你问什么是本地存储？嗯，localStorage 只是一个 Javascript 对象。但这还不是全部。它是美国开发者用来在客户端本地存储数据的 Web 存储 API 的一部分。localStorage 对象是用于在客户机(浏览器)上存储数据的两个对象之一。这些是`localStorage`和`sessionStorage`对象。

这两种类型的存储对象之间的主要区别在于，localStorage 用于在浏览器打开时存储数据，也用于在浏览器未打开时存储数据，这意味着在浏览器关闭后数据会被持久化。使用 sessionStorage，您的数据存储仅在浏览器仍然打开时可用。

那么为什么要使用 localStorage 或者 sessionStorage 呢？

在 HTML5 出现之前，只有 cookies 被用来存储数据。Cookies 在每次请求时都发送到服务器，它们提供的存储空间(大约 4kb)和安全性都比 localStorage 和 sessionStorage 低。使用 localStorage，存储数据最多有 5MB 的空间，并且没有到期日期。

# 何时使用 localStorage

每当您希望客户端数据持久化，这样它就不会像会话一样在页面重新加载时消失，那么 localStorage 就是一个很好的选择。例如，如果您正在构建一个 chrome 扩展，您可能希望您的扩展能够存储数据并在页面刷新时可用。

# 如何使用本地存储

要使用 localStorage，我们必须首先通过全局`window`对象访问它。当我们从`window`对象调用 localStorage 时，我们得到的是`Storage`对象的一个实例，它允许我们设置、获取和删除会话和本地存储类型的数据项。

```
> window.localStorage
► Storage {length: 0}
```

为了简单起见，我们在这里只使用一个变量来引用我们的`window.localStorage`。

```
const myLocalStorage = window.localStorage
```

要开始使用我们的 localStorage，让我们快速浏览一下它可用的五种不同方法。

*   `setItem()`设置要存储为本地存储字符串的键/值对
*   `getItem()`通过引用键从 localStorage 获取数据项
*   `removeItem()`通过键从本地存储中删除特定数据项
*   完全清除本地存储
*   `key()`接受一个索引号来获取本地存储中的一个键的名称

让我们使用`myLocalStorage`来看看这些方法中的一些。

```
// set up localStorage key and value
myLocalStorage.setItem("Name", "Tim Berners-Lee");// retrieve the Name value
myLocalStorage.getItem("Name"); // Tim Berners-Lee// access the Name key
myLocalStorage.key(0) // Name
```

现在我们的 localStorage 如下所示:

```
► Storage {Name: "Tim Berners-Lee", length: 1}
```

然后，如果我们想从本地存储中删除数据，我们可以使用`removeItem()`方法删除特定的数据项或`clear()`，这将完全清空存储。在这种情况下，两者的作用是一样的，因为我们只需要删除一个键/值对。

```
myLocalStorage.removeItem("Name")
// Or
myLocalStorage.clear()
```

这将从`myLocalStorage`中删除我们的键/值对:

```
► Storage {length: 0}
```

如果我们想在`myLocalStorage`中存储其他数据类型，而不仅仅是硬编码字符串作为值，会怎么样？这就是`[JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify)`和`[JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)`的用武之地。让我们将之前的数据项存储为添加了另一个属性的对象，然后将该对象转换为 JSON 字符串并将其传递给`setItem()`:

```
const inventorOfTheWeb = {
    name: "Tim Berners-Lee",
    organization: "W3C"
}localStorage.setItem("person", JSON.stringify(inventorOfTheWeb))
```

现在，我们的存储将如下所示:

```
► Storage {person: 
"{'name':'Tim Berners-Lee','organization':'W3C'}", length: 1}
```

如果我们需要从存储中检索我们的`person`，我们可以使用`JSON.parse()`解析它，将它构造回一个对象:

```
let storedPerson = JSON.parse(localStorage.getItem("person"))
```

# 结论

在本文中，我们回顾了使用 localStorage 在 web 上存储数据的基础知识。我们还简要提到了会话存储和 cookies 的其他数据存储方式。

其中每一种都有自己的用例，所以在为应用程序选择实现哪一种时，将取决于您的具体情况。

如果您需要在客户端存储没有截止日期的数据，并且需要更大的存储容量，那么本地存储可能是一个不错的选择！

*更多内容请看*[***plain English . io***](http://plainenglish.io)