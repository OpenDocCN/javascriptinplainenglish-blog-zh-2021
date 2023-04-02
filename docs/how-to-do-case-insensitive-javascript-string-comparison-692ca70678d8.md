# 如何进行不区分大小写的 JavaScript 字符串比较？

> 原文：<https://javascript.plainenglish.io/how-to-do-case-insensitive-javascript-string-comparison-692ca70678d8?source=collection_archive---------7----------------------->

![](img/2de335d115870a23e3fcf83f65a16bb6.png)

Photo by [DESIGNECOLOGIST](https://unsplash.com/@designecologist?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们不得不在代码中进行不区分大小写的 JavaScript 字符串比较。

在本文中，我们将研究如何进行不区分大小写的 JavaScript 字符串比较。

# 将两个字符串都转换为大写

用 JavaScript 进行不区分大小写的字符串比较的一种方法是在将它们转换成大写字母后进行比较。

例如，我们可以写:

```
const string1 = 'abc'
const string2 = 'Abc'
const areEqual = string1.toUpperCase() === string2.toUpperCase();
console.log(areEqual);
```

我们有字母相同但大小写不同的`string1`和`string2`。

然后我们用`toUpperCase`方法把它们都转换成大写字母。

然后我们记录下`areEqual`的值。

控制台日志应该记录`true`，因为它们在转换成大写时是一样的。

# 将两个字符串都转换成小写

我们可以将两个字符串都转换成小写，这样就可以进行比较了。

例如，我们可以写:

```
const string1 = 'abc'
const string2 = 'Abc'
const areEqual = string1.toLowerCase() === string2.toLowerCase();
console.log(areEqual);
```

那么`areEqual`应该是`true`，因为当它们都转换成小写时是相同的。

# localeCompare 方法

我们可以使用 JavaScript 字符串的`localeCompare`方法来进行不区分大小写的字符串比较。

如果它们相同，那么它返回 0。

例如，我们可以写:

```
const string1 = 'abc'
const string2 = 'Abc'
const areEqual = string1.localeCompare(string2, undefined, {
  sensitivity: 'base'
});
console.log(areEqual);
```

我们在`string1`上调用`localeCompare`，并将`string2`传递给第一个参数来比较它们。

然后在第三个参数中，我们传入一个对象，将`sensitivity`设置为`'base'`以在比较时忽略大小写。

那么`areEqual`应该为 0，因为它们在忽略案例时是相同的。

# 结论

为了对两个 JavaScript 字符串进行不区分大小写的比较，我们可以将两个字符串都转换为大写或小写。

此外，我们可以通过设置`sensitivity`设置，使用字符串`localeCompare`方法以不区分大小写的方式比较两个字符串。