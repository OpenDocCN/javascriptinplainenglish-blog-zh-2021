# 如何在 JavaScript 中检查一个对象是否为空？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-an-object-is-empty-in-javascript-d0686d67e7ed?source=collection_archive---------12----------------------->

![](img/84efcd3c9c00e454b34ad3372d1d1ed1.png)

Photo by [Mike Dorner](https://unsplash.com/@dorner?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

检查空对象是我们有时必须做的事情。

在本文中，我们将看看用 JavaScript 检查对象是否为空的各种方法。

# Object.keys 和构造函数属性

我们可以结合`Object.keys`方法和`constructor`属性来检查一个对象是否为空对象。

为此，我们写道:

```
const obj = {}
console.log(obj &&
  Object.keys(obj).length === 0 && obj.constructor === Object)
```

`obj`确保`obj`不是`null`或`undefined`。

`Object.keys(obj).length === 0`检查`obj`中的键数是否为 0。

`Object.keys`返回一个对象的非继承键数组。

然而，我们没有检查`obj`是否是一个对象文字。

因此，我们需要写:

```
obj.constructor === Object
```

去检查一下。

如果它是一个对象文字，那么它应该从`Object`构造函数中创建。

所以`obj.constructor`应该返回`Object`is`obj`is object literal。

这是检查空对象的唯一方法。

很少有其他方法可以做到这一点。

# JSON.stringify

我们可以用`JSON.stringify`方法检查一个对象。

例如，我们可以写:

```
function isEmpty(obj) {
  for (const prop in obj) {
    if (obj.hasOwnProperty(prop)) {
      return false;
    }
  } return JSON.stringify(obj) === JSON.stringify({});
}
```

我们用 for-in 循环遍历 ketys。

然后我们用`hasOwnProperties`检查一个对象是否有任何非继承的属性。

如果`obj.hasOwnProperties`返回带有任何`prop`值的`true`，该值具有正在被迭代的键，那么我们应该返回`false`。

这是因为这意味着在`obj`中存在一个非继承键，并且`obj`不为空。

如果循环没有找到键，那么我们可以使用`JSON.stringify`来检查一个字符串化的空对象。

这有利于支持没有`Object.keys`方法的运行时环境，这种情况应该很少见。

# Lodash 是一个空方法

Lodash 附带了`isEmpty`方法，它让我们检查一个对象是否为空。

我们只是传入一个想要检查的对象:

```
_.isEmpty({});
```

# object . getownpropertymanames

方法返回一个对象的非继承键数组。

所以我们可以像使用`Object.keys`一样使用它来检查一个空对象。

例如，我们可以写:

```
if (Object.getOwnPropertyNames(obj).length === 0) {
  //...
}
```

我们只是检查返回的数组长度是否为 0。

它还返回不可枚举的属性，这意味着它返回不会被`Object.keys`返回的键，但不是从任何原型对象继承的。

所以这个检查比用`Object.keys`检查更全面。

# 结论

用 JavaScript 检查空对象有几种方法。

最好的方法是使用`Object.keys`或`Object.getOwnPropertyNames`。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)