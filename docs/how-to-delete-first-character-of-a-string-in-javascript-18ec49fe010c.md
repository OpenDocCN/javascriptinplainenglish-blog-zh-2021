# JavaScript 中如何删除一个字符串的第一个字符？

> 原文：<https://javascript.plainenglish.io/how-to-delete-first-character-of-a-string-in-javascript-18ec49fe010c?source=collection_archive---------10----------------------->

![](img/b8230f074ff69876d73b6190fd96891f.png)

Photo by [Ines Monnet](https://unsplash.com/@imonnet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候我们需要用 JavaScript 去掉一个字符串的第一个字符。

在本文中，我们将研究如何用 JavaScript 删除字符串的第一个字符。

# 字符串.原型.子字符串

我们可以使用 JavaScript 字符串的`substring`方法从字符串中提取子字符串。

我们分别传入开始和结束索引参数。

开始索引处的字符包括在内，但结束索引处的字符不包括在内。

结束索引是可选的。

如果我们不包括它，那么结束索引就是字符串的`length`属性值。

例如，我们可以写:

```
const str = "foobar";
const newStr = str.substring(1);
console.log(newStr)
```

那么`newStr`就是`'oobar'`。

# 字符串.原型.切片

JavaScript 字符串的`slice`方法也让我们从字符串中获取子字符串。

它采用相同的参数，它们的用法与`substring`相同。

例如，我们可以写:

```
const str = "foobar";
const newStr = str.slice(1);
console.log(newStr)
```

我们得到了同样的结果。

`slice`也采用负指标。

Index -1 是字符串最后一个字符的索引，-2 是字符串倒数第二个字符的索引，依此类推。

因此，要使用负索引调用`slice`来提取从第一个字符到字符串末尾的子字符串，我们编写:

```
const str = "foobar";
const newStr = str.slice(-str.length + 1);
console.log(newStr)
```

我们将`str.length`乘以-1，然后加 1，得到字符串第二个字符的索引。

所以`newStr`和其他例子一样。

# Rest 运算符

因为 JavaScript 字符串是可迭代的对象，所以我们可以使用 rest 操作符来获取它自己的数组中除了第一个以外的字符。

例如，我们可以写:

```
const str = "foobar";
const [firstChar, ...chars] = str
const newStr = chars.join('')
console.log(newStr)
```

我们有一个`chars`数组，它有一个来自`str`的字符数组，除了第一个字符。

然后我们可以用一个空字符串调用`join`来将字符连接回一个字符串。

所以`newStr`和我们之前的一样。

# 结论

我们可以使用`substring`和`slice`方法从第二个字符位于原始字符串末尾的字符串中提取子字符串。

此外，我们可以使用 rest 操作符获取除第一个字符之外的所有字符，并调用`join`将这些字符连接回一个字符串。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)