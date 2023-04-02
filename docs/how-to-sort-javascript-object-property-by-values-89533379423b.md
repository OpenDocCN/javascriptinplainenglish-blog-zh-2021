# 如何按值对 JavaScript 对象属性进行排序？

> 原文：<https://javascript.plainenglish.io/how-to-sort-javascript-object-property-by-values-89533379423b?source=collection_archive---------8----------------------->

![](img/74dba95fdfa8efe88f3e0b692b1b8eec.png)

Photo by [Jess Bailey](https://unsplash.com/@jessbaileydesigns?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要根据值对 JavaScript 对象进行排序。

在本文中，我们将研究在 JavaScript 程序中实现这一点的各种方法。

# 使用`Object.entries and Array Methods`按值对 JavaScript 对象属性进行排序

我们可以使用内置在`Object`构造函数中的 JavaScript 方法，以数组的形式获取对象的键和值。

然后我们可以用数组方法重新排列它们。

例如，我们可以写:

```
const ages = {
  james: 10,
  jane: 9,
  bob: 30
}const sorted = Object.entries(ages)
  .sort(([, v1], [, v2]) => v1 - v2)
  .reduce((obj, [k, v]) => ({
    ...obj,
    [k]: v
  }), {})
console.log(sorted)
```

我们使用`Object.entries`方法从`ages`对象中获取一个键值对数组。

然后我们用回调函数调用`sort`，对从`Object.entries`返回的数组中析构的值进行排序。

然后我们用回调函数调用`reduce`，将`obj`对象与`k`和`v`键值对合并。

第二个参数应该设置为一个对象，这样我们就可以开始进行对象扩展。

因此，`sorted`应该是:

```
{jane: 9, james: 10, bob: 30}
```

除了使用`reduce`，我们还可以使用`Object.fromEntries`将排序后的数组转换回对象。

例如，我们可以写:

```
const ages = {
  james: 10,
  jane: 9,
  bob: 30
}const sortedArr = Object.entries(ages)
  .sort(([, v1], [, v2]) => v1 - v2)
const sorted = Object.fromEntries(sortedArr)
console.log(sorted)
```

`Object.fromEntries`接受一个由键值对组成的数组。这些键作为属性名放入对象中。

并且这些值是它们对应的值。

因此，我们应该得到与之前相同的结果，但是以更短的方式书写。

# `Object.keys`

根据属性值对对象属性进行排序的另一种方法是从`Object.keys`方法中获取键。

然后我们可以用同样的方法排序。

例如，我们可以写:

```
const ages = {
  james: 10,
  jane: 9,
  bob: 30
}const sorted = Object.keys(ages)
  .sort((key1, key2) => ages[key1] - ages[key2])
  .reduce((obj, key) => ({
    ...obj,
    [key]: ages[key]
  }), {})
console.log(sorted)
```

`Object.keys`只返回`ages`对象的属性名字符串，所以在`sort`回调中，我们必须从`ages`对象获取值来进行排序。

此外，我们必须在`reduce`回调中做同样的事情，从`ages`获取对象值。

最后，`sorted`应该和上一个例子一样。

# 结论

我们可以使用原生 JavaScript 对象和数组方法，让我们根据属性值对属性进行排序。

*更多内容看* [*说白了. io*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*