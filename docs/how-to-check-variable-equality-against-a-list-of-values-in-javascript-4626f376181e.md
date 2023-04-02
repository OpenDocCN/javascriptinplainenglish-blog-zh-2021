# 如何在 JavaScript 中根据值列表检查变量的相等性？

> 原文：<https://javascript.plainenglish.io/how-to-check-variable-equality-against-a-list-of-values-in-javascript-4626f376181e?source=collection_archive---------9----------------------->

![](img/15b65cf6f6a7ba9500cead8761c70f48.png)

Photo by [Chris Rosiak](https://unsplash.com/@oserone?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须对照 JavaScript 中的值列表检查变量的相等性。

在本文中，我们将研究如何在 JavaScript 中根据值列表检查变量的相等性。

# 使用 Array.prototype.indexOf 方法

我们可以使用 JavaScript 数组的`indexOf`方法来检查一个值是否包含在数组的值列表中。

例如，我们可以写:

```
let foo;
//...
if ([1, 3, 12].indexOf(foo) > -1) {
  //...
}
```

我们有了`foo`变量，我们通过将这些值放入一个数组来检查`foo`是 1、3 还是 12，然后用`foo`调用数组的`indexOf`方法。

然后，如果它返回一个大于-1 的数字，我们知道`foo`是数组中列出的值之一。

# 使用 Array.prototype.includes 方法

我们可以用来检查一个变量是否是列表中的一个值的另一个数组方法是使用`includes`方法。

例如，我们可以写:

```
let foo;
//...
if ([1, 3, 12].includes(foo)) {
  //...
}
```

我们用称呼`indexOf`的方式称呼`includes`。

如果`includes`返回`true`，那么我们知道`foo`是数组中的一个值。

# 结论

我们可以将想要检查的值列表放入一个数组中，然后使用`includes`或`indexOf`方法来检查变量是否在数组中。