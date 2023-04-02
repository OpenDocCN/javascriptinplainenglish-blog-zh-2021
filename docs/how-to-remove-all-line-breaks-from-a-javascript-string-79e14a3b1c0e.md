# 如何移除 JavaScript 字符串中的所有换行符？

> 原文：<https://javascript.plainenglish.io/how-to-remove-all-line-breaks-from-a-javascript-string-79e14a3b1c0e?source=collection_archive---------7----------------------->

![](img/137d48adacb7849ce27e64afc7f2b02b.png)

Photo by [Lubo Minar](https://unsplash.com/@bubo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要在 JavaScript 应用程序中删除字符串中的所有换行符。

在本文中，我们将研究如何从 JavaScript 字符串中移除所有换行符。

# 字符串.原型.替换

我们可以用正则表达式调用`replace`方法来搜索字符串中的所有换行符，并用空字符串替换它们来移除换行符。

例如，我们可以写:

```
const trimmed = 'abc\r\ndef'.replace(/(\r\n|\n|\r)/gm, "");
console.log(trimmed)
```

删除所有换行符。

`\r`和`\n`是换行符的样式。

`g`让我们在整个字符串中搜索换行符的所有实例。

因此`trimmed`就是`'abcdef'`。

我们也可以使用控制代码字符等效物来代替`\r`和`\n` ，编写如下:

```
const trimmed = 'abc\r\ndef'.replace(/[^\x20-\x7E]/gmi, "")
console.log(trimmed)
```

`\x20`相当于`\r`。

而`\x7E`相当于`\n`。

# 字符串.原型.修剪

`trim`方法让我们从一个字符串的开头和结尾删除所有的换行符。

例如，我们可以写:

```
const trimmed = 'abc\r\n'.trim()
console.log(trimmed)
```

那么`trimmed`就是`'abc'`。

# String.prototype.trimStart

`trimStart`方法让我们从一个字符串的开头删除所有的换行符。

例如，我们可以写:

```
const trimmed = '\r\nabc'.trimStart()
console.log(trimmed)
```

那么`trimmed`就是`'abc'`。

# String.prototype.trimEnd

`trimEnd`方法让我们删除字符串末尾的所有换行符。

例如，我们可以写:

```
const trimmed = 'abc\r\n'.trimEnd()
console.log(trimmed)
```

那么`trimmed`就是`'abc'`。

# 结论

我们可以使用 string `replace`方法从一个字符串中删除所有换行符。

我们可以使用`trim`、`trimStart`或`trimEnd`方法分别从字符串的开头和结尾、开头或结尾删除换行符。