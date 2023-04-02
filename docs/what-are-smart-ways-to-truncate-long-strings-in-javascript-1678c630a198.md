# JavaScript 中截断长字符串的聪明方法有哪些？

> 原文：<https://javascript.plainenglish.io/what-are-smart-ways-to-truncate-long-strings-in-javascript-1678c630a198?source=collection_archive---------8----------------------->

![](img/daaf351db759dfa1e1e1d61c19e398cc.png)

Photo by [Sara Kurfeß](https://unsplash.com/@stereophototyp?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要截断 JavaScript 代码中的长字符串。

在本文中，我们将研究一些在 JavaScript 中截断长字符串的好方法。

# 使用 String.prototype.substr 方法

我们可以使用字符串实例的`substr`方法返回给定起始和结束索引的子字符串。

例如，我们可以写:

```
const truncate = (str, n) => {
  return (str.length > n) ? str.substr(0, n - 1) + '...' : str;
};console.log(truncate('Lorem ipsum dolor sit amet, consectetur adipiscing elit.', 10))
```

我们用接受字符串的`str`参数创建了`truncate`函数。

`n`是要截断的字符数。

如果字符串长度大于`n`，我们将返回由`substr`方法返回的带有开始和结束索引的子字符串。

否则，我们返回整个字符串。

因此，控制台日志应该记录`'Lorem ips…’`,因为我们将字符串截断为 10 个字符的长度。

# 字符串.原型.替换方法

我们可以使用带有正则表达式的 string `replace`方法来截断一个字符串。

为了使用它，我们写:

```
const truncate = (str, n) => {
  return str.replace(new RegExp(`(.{${n-1}})..+`), "$1...");
};console.log(truncate('Lorem ipsum dolor sit amet, consectetur adipiscing elit.', 10))
```

我们用一个正则表达式调用`replace`，该正则表达式接受`n`值并匹配字符串的第一个`n-1`字符。

然后在第二个参数中，我们使用`$1`占位符来获取匹配的字符串，然后在它后面添加`...`。

因此，在控制台日志中，我们会得到与之前相同的结果。

# 洛达什截断法

另一种简单截断字符串的方法是使用 Lodash `truncate`方法。

例如，我们可以写:

```
const truncated = _.truncate('Lorem ipsum dolor sit amet, consectetur adipiscing elit.', {
  length: 12
});
console.log(truncated)
```

调用`truncate`方法来截断字符串。

第一个参数是要截断的字符串。

第二个参数是截断选项。

我们将`length`设置为 12，将字符串截断为 12 个字符长，包括省略号。

因此，`truncated`就是`'Lorem ips…’`就是`truncated`的值。

# 结论

我们可以使用普通的 JavaScript 字符串方法或 Lodash `truncate`方法来截断 JavaScript 中的字符串。

*更多内容请看*[***plain English . io***](http://plainenglish.io)