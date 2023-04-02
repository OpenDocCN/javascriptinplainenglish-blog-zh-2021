# 如何获取一个 JavaScript 数组中所有非唯一的值？

> 原文：<https://javascript.plainenglish.io/how-to-get-all-non-unique-values-in-a-javascript-array-6e98365f54be?source=collection_archive---------12----------------------->

![](img/fb9dd8ec62ef5e52452fe2fe8f37bc4f.png)

Photo by [Andy Brunner](https://unsplash.com/@andy_brunner?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望从一个 JavaScript 数组中获得所有重复的值。

在本文中，我们将研究获取 JavaScript 数组中所有非唯一值的方法。

# 数组.原型.过滤器

我们可以使用 JavaScript 数组的`filter`方法返回满足给定条件的数组。

它接受一个回调，该回调返回我们希望每个返回项具有的条件。

因此，我们可以将此与在回调中调用`indexOf`方法结合起来，以检查该项目是否是项目的第一个实例。

为此，我们在调用`filter`的数组上调用`indexOf`，这可以从回调的第三个参数中获得。

然后，我们可以检查返回的索引是否与被迭代的项所在的索引相同。

例如，我们可以写:

```
const duplicates = [1, 2, 2, 4, 3, 4].filter((e, index, arr) => arr.indexOf(e) !== index)
console.log(duplicates)
```

然后我们用带有`e`、`index`和`arr`参数的回调函数调用`filter`。

`e`是被迭代的项目。

`index`是项目`e`的索引。

而`arr`是正在调用`filter`的数组。

我们用参数`e`调用`arr`上的`indexOf`来返回`arr`中第一个`e`实例的索引。

如果它与`index`不同，那么我们知道它不是一个值的第一个实例。

因此，`duplicates`是`[2, 4]`，因为它们在数组中是重复的。

# 清点物品

我们可以通过创建自己的对象来设置计数，从而对数组中的项目进行计数。

例如，我们可以写:

```
const obj = [1, 2, 2, 4, 3, 4]
  .map((val) => {
    return {
      count: 1,
      val
    }
  })
  .reduce((a, b) => {
    a[b.val] = (a[b.val] || 0) + b.count
    return a
  }, {})const duplicates = Object.entries(obj)
  .filter(([, val]) => {
    return val > 1
  })
  .map(([key]) => +key)
console.log(duplicates)
```

我们调用`map`将每个条目映射到一个对象，其中`count`设置为 1，`val`设置为数组项值。

然后我们调用`reduce`用每一项的计数创建一个对象，每一项都是键。

我们通过将来自`a[b.val]`的计数分配给`(a[b.val] || 0) + b.count`来实现这一点。

`b.count`有了新的计数。

我们返回`a`，它记录了目前为止所有的计数。

第二个参数是一个空对象，所以我们在最后创建一个对象。

然后为了得到重复的值，我们得到所有值大于 1 的键。

为此，我们在`obj`上调用`Object.entries`。

然后我们用回调函数调用`filter`来返回任何`val`大于 1 的条目。

`val`是对象属性值。

然后我们调用`map`从键值对数组中获取`key`。

因此，我们得到了与上一个例子相同的结果。

# 结论

我们可以使用各种数组和对象方法从数组中获取重复值。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)