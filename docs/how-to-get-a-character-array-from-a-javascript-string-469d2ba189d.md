# 如何从 JavaScript 字符串中获取字符数组？

> 原文：<https://javascript.plainenglish.io/how-to-get-a-character-array-from-a-javascript-string-469d2ba189d?source=collection_archive---------13----------------------->

![](img/46a5c46118938654c1c638f20dc13e0d.png)

Photo by [francis Kwan](https://unsplash.com/@f_kwan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想从字符串中获取一个字符数组。

在本文中，我们将了解如何从字符串中获取字符数组。

# 字符串.原型. split

string 实例的`split`方法让我们可以用任何分隔符分割字符串。

如果我们想从一个字符串中获取一个字符数组，我们可以使用带有空字符串的`split`方法。

例如，我们可以写:

```
const output = "Hello world!".split('');
console.log(output);
```

那么`output`是:

```
["H", "e", "l", "l", "o", " ", "w", "o", "r", "l", "d", "!"]
```

结果。

# 传播算子

将字符串拆分成字符数组的另一种方法是 spread 运算符。

我们可以这样做，因为字符串是一个可迭代的对象。

为了使用它，我们写:

```
const output = [..."Hello world!"]
console.log(output);
```

然后我们得到与之前相同的`output`值。

# 正则表达式 u 标志

我们也可以使用带有正则表达式的字符串`split`方法将一个字符串分割成一个字符数组。

例如，我们可以写:

```
const output = "Hello world!".split(/(?=[\s\S])/u);
console.log(output);
```

\s 匹配任何空白字符，而\S 匹配任何非空白字符。

`/u`标志让我们可以正确地使用 Unicode 字符串进行搜索。

`?=`是后跟量词的 the。

所以我们搜索任何跟在空白或非空白字符后面的东西，并把它们分开。

所以我们得到了和以前一样的结果。

# for-of 循环和数组. prototype.push

由于字符串是一个可迭代的对象，我们可以使用 for-of 循环遍历每个字符。

例如，我们可以写:

```
const output = [];
for (const s of "Hello world!") {
  output.push(s);
}
console.log(output);
```

`s`具有字符串中的字符。

在循环体中，我们调用`output.push`将字符`s`推入`output`数组。

所以我们得到了和以前一样的结果。

# 数组. from

`Array.from`方法是一个静态数组方法，它让我们将一个可迭代的对象转换成一个数组。

所以我们可以用它把一个字符串转换成一个字符数组。

例如，我们可以写:

```
const output = Array.from("Hello world!")
console.log(output);
```

我们得到与之前相同的`output`值。

# 结论

有许多方法可以将 JavaScript 字符串转换成字符数组。

这包括数组方法、扩展运算符和循环。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)