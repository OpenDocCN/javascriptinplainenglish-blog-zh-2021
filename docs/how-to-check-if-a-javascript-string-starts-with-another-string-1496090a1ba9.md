# 如何检查一个 JavaScript 字符串是否以另一个字符串开头？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-javascript-string-starts-with-another-string-1496090a1ba9?source=collection_archive---------13----------------------->

![](img/512edde7dfde0389e5158c2d507afdaa.png)

Photo by [Sarra Marzguioui](https://unsplash.com/@geist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时我们必须检查 JavaScript 字符串是否以给定的子字符串开头。

在本文中，我们将看看如何检查一个 JavaScript 字符串是否以另一个字符串开头。

# string . prototype . starts

ES6 将`startsWith`方法添加到一个字符串中。

例如，我们可以写:

```
console.log("hello world".startsWith("hello"));
```

我们在字符串上调用`startsWith`,并传入想要检查`'hello world'`字符串是否以它开头的子字符串。

控制台日志应该显示`true`，因为`'hello world'`从`'hello'`开始。

# 字符串.原型.子字符串

检查字符串是否以给定子串开头的另一种方法是使用`substring`方法。

它将开始和结束索引作为参数。

它返回从起始索引开始到结束索引减 1 的子字符串。

因此，我们可以这样写:

```
const data = 'hello world'
const input = 'hello'
console.log(data.substring(0, input.length) === input)
```

`data`是完整的字符串。

`substring`有参数 0 和`input.length`来提取从索引 0 到`input.length — 1`的子串。

所以`subtring`应该返回`'hello'`，和`input`一样。

# 正则表达式测试

我们可以用 JavaScript regex 对象的`test`方法搜索给定的模式。

我们可以通过使用`^`符号开始搜索字符串开头的模式来检查字符串是否以给定子串开头。

例如，我们可以写:

```
console.log(/^hello/.test('hello world'))
```

检查`'hello world'`是否从`hello`开始。

同样，我们可以使用`RegExp`构造函数来创建 regex 对象:

```
console.log(new RegExp('^hello').test('hello world'))
```

这让我们可以传入一个 regex 字符串来创建 regex 对象，而不是创建一个 regex 文字。

所以动态创建 regex 对象很方便。

# String.prototype. `lastIndexOf`

JavaScript 字符串还附带了`lastIndexOf`方法来检查字符串中给定子串的最后一个索引。

要使用它来检查一个字符串是否以给定的子字符串开始，我们可以写:

```
console.log('hello world'.lastIndexOf('hello', 0) === 0)
```

像第一个参数一样，我们用要搜索的子串调用`lastIndexOf`。

第二个参数是我们开始搜索子字符串的索引。

如果它返回 0，那么我们知道子串位于索引 0，并从那里开始。

# String.prototype. `indexOf`

我们可以用`indexOf`替换`lastIndexOf`来获得相同的行为。

而不是用`lastIndexOf`搜索子串的最后一个实例。

我们可以用`indexOf`搜索一个子串的搜索实例。

这对我们来说没什么区别，因为我们只想知道一个字符串是否以给定的子字符串开头。

例如，我们可以写:

```
console.log('hello world'.indexOf('hello', 0) === 0)
```

去做检查。

# 结论

我们可以使用许多 JavaScript 字符串方法来检查一个字符串是否以给定的子字符串开头。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)