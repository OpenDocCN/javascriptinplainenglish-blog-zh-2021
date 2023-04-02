# 如何获取一个 JavaScript 字符串的第一个字符？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-first-character-of-a-javascript-string-688206dead9f?source=collection_archive---------20----------------------->

![](img/12a85e334796f0b09fc3c9cf1eb83ac5.png)

Photo by [DESIGNECOLOGIST](https://unsplash.com/@designecologist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要获取代码中 JavaScript 字符串的第一个字符。

在本文中，我们将研究如何获取 JavaScript 字符串的第一个字符。

# 字符串.原型.字符

JavaScript 字符串附带的`chartAt`方法让我们通过索引从字符串中获取字符。

为了获得第一个字符，我们将 0 传递给方法。

例如，我们可以写:

```
const first = 'abc'.charAt(0)
console.log(first)
```

因此，`first`就是`'a'`。

# 字符串.原型.子字符串

`substring`方法让我们从给定起始和结束索引的字符串中获取子字符串。

包括起始索引处的字符。

但是结尾索引处的字符不是。

所以我们可以写:

```
const first = 'abc'.substring(0, 1)
console.log(first)
```

我们得到了同样的结果。

# 字符串.原型.切片

像`substring`方法一样，`slice`方法也让我们获得带有开始和结束索引的子串。

和`substring`一样，起始索引处的字符也包含在内。

但是结尾索引处的字符不是。

例如，我们可以写:

```
const first = 'abc'.slice(0, 1)
console.log(first)
```

我们得到了和其他例子一样的结果。

# 方括号

我们可以像处理`charAt`一样，将第一个字符的索引传入方括号中。

例如，我们可以写:

```
const first = 'abc'[0]
console.log(first)
```

然后我们得到与`charAt`相同的结果。

# 结论

用 JavaScript 有几种方法可以得到字符串的第一个字符。

我们可以用方括号或字符串方法来实现。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***