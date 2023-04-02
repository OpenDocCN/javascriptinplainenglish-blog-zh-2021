# 如何在 JavaScript 中替换特定索引处的字符？

> 原文：<https://javascript.plainenglish.io/how-to-replace-a-character-at-a-particular-index-in-javascript-3375246c0ff8?source=collection_archive---------6----------------------->

![](img/0fbd421e049f507a272f864403eef1da.png)

Photo by [Yiqun Tang](https://unsplash.com/@equeen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要替换 JavaScript 字符串中特定索引处的字符。

在本文中，我们将研究如何用 JavaScript 替换特定索引处的字符。

# 使用 String.prototype.substr 方法

我们可以用`substr`方法从字符串中提取子字符串。

这将有助于我们进行替换，因为我们可以从索引 0 到想要替换的字符的索引提取子字符串。

我们可以从索引中提取字符串到字符串的末尾。

然后我们可以在两个子字符串之间添加替换。

例如，我们可以写:

```
const replaceAt = (str, index, replacement) => {
  return str.substr(0, index) + replacement + str.substr(index + 1);
}const str = 'a b c'
const newStr = replaceAt(str, 2, 'foo')
console.log(newStr)
```

我们创建了`replaceAt`函数，它接受我们想要替换的`str`字符串。

我们想要替换的字符的`index`。

而`replacement`是替换字符串。

然后，我们返回第一个子串与第二个子串连接的`replacement`。

所以当我们向它传递参数时，我们得到了`newStr`，它是:

```
'a foo c'
```

`substr`和`substring`方法是相同的，所以我们可以这样写:

```
const replaceAt = (str, index, replacement) => {
  return str.substring(0, index) + replacement + str.substring(index + 1);
}const str = 'a b c'
const newStr = replaceAt(str, 2, 'foo')
console.log(newStr)
```

我们可以用它将任何字符替换成另一个任意长度的子串。

# String.prototype.split 和 String.prototype.join

我们也可以使用`split`和`join`方法来拆分和连接一个字符串。

例如，我们可以写:

```
let str = 'a b c'
str = str.split('');
str[2] = 'd';
str = str.join('');
console.log(str)
```

我们用一个空字符串调用`split`，将字符串拆分成一个字符数组。

然后我们用一个新的字符给给定索引的字符串的字符赋值。

然后我们用`join`方法和一个空字符串作为参数将字符串连接起来。

所以`str`应该是`'a d c’`。

这对于用一个字符替换另一个字符很方便。

# 结论

要用另一个子串替换一个字符，我们可以将这个字符串拆分成子串。

然后我们可以用替代品把它们重新连接起来。

我们也可以将一个字符串拆分成一个字符数组，将该位置的字符赋给另一个字符。

然后我们可以把绳子重新连在一起。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*