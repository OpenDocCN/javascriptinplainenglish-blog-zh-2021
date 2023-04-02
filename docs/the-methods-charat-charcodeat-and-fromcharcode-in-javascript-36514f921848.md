# JavaScript 中的 charAt、charCodeAt 和 fromCharCode 方法

> 原文：<https://javascript.plainenglish.io/the-methods-charat-charcodeat-and-fromcharcode-in-javascript-36514f921848?source=collection_archive---------2----------------------->

## charAt VS charcode at VS from charcode

![](img/52ea60cc3cc00efca599aa813c17bc7e.png)

Photo by [Tudor Baciu](https://unsplash.com/@baciutudor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，charAt()、charCodeAt()和 fromCharCode()都是可以使用的有用的字符串方法。它们在语法上可能看起来相似，但是每一个都有不同的作用，并允许我们以不同的方式处理字符串。

在 JavaScript 中，总会有需要使用这些方法的情况。这就是为什么你作为一个开发者需要了解他们。

在本文中，我们将通过介绍这三种方法之间的区别来了解它们。让我们开始吧。

# 字符法

方法`charAt()`允许我们通过指定一个字符串的索引来轻松地从该字符串中获取一个字符。该方法接受一个参数(索引)并返回字符串中指定索引处的字符。

这里有一个例子:

```
let ourSentence = "JavaScript is super awesome";//get the first character of the string.
ourSentence.charAt(0); //returns "J"//the second character of the string.
ourSentence.charAt(1); //returns "a"//get the last character of the string.
ourSentence.charAt(ourSentence.length - 1); //returns "e"
```

如您所见，方法`charAt()`允许我们通过在字符串上指定它的索引来轻松地获得我们想要的任何字符。另外，请记住，如果您传递了一个不存在的索引，该方法将返回一个空字符串。

在下面的例子中，方法`charAt()`返回一个空字符串，因为没有找到索引号。

```
let ourSentence = "JavaScript is super awesome"; ourSentence.charAt(100); //returns an empty string ""
```

请务必传递有效的索引。另外，方法`charAt()`的好处是它在所有浏览器中都得到完全支持。

# charCodeAt 方法

方法`charCodeAt()`允许我们获取字符串中字符的 Unicode 值。每个字符都有自己特定的 Unicode。例如，字母`H`的 Unicode 值为 72。

该方法接受一个参数(字符的索引)并返回字符串中字符的 Unicode 值。除此之外，所有的浏览器都支持方法`charCodeAt()`,这很好。

看看下面的例子:

```
let ourSentence = "JavaScript is super awesome";//get the Unicode of the first character(J).
ourSentence.charCodeAt(0); //returns 74//the Unicode of the second character(a).
ourSentence.charCodeAt(1); //97//get the Unicode of the last character(e).
ourSentence.charCodeAt(ourSentence.length - 1); //returns 101
```

正如您在上面看到的，方法`charCodeAt()`允许我们轻松地获得字符串中每个字符的 Unicode 值。

同样，总是确保传递一个有效的索引。因为如果不这样做，方法会返回`NaN`来代替。

这里有一个例子:

```
let ourSentence = "JavaScript is super awesome";ourSentence.charCodeAt(200); //returns NaN
```

在上述情况下，该方法没有找到索引。这就是它返回`NaN`而不是 Unicode 值的原因。

# fromCharCode 方法

方法`fromCharCode`允许我们轻松地将任何 Unicode 值转换成字符。与方法`charCodeAt()`相反。

该方法接受一个必需的参数(Unicode 值),如果您想组成一个单词或句子，也可以传递多个 Unicode。

该方法通过带点符号的对象`String`访问。

下面是一个例子:

```
String.fromCharCode(74); //returns "J"
String.fromCharCode(118); //returns "v"//multiple arguments.
String.fromCharCode(74, 65, 118, 65); //returns "JAvA"
```

如您所见，您可以传递一个或多个 Unicode 值作为参数，该方法会将其转换为字符。

# charAt VS charcode at VS from charcode

*   方法`charAt()`通过指定索引从字符串中返回一个字符。
*   `charCodeAt()`返回字符串中指定字符的 Unicode 值。
*   方法`fromCharCode`将 Unicode 值转换成字符。

这就是 JavaScript 中这三个有用方法的区别。

# 结论

正如您在上面几节中看到的，这些方法对于字符串非常有用。您需要知道它们之间的区别以及如何在您的 JavaScript 代码中使用它们。此外，这些方法有许多用例，例如将二进制文本转换为普通文本。

*感谢您阅读这篇文章。此外，如果你觉得我的内容有用，而你不是一个媒体成员，你可以抓住你的媒体成员* [*这里*](https://mehdiouss.medium.com/membership) *(媒体推荐链接)获得所有内容的无限访问和支持我们作为作家。*

**延伸阅读:**

[](/7-useful-javascript-code-snippets-for-solving-coding-problems-c146e768bb41) [## 解决编码问题的 7 个有用的 JavaScript 代码片段

### 您经常需要使用的 JavaScript 代码片段。

javascript.plainenglish.io](/7-useful-javascript-code-snippets-for-solving-coding-problems-c146e768bb41) [](https://blog.devgenius.io/5-useful-books-for-software-developers-a5f405efe33e) [## 对软件开发人员有用的 5 本书

### 帮助你成为一名成功的开发人员的优秀书籍列表。

blog.devgenius.io](https://blog.devgenius.io/5-useful-books-for-software-developers-a5f405efe33e) 

*原载于 2021 年 7 月 30 日 https://webdevidea.com*[](https://webdevidea.com/blog/charat-charcodeat-and-fromcharcode-in-javascript/)**。**