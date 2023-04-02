# 如何替换 JavaScript 字符串的所有匹配项

> 原文：<https://javascript.plainenglish.io/how-to-replace-all-occurrences-of-a-javascript-string-2c397c0418a2?source=collection_archive---------17----------------------->

![](img/e49c558703fca58a9b8b0a26df080476.png)

Photo by [Dan Gold](https://unsplash.com/@danielcgold?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 应用程序中，替换所有出现的字符串是我们经常要做的事情。

在本文中，我们将研究如何替换 JavaScript 应用程序中出现的所有字符串。

# 字符串.原型. replaceAll

`replaceAll`方法是一种新方法，从 ES2021 开始，它就成为 JavaScript 字符串的一部分。

许多最新的浏览器都支持它，如 Chrome、Edge 或 Firefox。

为了使用它，我们写:

```
const result = "1 abc 2 abc 3".replaceAll("abc", "def");
```

第一个参数是我们要替换的字符串。

第二个参数是我们想要替换的字符串。

因此，`result`就是`'1 def 2 def 3'`。

# 拆分和合并

我们也可以用我们想要替换的字符串来分割一个字符串，并用我们想要替换原始字符串的字符串来调用`join`，

例如，我们可以写:

```
const result = "1 abc 2 abc 3".split("abc").join("def");
```

用`'abc'`作为分隔符拆分字符串，用`'def'`调用`join`。

我们得到了相同的结果。

# 正则表达式替换

我们可以用新的字符串替换给定模式的字符串。

例如，我们可以写:

```
const result = "1 abc 2 abc 3".replace(/abc/g, 'def');
```

用`'def'`替换所有实例`'abc'`。

`g`标志意味着我们寻找具有给定模式的所有实例。

我们也可以使用`RegExp`构造函数来创建我们的 regex 对象:

```
const result = "1 abc 2 abc 3".replace(new RegExp('abc', 'g'), 'def');
```

# While 循环并包含

我们可以使用`includes`方法来检查一个字符串是否有给定的子串。

所以如果它有一个给定的子串，`includes`将返回`true`。

因此，我们可以将它与`while`循环一起使用，通过在条件中使用`includes`用一个新的子字符串替换一个子字符串的所有实例。

例如，我们可以写:

```
let str = "1 abc 2 abc 3";
while (str.includes("abc")) {
  str = str.replace("abc", "def");
}
```

我们使用`let`来重新赋值。

唯一的缺点是我们必须改变变量`str`。

# 结论

在 JavaScript 中，用另一个子字符串替换一个子字符串的所有实例有很多种方法。

替换所有子字符串的最新且更简单的方法是使用 ES2021 附带的`replaceAll`方法，该方法可用于最新的浏览器。

*更多内容看* [***说白了***](https://plainenglish.io/)