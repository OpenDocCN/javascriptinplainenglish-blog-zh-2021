# 你应该知道的最好的 JavaScript ES2019 方法

> 原文：<https://javascript.plainenglish.io/best-javascript-es2019-methods-that-you-should-know-380cf370c5?source=collection_archive---------5----------------------->

## 通过示例了解一些有用的 ES2019 方法。

![](img/71359370c8489be7b546316594a37574.png)

Photo by [Filiberto Santillán](https://unsplash.com/@filisantillan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如今，JavaScript 是每个 web 开发人员的必修编程语言。每年，我们都有新的特性被添加到语言中，以使开发人员的工作变得更容易。在过去的几年里，JavaScript 生态系统发生了很多改进。

ES2019 版本提供了许多有用的新功能，我们可以在 JavaScript 中使用它们。所以我们应该利用这些特性来加速开发过程。

在本文中，我们将发现一些你应该知道的有用的 JavaScript ES2019 方法。让我们开始吧。

# 1.扁平法

方法`flat()`是 JavaScript ES2019 中发布的很酷的特性之一。它用于展平多维数组。

方法`flat()`采用一个可选参数(number)，它表示我们希望将多维数组展平到什么程度。如果没有传递参数，默认情况下扁平化的级别是 1。

让我们看一个简单的例子:

```
let names = ["Mehdi", ["John", "Alex"], "James"];
names.**flat()**; //returns: ["Mehdi", "John", "Alex", "James"]let level2 = ["Mehdi", **[[**"John", "Alex"],["Brad", "Anna"**]]**,"James"]level2.**flat();** //["Mehdi",["John", "Alex"],["Brad", "Anna"],"James"]
level2.**flat(2);** //["Mehdi", "John", "Alex", "Brad", "Anna", "James"]
```

正如您所看到的，您可以根据数组的深度将扁平化的级别作为参数传递给函数。还有其他方法来展平数组，但是方法`flat()`是最简单的方法。

# 2.trimStart()和 trimEnd()方法

ES2019 还增加了两个有用的弦乐方法`trimStart()`和`trimEnd()`。这些方法允许我们修剪或删除字符串开头和结尾的空白。

因此，如果您想删除字符串开头的空格，可以使用方法`trimStart()`:

```
let ourStr = "  Hello JavaScript ";
ourStr.**trimStart()**; //output: "Hello JavaScript "
```

如果你想删除字符串末尾的空白，使用方法`trimEnd()`:

```
let ourStr = "Hello JavaScript   ";
ourStr.**trimEnd()**; //output: "Hello JavaScript"
```

如果你想删除两边的空白，你可以使用 ES2019 之前已经可用的方法`trim()`:

```
let ourStr = "  JavaScript is Awesome   ";
ourStr.**trim()**; //output: "JavaScript is Awesome"
```

# 3.Object.fromEntries()

方法`Object.fromEntries()`是 ES2019 中发布的一个很酷的功能。它允许我们将键和值对的数组或列表转换成一个对象。

这里有一个例子:

```
let keyValue = [["name", "John"], ["age", 19]];
const obj = **Object.fromEntries(keyValue)**;console.log(obj); //prints: {name: "John", age: 19}
```

您可以在 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/fromEntries)中了解关于此方法的更多信息。

# 结论

如你所见，这些是 ES2019 非常重要的方法。它们绝对有用，而且总有你需要使用它们的时候。

感谢您阅读这篇文章。希望你觉得有用。

**延伸阅读**

[](/4-useful-javascript-es2020-features-that-you-should-know-5d690430cf6e) [## 您应该知道的 4 个有用的 JavaScript ES2020 特性

### 您应该知道的强大 ES2020 功能。

javascript.plainenglish.io](/4-useful-javascript-es2020-features-that-you-should-know-5d690430cf6e) 

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)