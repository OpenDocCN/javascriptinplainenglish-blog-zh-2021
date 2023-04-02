# 如何统计一个 JavaScript 字符串中子串出现的次数？

> 原文：<https://javascript.plainenglish.io/how-to-count-the-number-of-substring-occurrences-in-a-javascript-string-5b56f4ab3f3c?source=collection_archive---------7----------------------->

![](img/3e98188ae6f228a8dc1e7008c7ed5e83.png)

Photo by [Sarra Marzguioui](https://unsplash.com/@geist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须计算 JavaScript 字符串中一个子字符串出现的次数。

在本文中，我们将研究如何计算 JavaScript 字符串中子串的出现次数。

# 字符串.原型.匹配

string `match`方法让我们在调用它的字符串中找到带有给定正则表达式模式的子字符串。

因此，我们可以用它来查找 JavaScript 字符串中子串出现的次数。

为了使用它，我们写:

```
const str = "This is a string.";
const count = [...(str.match(/is/g) || [])].length;
console.log(count);
```

我们有`str`字符串。

我们用我们要寻找的子串和`g`标志对它调用`match`,在字符串中寻找子串的所有实例。

如果没有匹配，它返回`undefined`，所以我们必须添加`|| []`来返回一个空数组。

然后我们得到数组的`length`来得到出现的次数。

所以`count`是 2，因为字符串中有 2 个`'is'`的实例。

# 字符串.原型. split

我们可以使用`split`方法通过分隔符分割一个字符串。

所以我们可以使用`split`按照我们要寻找的子串来分割字符串，然后减去 1，得到子串的实例数。

为此，我们写道:

```
const str = "This is a string.";
const count = str.split('is').length - 1;
console.log(count);
```

我们用`'is'`调用`split`以`'is'`为分隔符拆分`str`串。

然后我们必须从返回的`length`中减去 1 以得到正确的结果。

# 结论

要计算一个字符串中一个子字符串出现的次数，我们可以分割该字符串或者使用正则表达式搜索它。

*更多内容请看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***