# JavaScript 中如何检查变量是否为字符串？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-a-variable-is-a-string-in-javascript-a6728d279fe2?source=collection_archive---------17----------------------->

![](img/f3ea9a904e62c4c9b8d86519615c5e09.png)

Photo by [Pascal Bernardon](https://unsplash.com/@pbernardon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

由于 JavaScript 变量可以存储任何类型的数据，所以检查变量是否是字符串是我们在 JavaScript 中要做的很多事情。

在本文中，我们将看看如何在 JavaScript 中检查变量是否是字符串。

# 运算符的类型

JavaScript `typeof`操作符对于检查变量是否是字符串很有用。

例如，我们可以写:

```
const booleanValue = true;
const numericalValue = 123;
const stringValue = "abc";
const stringObject = new String("abc");
console.log(typeof booleanValue)
console.log(typeof numericalValue)
console.log(typeof stringValue)
console.log(typeof stringObject)
```

我们在变量之前使用`typeof`操作符来检查它们返回什么。

第一个`console.log`应该登录`'boolean'`。

第二个`console.log`应该记录`'boolean'`。

第三个`console.log`应该记录`'string'`。

第四个`console.log`应该记录`'object'`。

我们不应该使用`String`构造函数，因为它不返回我们期望的字符串类型。

相反，我们应该总是使用字符串文字。

# `toString`

我们可以使用一个字符串的`toString`方法来检查它是否是一个字符串。

例如，我们可以写:

```
const booleanValue = true;
const numericalValue = 123;
const stringValue = "abc";
const stringObject = new String("abc");const isString = (x) => {
  return Object.prototype.toString.call(x) === "[object String]"
}
console.log(isString(booleanValue))
console.log(isString(numericalValue))
console.log(isString(stringValue))
console.log(isString(stringObject))
```

我们用参数`x`从`Object.prototype`调用`toString`，看它是否返回`'[object String]'`。

如果`x`是一个字符串，那么它从`Object.prototype`继承的`toString`方法应该返回`'[object String']`。

因此，前 2 个控制台日志记录了`false`。

以及最后 2 个日志`true`。

# **罗达什**

Lodash 有一个`isString`方法来检查变量是否是字符串。

例如，我们可以写:

```
const booleanValue = true;
const numericalValue = 123;
const stringValue = "abc";
const stringObject = new String("abc");console.log(_.isString(booleanValue))
console.log(_.isString(numericalValue))
console.log(_.isString(stringValue))
console.log(_.isString(stringObject))
```

它对字符串文字和字符串包装对象都有效，所以前两个控制台日志 log `false`。

以及最后 2 个日志`true`。

# 结论

有很多方法可以检查 JavaScript 变量是否包含字符串。

一种方法是使用`typeof`操作符。另一个检查`toString`的返回结果。

Lodash 还有`isString`方法来检查变量是否是字符串。

*更多内容请看*[***plain English . io***](http://plainenglish.io)