# 如何在 JavaScript 中从对象数组中获取不同的值？

> 原文：<https://javascript.plainenglish.io/how-to-get-distinct-values-from-an-array-of-objects-in-javascript-1d7d5f1eb127?source=collection_archive---------3----------------------->

![](img/2a6e121511d11e524b94c04ea0c6f6db.png)

Photo by [William Bayreuther](https://unsplash.com/@wbayreuther?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要从 JavaScript 中的一组对象中获取不同的值。

在本文中，我们将研究如何用 JavaScript 从一组对象中获取不同的值。

# 使用 Array.prototype.map、集合和扩展运算符

从 JavaScript 对象数组中获取不同值的一种方法是使用数组的`map`方法来获取每个对象的属性值数组。

然后我们可以用`Set`构造函数移除重复的值。

然后我们可以用 spread 操作符将集合转换回数组。

例如，我们可以写:

```
const array = [{
    "name": "Joe",
    "age": 17
  },
  {
    "name": "Bob",
    "age": 17
  },
  {
    "name": "Carl",
    "age": 35
  }
]
const unique = [...new Set(array.map(item => item.age))];
console.log(unique)
```

我们有一个`array`数组，它包含具有`name`和`age`属性的对象。

我们希望获得`age`属性的所有不同值。

为此，我们用回调函数调用`array.map`，该回调函数从每个对象返回`age`属性值，并将它们放入数组中。

然后，我们将返回的数组传递给`Set`构造函数。

然后我们用 spread 操作符将集合转换回数组。

所以`unique`就是`[17, 35]`。

# 使用 Array.prototype.map、集合和 Array.from

我们可以用`Array.from`方法替换 spread 操作符，将集合转换成数组

例如，我们可以写:

```
const array = [{
    "name": "Joe",
    "age": 17
  },
  {
    "name": "Bob",
    "age": 17
  },
  {
    "name": "Carl",
    "age": 35
  }
]
const unique = Array.from(new Set(array.map(item => item.age)));
console.log(unique)
```

调用`Array.from`，将集合作为参数，而不是扩展运算符。

我们得到了和以前一样的结果。

# 使用 Array.prototype.map 和 Array.prototype.filter

除了使用`Set`构造函数和 spread 操作符，我们还可以使用`filter`方法来获得不同的值

例如，我们可以写:

```
const array = [{
    "name": "Joe",
    "age": 17
  },
  {
    "name": "Bob",
    "age": 17
  },
  {
    "name": "Carl",
    "age": 35
  }
]
const unique = array
  .map(item => item.age)
  .filter((value, index, self) => self.indexOf(value) === index)console.log(unique)
```

我们用具有`value`、`index`和`self`参数的回调来调用`filter`方法。

`value`具有从`map`返回的数组的值。

`index`拥有从`map`返回的正在被迭代的数组元素的索引。

而`self`是由`map`返回的数组。

我们用`indexOf`方法返回所有给定值的第一个实例。

`indexOf`方法返回第一个元素的索引值。

所以我们可以用它来检查`index`是否只返回每个值的每个实例的第一项。

我们得到了和以前一样的结果。

# 结论

我们可以使用原生 JavaScript 数组方法和 spread 运算符从数组中获取不同的属性值。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)