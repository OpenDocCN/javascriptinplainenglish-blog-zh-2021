# 如何在 Javascript 中移除数组中的空元素？

> 原文：<https://javascript.plainenglish.io/how-to-remove-empty-elements-from-an-array-in-javascript-48647fe2abe7?source=collection_archive---------2----------------------->

![](img/652feebde046dcf35f77596b8762cb00.png)

Photo by [Hans Eiskonen](https://unsplash.com/@eiskonen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从 JavaScript 数组中移除空元素是我们有时不得不做的事情。

在本文中，我们将研究如何从 JavaScript 数组中移除空元素。

# 数组.原型.过滤器

我们可以使用数组实例的`filter`方法从数组中移除空元素。

要从数组中移除所有的`null`或`undefined`元素，我们可以写:

```
const array = [0, 1, null, 2, "", 3, undefined, 3, , , , , , 4, , 4, , 5, , 6, , , , ];
const filtered = array.filter((el) => {
  return el !== null && typeof el !== 'undefined';
});
console.log(filtered);
```

`filter`方法将数组孔视为`undefined`。

所以我们应该看到:

```
[0, 1, 2, "", 3, 3, 4, 4, 5, 6]
```

作为`filtered`的值。

如果我们想删除所有的 falsy 值，我们可以将`Boolean`函数传递给`filter`。

例如，我们可以写:

```
const array = [0, 1, null, 2, "", 3, undefined, 3, , , , , , 4, , 4, , 5, , 6, , , , ];
const filtered = array.filter(Boolean);
console.log(filtered);
```

Falsy 值包括`null`、`undefined`、0、空字符串、`NaN`和`false`。

因此，如果我们将它们传递给`Boolean`函数，它们将返回`false`。

因此，`filtered`是:

```
[1, 2, 3, 3, 4, 4, 5, 6]
```

如果我们想返回一个只剩下数字的数组，我们可以写:

```
const array = [0, 1, null, 2, "", 3, undefined, 3, , , , , , 4, , 4, , 5, , 6, , , , ];
const filtered = array.filter(Number);
console.log(filtered);
```

然后我们得到同样的结果。

或者我们可以写:

```
const array = [0, 1, null, 2, "", 3, undefined, 3, , , , , , 4, , 4, , 5, , 6, , , , ];
const filtered = array.filter(n => n);
console.log(filtered);
```

并且还会得到相同的结果，因为回调的返回值将被自动转换为布尔值。

# 洛达什

Lodash 也有一个`filter`方法，它与原生的`filter`方法做同样的事情。

例如，我们可以写:

```
const array = [0, 1, null, 2, "", 3, undefined, 3, , , , , , 4, , 4, , 5, , 6, , , , ];
const filtered = _.filter(array, Boolean);
console.log(filtered);
```

过滤掉所有虚假值。

那么`filtered`就是`[1, 2, 3, 3, 4, 4, 5, 6]`。

它还有一个`compact`方法，专门用来从数组中删除虚假值。

例如，我们可以写:

```
const array = [0, 1, null, 2, "", 3, undefined, 3, , , , , , 4, , 4, , 5, , 6, , , , ];
const filtered = _.compact(array);
console.log(filtered);
```

然后我们得到同样的结果。

# 结论

有多种方法可以用原生数组方法或 Lodash 从 JavaScript 数组中移除 falsy 元素。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)