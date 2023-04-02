# 如何在 JavaScript 中比较数组

> 原文：<https://javascript.plainenglish.io/how-to-compare-arrays-in-javascript-3ee00907e7cf?source=collection_archive---------7----------------------->

![](img/4016037153d6b0f84d15e070fa8074eb.png)

Photo by [Coffee Geek](https://unsplash.com/@coffeegeek?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

比较两个数组是否相同是我们在 JavaScript 应用程序中经常要做的事情。

在本文中，我们将看看如何用 JavaScript 比较数组。

# 数组.原型.每

我们可以使用数组的`every`方法来检查一个数组中的每个元素是否也在我们要比较的数组中。

如果它们有相同的长度，并且一个数组中的每个元素也在另一个数组中，那么我们知道两个数组是相同的。

例如，我们会写:

```
const array1 = [1, 2, 3]
const array2 = [1, 2, 3]
const sameArray = array1.length === array2.length && array1.every((value, index) => value === array2[index])
console.log(sameArray)
```

我们有两个内容相同的数组`array1`和`array2`。

然后我们检查两者的长度是否相同。

然后我们用回调函数调用`every`来比较`value`和`array2[index]`。

`value`拥有我们正在迭代的`array1`条目。

`index`拥有我们正在迭代的`array1`条目的索引。

因此，我们可以使用`index`从`array2`中获取元素，并对它们进行比较。

# Lodash isEqual 方法

我们还可以使用 Lodash 的`isEqual`方法来比较 2 个数组，看它们是否有相同的内容。

例如，我们可以写:

```
const array1 = [1, 2, 3]
const array2 = [1, 2, 3]
const sameArray = _.isEqual(array1, array2)
console.log(sameArray)
```

我们只是把想要比较的数组作为参数传入。

# `JSON.stringify`

同样，我们可以用`JSON.stringify`方法进行简单的数组比较。

它会把数组转换成 JSON 字符串。

然后我们可以直接比较字符串化的数组。

例如，我们可以写:

```
const array1 = [1, 2, 3]
const array2 = [1, 2, 3]
const sameArray = JSON.stringify(array1) === JSON.stringify(array2);
console.log(sameArray)
```

# 结论

有几种方法可以用来比较 JavaScript 中两个数组是否相同。

最简单的方法是使用`JSON.stringify`来比较数组的字符串化版本。

同样，我们可以使用`every`方法来检查数组中的每一项，看它们是否相同。

最后，我们可以使用 Lodash `isEqual`方法来比较 2 个数组。

*更多内容请看*[***plain English . io***](http://plainenglish.io)