# 如何修剪掉 JavaScript 字符串中的最后一个字符？

> 原文：<https://javascript.plainenglish.io/how-to-trim-off-the-last-character-in-a-javascript-string-c153abb5581b?source=collection_archive---------19----------------------->

![](img/cfc499d2c810a84d3200862fef43379f.png)

Photo by [Devon Janse van Rensburg](https://unsplash.com/@devano23?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

删除 JavaScript 字符串中的最后一个字符是我们经常要做的事情。

在本文中，我们将研究如何删除 JavaScript 字符串中的最后一个字符。

# 字符串.原型.子字符串

我们可以使用 string 实例中可用的`substring`方法来返回它所调用的字符串的子字符串。

例如，我们可以这样使用它:

```
let str = "abc";
str = str.substring(0, str.length - 1);
console.log(str);
```

我们有一个`str`字符串，我们想从中删除最后一个字符。

然后我们调用`substring`,用我们想要提取的开始和结束索引。

然后我们将返回值赋回`str`。

结束索引本身被排除在字符串之外，所以我们需要从我们想要的结束索引中减去一，以提取我们想要的子串。

因此，`str`是代码最后一行的`'ab'`。

# 字符串.原型.切片

一个字符串也伴随着`slice`方法而来。

例如，我们可以写:

```
let str = "abc";
str = str.slice(0, -1);
console.log(str);
```

`slice`也分别取开始和结束索引。

但是我们可以使用负索引，从-1 开始表示最后一个字符，-2 表示倒数第二个字符，依此类推。

与`substring`一样，`slice`从返回的字符串中排除结束索引处的字符。

因此，我们用`slice`和`substring`得到了相同的结果。

# 带 lastIndexOf 的切片

`lastIndexOf`方法返回给定字符的最后一个索引。

所以我们可以写:

```
let str = "abc";
str = str.slice(0, str.lastIndexOf("c"));
console.log(str);
```

我们将`'c'`传递给`lastIndexOf`来获取`str`字符串的最后一个索引。

所以我们把`'ab'`看成最后一行`str`的值。

# split、pop 和 join 方法

此外，要从 JavaScript 字符串中删除最后一个字符，我们可以将字符串拆分成一个数组，然后调用`pop`从数组中删除最后一项，然后使用`join`将字符数组连接回字符串。

为此，我们写道:

```
let str = "abc";
const strArr = str.split("")
strArr.pop();
str = strArr.join('')
console.log(str);
```

我们用一个空字符串调用`split`来将`str`分割成一个字符数组，并将它存储在`strArr`中。

然后我们调用`strArr`上的`pop`来移除`strArr`中的最后一个元素。

然后我们调用`join`将字符数组组合回一个字符串。

由于字符串是可迭代的对象，我们可以使用 spread 运算符将其扩展成字符串。

例如，我们可以写:

```
let str = "abc";
const strArr = [...str]
strArr.pop();
str = strArr.join('')
console.log(str);
```

# 结论

有很多种方法可以用 JavaScript 删除字符串中的最后一个字符。

*多内容于* [***浅显易懂***](http://plainenglish.io)