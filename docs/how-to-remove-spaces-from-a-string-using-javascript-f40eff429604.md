# 如何使用 JavaScript 删除字符串中的空格？

> 原文：<https://javascript.plainenglish.io/how-to-remove-spaces-from-a-string-using-javascript-f40eff429604?source=collection_archive---------20----------------------->

![](img/ce03de4cd4b28c5374748da8dc34014e.png)

Photo by [Jeremy Thomas](https://unsplash.com/@jeremythomasphoto?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在很多情况下，我们可能想用 JavaScript 删除字符串中的空格。

在本文中，我们将看看如何用 JavaScript 删除字符串中的空格。

# 用正则表达式搜索空格并替换它们

我们可以用 regex 搜索空格，并用 JavaScript 字符串的`replace`方法替换它们。

例如，我们可以写:

```
const result = ' abc '.replace(/ +/g, '');
console.log(result)
```

使用`replace`方法删除一个或多个空格。

我们只是有一个空格，后面有一个加号，用来搜索一个或多个空格。

然后`g`标志让我们搜索一个字符串中空格的所有实例。

因此，`result`应该是`'abc'`。

或者，我们可以搜索一个或多个空间的实例，并替换为:

```
const result = ' abc '.replace(/\s+/g, '');
console.log(result)
```

此外，我们可以搜索单个空格的实例，并替换为:

```
const result = ' abc '.replace(/ /g, '');
console.log(result)
```

我们得到了同样的结果。

同样，我们可以使用`\s`模式来搜索单个空格并替换它们。

例如，我们可以写:

```
const result = ' abc '.replace(/\s/g, '');
console.log(result)
```

得到同样的结果。

替换所有空白空间的最快方法是:

```
const result = ' abc '.replace(/ /g, '');
console.log(result)
```

对于短弦。

对于长字符串:

```
const result = ' abc '.replace(/ +/g, '');
console.log(result)
```

是最快的。

# 字符串.原型. split

我们也可以使用空格作为分隔符，用`split`方法分割字符串。

然后我们用`join`把分开的字符串数组重新连接在一起。

例如，我们可以写:

```
const result = ' abc '.split(' ').join('');
console.log(result)
```

我们得到了和前面例子一样的结果。

# 结论

我们可以使用带有正则表达式的`replace`方法来搜索所有空格，并用空字符串替换它们，以删除字符串中的所有空格。

此外，我们可以使用`split`方法通过空白字符串分割一个字符串，然后用`join`将它连接起来，做同样的事情。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)