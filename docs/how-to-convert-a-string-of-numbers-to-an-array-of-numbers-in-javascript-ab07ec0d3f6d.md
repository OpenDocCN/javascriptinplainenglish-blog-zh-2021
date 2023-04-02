# 如何在 JavaScript 中将一串数字转换成一个数字数组？

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-string-of-numbers-to-an-array-of-numbers-in-javascript-ab07ec0d3f6d?source=collection_archive---------7----------------------->

![](img/9fa9b5a7208a4d0e21b17faeba6e47d4.png)

Photo by [Donald Giannatti](https://unsplash.com/@wizwow?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们有一个用逗号分隔的数字列表的字符串，我们想把它转换成一个数字数组。

在本文中，我们将看看如何在 JavaScript 中将一串数字转换成一个数字数组。

# 使用字符串和数组方法

我们可以使用 JavaScript 字符串可用的`split`方法，通过分隔符分割字符串，将字符串转换为字符串数组。

所以我们可以使用`split`方法将字符串按照逗号分割成一个字符串数组。

所以它会返回一个字符串数组，字符串之间用逗号隔开。

然后我们可以调用数组`map`方法将拆分后的字符串数组条目映射成数字。

例如，我们可以写:

```
const nums = "1,2,3,4".split(`,`).map(x => +x)
console.log(nums)
```

我们用逗号调用`split`将字符串分隔成一个数组，数组中有数字字符串。

然后我们用回调函数调用`map`，用一元运算符`+`将每个条目转换成一个数字。

因此，`nums`就是`[1, 2, 3, 4]`的结果。

除了使用一元的`+`运算符，我们还可以使用`parseInt`函数。

为了使用它，我们写:

```
const nums = "1,2,3,4".split(`,`).map(x => parseInt(x, 10))
console.log(nums)
```

`parseInt`带 2 个参数。

第一个参数是我们要转换成数字的值。

第二个参数是我们希望返回的数字所在的基数。

所以 10 会将`x`转换成十进制数。

因此，我们得到和以前一样的结果。

另一种将字符串转换成数字的方法是使用`Number`函数。

为了使用它，我们写:

```
const nums = "1,2,3,4".split(`,`).map(x => Number(x))
console.log(nums)
```

我们得到了同样的结果。

`Number`总是转换成十进制数，所以我们不必指定它。

如果我们需要的话，还有一个将值转换成浮点数的`parseFloat`函数。

它采用与`parseInt`相同的论点。

为了使用它，我们写:

```
const nums = "1,2,3,4".split(`,`).map(x => parseFloat(x, 10))
console.log(nums)
```

对于`nums`，我们得到了与之前相同的结果。

# 结论

我们可以用一些字符串、数组和数字函数把一串数字转换成一个数字数组。

***更多内容看*** [***说白了. io***](http://plainenglish.io/)