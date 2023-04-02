# 你应该知道的 7 个强大的 JavaScript 字符串方法

> 原文：<https://javascript.plainenglish.io/7-powerful-javascript-string-methods-that-you-should-know-b2ec3eec02ae?source=collection_archive---------6----------------------->

## JavaScript 中你需要知道的有用的字符串方法。

![](img/aa21341c13712f7c11be999c6f9cfdbb.png)

Photo by [Jexo](https://unsplash.com/@jexo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如今，JavaScript 是软件开发中最好和最流行的编程语言之一。作为开发人员，你可以单独用 JavaScript 做很多事情。网站、网络应用、移动应用、游戏、人工智能等等。

JavaScript 有很多很酷的特性和内置方法，您可以使用它们来轻松完成任务并加快开发速度。JavaScript 中有一些方法可以操作数组、对象、字符串和其他数据类型。你不必记住所有可用的方法。当你忘记某事时，谷歌将是你最好的朋友。

在这篇文章中，我会给你一些有用的 JavaScript 字符串方法的列表，这些方法会对你有很大的帮助。所以让我们开始吧。

# 1.切片法

方法`slice()`是一个字符串方法，允许我们复制和提取部分字符串。因此，它在新字符串中返回提取的部分。您也可以对数组使用此方法。

方法`slice()`接受两个参数:

*   起始索引(要开始的字符的索引)。
*   结束索引(要结束的字符的索引)。

这里有一个例子:

```
const str = "JavaScript is Awesome";str.**slice(0, 10)**; //returns "JavaScript"
```

在上面的例子中，我们使用了方法`slice`,我们给它传递了两个参数来从一个指定的索引到另一个索引提取字符串的一部分。

如果你愿意，也可以只传递一个参数。因此，它将从该索引参数中提取字符串，直到该字符串的最后一个索引。

这里有一个例子:

```
const str = "JavaScript is Awesome";str.**slice(14)**; //returns "Awesome"str.**slice(-7)**; //returns "Awesome"
```

如您所见，如果您愿意，您也可以传递负数，该方法将从字符串的末尾开始提取。

# 2.concat 方法

方法`concat()`允许将字符串连接和组合在一起。这就像使用一元运算符`+`进行字符串连接一样。

这里有一个例子:

```
const tool = "JavaScript";tool.**concat(" is Awesome.")**; //returns "JavaScript is Awesome."tool.**concat(" Hello", " World")**; //returns "JavaScript Hello World"
```

正如您所看到的，该方法返回一个新的连接字符串，如果您愿意，可以向它传递多个字符串。

# 3.拆分方法

JavaScript 中的方法`split()`允许我们将一个字符串拆分成一个数组。它让我们能够在 JavaScript 中将字符串转换成数组。

这里有一个例子:

```
const str = "JavaScript is Awesome";//convert to an array of single characters.
str.**split("")**;
// returns ["J", "a", "v", "a", "S", "c", "r", "i", "p", "t", " ", "i", "s", " ", "A", "w", "e", "s", "o", "m", "e"]//convert to an array of words.
str.**split(" ")**; //returns ["JavaScript", "is", "Awesome"]//get the first two words inside an array.
str.**split(" ", 2)**; //returns ["JavaScript", "is"]
```

如您所见，该方法最多可以接受两个参数，允许您按照自己的方式将字符串拆分成数组。

# 4.该方法包括

方法`includes()`检查一个字符串是否包含您作为该方法的参数传递的另一个特定字符串。如果是，则返回`true`。否则返回`false`。

下面是一个例子:

```
const str = "JavaScript is Awesome";str.**includes("JavaScript")**; //returns truestr.**includes("Python")**; //returns false
```

# 5.charCodeAt 方法

方法`charCodeAt()`返回字符串中指定字符的 Unicode 编码。

您只需将想要获取其 Unicode 编码的字符的索引作为参数传递给该方法。

这里有一个例子:

```
const str = "JavaScript is Awesome";str.**charCodeAt(0)**; //returns 74str.**charCodeAt(2)**; //returns 118
```

正如您在上面看到的，该方法返回指定字符的 Unicode 值。当我们将 0 作为参数传递时，它返回字符串中第一个字母的 Unicode 值，也就是 Unicode 值为 74 的字母“J”。另一方面，当我们将 2 作为参数传递时，它返回 118，因为字母“v”的 Unicode 值是 118。

# 6.CharCode 的方法

方法`fromCharCode()`允许我们将 Unicode 值转换成人类可读的字符。因为这个方法是 String 对象的一部分，所以我们使用关键字`String`来访问它。

这里有一个例子:

```
String.**fromCharCode(77)**; //returns "M"String.**fromCharCode(65)**; //returns "A"String.**fromCharCode(74, 65, 118, 65)**; //returns "JAVA"
```

如果您想使用 JavaScript 将字符串从二进制转换为普通文本，这个方法非常有用。

# 7.方法 replaceAll

方法`replaceAll()`是 ES2020 的一种新方法。它允许我们用另一个作为参数传递的特定字符串替换一个字符串的多个实例。

我们可以使用普通字符串或全局正则表达式来替换所有实例。您甚至可以传递一个函数来操作所有实例。

方法`replaceAll()`接受两个参数:

1.  要用某物替换的字符串的实例。
2.  将替换实例的字符串(也可以传递普通字符串或函数)。

这里有一个例子:

```
const str = "Hello Hello JavaScript";str.**replaceAll(****/Hello/g, "Hi")**; //returns "Hi Hi JavaScript"str.**replaceAll("Hello", "Hi")**; //returns "Hi Hi JavaScript"str.**replaceAll("Hello", (i) => i + " World")**;
//returns "Hello World Hello World JavaScript"
```

因此，该方法返回一个新的字符串，其中包含我们替换的所有新实例。

# 结论

如您所见，在 JavaScript 中处理字符串时，上述方法非常有用。它们真的节省了你的时间，帮助你用 JavaScript 创造出令人惊叹的东西。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读:**

[](/javascript-hoisting-explained-with-examples-2dd571f780b) [## JavaScript 提升举例说明

### JavaScript 中提升的概念比您想象的要简单。

javascript.plainenglish.io](/javascript-hoisting-explained-with-examples-2dd571f780b) [](/7-awesome-css-tools-for-all-web-developers-390ceced6f83) [## 面向所有 Web 开发人员的 7 款出色的 CSS 工具

### 有用的 CSS 工具，让您的生活更轻松，提高您的生产力。

javascript.plainenglish.io](/7-awesome-css-tools-for-all-web-developers-390ceced6f83) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)