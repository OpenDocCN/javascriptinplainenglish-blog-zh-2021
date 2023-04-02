# 如何在 JavaScript 中多次重复一个字符串？

> 原文：<https://javascript.plainenglish.io/how-to-repeat-a-string-in-javascript-a-number-of-times-8724feed02b8?source=collection_archive---------7----------------------->

![](img/e16ff96f103aded1402ce1284c6176f1.png)

Photo by [Chinh Le Duc](https://unsplash.com/@mero_dnt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要创建一个字符串，它是通过在 JavaScript 代码中多次重复一个字符串而生成的。

在本文中，我们将看看如何在 JavaScript 中轻松地重复字符串。

# 字符串.原型.重复

JavaScript 字符串附带的`repeat`方法让我们创建一个字符串，这个字符串是通过重复调用它的字符串来创建的。

例如，我们可以写:

```
const str = "b".repeat(10)
console.log(str);
```

我们调用`repeat`,告诉它我们想要重复`'b'`的次数。

所以`str`就是`‘bbbbbbbbbb’`。

# 数组构造函数

我们可以使用`Array`构造函数用给定数量的空槽创建一个数组。

我们可以用我们想要重复的音调在上面调用`join`。

例如，我们可以写:

```
const str = Array(11).join("b") 
console.log(str);
```

数组的长度比我们想要重复字符串的次数大 1。

这是因为`join`将字符串放在数组条目之间。

所以我们得到了和以前一样的结果。

# 使用循环

我们可以使用循环来创建重复的字符串。

例如，我们可以写:

```
let word = ''
for (let times = 0; times < 10; times++) {
  word += 'b'
}
console.log(word)
```

我们创建一个运行 10 次迭代的 for 循环。

在循环体中，我们将需要的字符串添加到`word`字符串中。

所以`word`和`'bbbbbbbbbb’`就像我们以前一样。

# 洛达什重复法

从 Lodash 3.0.0 开始，它附带了`repeat`方法，让我们返回一个给定子串重复给定次数的字符串。

例如，我们可以写:

```
const word = _.repeat('b', 10)
console.log(word)
```

那么`word`就是`'bbbbbbbbbb’`，因为我们指定要重复`'b'`10 次。

# 结论

我们可以用 Lodash `repeat`方法或本地 string `repeat`方法重复一个字符串。

此外，我们可以使用循环来追加字符串。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***