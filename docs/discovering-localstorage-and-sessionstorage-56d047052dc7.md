# 在 JavaScript 中发现 Web 存储 Api

> 原文：<https://javascript.plainenglish.io/discovering-localstorage-and-sessionstorage-56d047052dc7?source=collection_archive---------13----------------------->

![](img/6023d42bab3cad6b5e8561184ee0abde.png)

## JavaScript web 存储对象，`localStorage`和`sessionStorage,`允许在浏览器中保存键/值对

# 介绍

`localStorage`是用户浏览器上可用的键/值数据存储。和 cookies 一样，`localStorage`只能为它的键和值存储字符串数据。该数据存储只能由该域中的 JavaScript 访问。

Cookies 仍然有用，特别是对于认证，但是有时候使用`localStorage`或`sessionStorage`可能是更好的选择。

所有现代浏览器都支持`localStorage`或`sessionStorage`，你现在可以毫无问题地使用它们。

# 什么是 Web 存储 API？

Web 存储 API 是一组使浏览器能够存储键/值对的机制。它被设计得比使用 cookies 更直观。

键/值对表示存储对象，它类似于对象，只是在页面加载期间保持不变，并且始终是字符串。您可以像访问一个对象一样访问这些值，或者使用`getItem()`方法(稍后会详细介绍)。

# 本地存储与 Cookies

如前所述，`localStorage`与 cookies 的相似之处在于，两种机制都可以用来在 HTTP 请求之间在浏览器中存储数据。但是`localStorage`和饼干是有区别的。

Cookies 是服务器可以存储在浏览器中的小块数据。浏览器将 cookie 和所有将来的 HTTP 请求一起发送到设置 cookie 的服务器。Cookies 的总大小不能超过 4KB。

> `localStorage`通过浏览器中执行的 JavaScript 进行设置。

`localStorage`属性永远不会被发送到任何服务器——除非您显式地将它们从`localStorage`中复制出来并附加到 AJAX 请求中。

`localStorage`可在浏览器中存储 2MB 至 10MB 的数据(根据来源-域名)。具体允许多少数据取决于浏览器。

> 5MB 到 10MB 的限制是最常见的。

# `localStorage`和`sessionStorage`的区别

`localStorage`和`sessionStorage`非常相似，都有相同的 API。

主要区别在于使用`sessionStorage`时，数据只保存到窗口或标签关闭。

使用`localStorage`，数据将被持久化，直到用户手动清除浏览器缓存，或者直到您的 web 应用程序清除数据。

在本教程中，我们看到了一些使用`localStorage api`的例子，创建、读取和更新键/值对，但是您可以将这些原则应用于使用`sessionStorage`编写代码。

# 创建新项目

您可以使用`setItem()`方法为`localStorage`对象创建条目。

对于`setItem()`方法，我们需要传递两个参数，即`key`和我们想要保存的值:

# 阅读项目

要读取条目，请使用`getItem()`方法。

`getItem()`方法接受一个必须是密钥的参数。该函数将以字符串形式返回相应的值:

上面的代码将变量`myItem`设置为等于`'Value'`，这是`key`的对应值。

# 更新项目

要更新现有的条目，我们可以简单地使用我们已经使用的`setItem()`方法，它有两个参数，第一个是现有条目的键值，在我们的例子中是“greeting1”，而 value 参数是新条目:

现在，`greeting1`的`localStorage`值是`'Hello LocalStorage Again!'`而不是`'Hello LocalStorage!'`。

# 删除和清除项目

您可以使用`removeItem()`方法删除一个条目。`removeItem()`方法接受一个参数，该参数将成为`localStorage`对象的一个键:

如果您想删除存储在`sessionStorage`或`localStorage`对象中的所有属性，您可以使用`clear()`功能:

# 用 JSON 存储对象

LocalStorage 只能对其键和值使用字符串。如果我们试图存储任何其他类型的数据，它会在存储之前将其转换为字符串。当我们想要保存 JavaScript 对象时，这会带来一些意想不到的行为。

为了在 LocalStorage 中正确存储 JavaScript 对象，我们首先需要将对象转换为 JSON 字符串。

为此，我们使用内置的`JSON.stringify()`函数。该函数的结果字符串将包含我们的 JSON 对象的所有属性。当我们使用`setItem()`时，我们保存该函数的输出。

虽然`personObj`是一个对象，但是`JSON.stringify(personObj)`将它转换成一个字符串。所以`personObj`现在是一个有效的`localStorage`值。

现在我们的对象被保存为一个字符串值，所以如果我们调用`getItem()` 方法，我们将得到一个字符串，而我们的原始值是一个对象。

感谢`JSON.parse()`方法，我们可以返回到我们的原始对象，该方法获取 JSON 字符串并将它们转换成 JavaScript 对象。`JSON.parse()`以`.getItem()`为自变量:

现在`item`被设置为等于`key`的值。在前面的代码片段中，`key`的值被设置为`personObj`的字符串化版本。使用`JSON.parse`将`personObj`转换回一个对象。所以`item`被设为等于`personObj`作为对象，而不是字符串。

能够使用`JSON.stringify`将数组和对象转换成字符串，然后使用`JSON.parse`将它们转换回来是非常有用的。您还需要知道如何检查`localStorage`是否为空。

# 迭代项目

`localStorage`和`sessionStorage`对象不支持`forEach`方法。

要迭代`localStorage`中的项目，使用一个`for`循环:

迭代`localStorage`项的问题是它们是用字符串键标识的，而不是用一个渐进的数字标识的，所以当你像上面一样使用 for 循环时，你不能直接访问这些项。

解决方案很简单，来自于`key()`方法，该方法将一个整数作为参数，并返回相应的键:

使用`getItem`方法返回`key`的相应值:

创建一条`console.log`语句，将`key`和`value`打印到屏幕上:

使用`for`循环遍历`localStorage`时，`key()`非常有用。并不是所有的浏览器都支持`localStorage`。

# 检查支持

您可以通过使用`if`语句检查`window`对象上是否有`localStorage`支持来测试它:

您也可以使用[我可以使用……](https://caniuse.com/namevalue-storage)网站来检查主流浏览器对`localStorage`的支持。

# 结论

您可以使用`localStorage`或`sessionStorage`对象来存储键/值对。

有一些方法可以让您与`localStorage`中的项目进行交互。
在本教程中，您创建、删除和更新了`localStorage`中的条目。

您还使用 JSON 方法将数组和对象数据转换成字符串，然后再转换回来。

*感谢阅读！*