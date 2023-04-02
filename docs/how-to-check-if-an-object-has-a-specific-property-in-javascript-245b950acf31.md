# 如何在 JavaScript 中检查一个对象是否有特定的属性？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-an-object-has-a-specific-property-in-javascript-245b950acf31?source=collection_archive---------5----------------------->

![](img/ce41fab90389fe866a60ea9dedc141ce.png)

Photo by [Gus Ruballo](https://unsplash.com/@gusruballo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 对象是动态创建的。

这意味着我们可能不知道 JavaScript 对象中有什么内容。

因此，我们必须找到检查一个对象是否包含特定属性的方法。

在本文中，我们将看看如何在 JavaScript 中检查一个对象是否有特定的属性。

# `The hasOwnProperty Method`

`hasOwnProperty`是从`Object.prototype`继承的一个方法。

大多数对象从它们继承，除非我们指定它们不从它继承。

因此，我们可以这样写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}console.log(obj.hasOwnProperty('a'))
console.log(obj.hasOwnProperty('d'))
```

用属性名字符串调用`hasOwnProperty`。

第一个控制台日志应该记录`true`，因为`a`在`obj`中。

第二个控制台日志应该记录`false`，因为`d`不在`obj`中。

`hasOwnProperty`方法是从`Object.prototype`继承的，所以它很容易被其他代码覆盖。

为了避免这个问题，我们可以通过编写以下代码用`call`调用`hasOwnProperty`:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}console.log(Object.prototype.hasOwnProperty.call(obj, 'a'))
console.log(Object.prototype.hasOwnProperty.call(obj, 'd'))
```

我们用`Object.prototype.hasOwnProperty.call`调用`hasOwnProperty`，它不能像用`hasOwnProperty`方法那样被覆盖。

第一个参数是`this`的值，它应该被设置为我们正在检查属性的对象。

而第二个参数是属性名字符串本身，也就是我们调用第一种方式时的`hasOwnProperty`的第一个参数。

因此，我们应该得到和以前一样的结果。

# in 运算符

`in`操作符让我们检查非继承的和继承的属性。

如果存在具有给定属性名的继承或非继承属性，它将返回`true`。

例如，如果我们有:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}console.log('a' in obj)
console.log('hasOwnProperty' in obj)
```

由于`a`本身就在`obj`中，所以它们都记录了`true`。

而`hasOwnProperty`是继承自`Object.prototype`。

# Lodash 有方法

我们也可以使用 Lodash `has`方法来检查一个属性是否是一个对象的非继承属性。

例如，如果我们写:

```
const obj = {
  a: 1,
  b: 2,
  c: 3
}console.log(_.has(obj, 'a'))
console.log(_.has(obj, 'hasOwnProperty'))
```

然后第一个控制台日志记录`true`。

第二控制台日志记录`false`。

# 结论

有很多方法可以检查一个属性是否在一个对象中。

我们还可以将它们区分为继承属性和非继承属性。

*更多内容看*[***plain English . io***](http://plainenglish.io)