# 如何在 JavaScript 中得到两个数组的区别？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-difference-between-two-arrays-in-javascript-8fbdb2155bf0?source=collection_archive---------1----------------------->

![](img/1b2d5242439569bb20f55e5b9e1fbfd9.png)

Photo by [JJ Ying](https://unsplash.com/@jjying?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候我们需要知道两个 JavaScript 数组的区别。

区别在于一个数组中的项目不在另一个数组中。

在本文中，我们将看看如何在 JavaScript 中获得两个数组之间的各种差异。

# `Intersection`

两个数组的交集是两个数组中都有的一组项。

为了得到交集，我们可以使用`filter`方法。

我们可以写:

```
const arr1 = ['a', 'b'];
const arr2 = ['a', 'b', 'c', 'd'];
const intersection = arr1.filter(x => arr2.includes(x));
console.log(intersection)
```

来计算交叉路口。

我们有两个阵列，`arr1`和`arr2`。

我们通过用回调函数调用`arr1`上的`filter`来计算`intersection`，回调函数检查来自`arr1`的项目`x`是否也包含在`arr2`中。

我们可以切换第 3 行中的`arr1`和`arr2`，得到相同的结果。

例如，我们可以写:

```
const arr1 = ['a', 'b'];
const arr2 = ['a', 'b', 'c', 'd'];
const intersection = arr2.filter(x => arr1.includes(x));
console.log(intersection)
```

在这两种情况下，`intersection`都是`[“a”, “b”]`。

# **两个阵列之间的差异**

两个数组之间的区别在于一个数组中包含一个数组中可用但另一个数组中不可用的所有项目。

例如，如果我们有像上面这样的`arr1`和`arr2`，我们可以通过编写以下内容从`arr2`中获取不在`arr1`中的所有项目:

```
const arr1 = ['a', 'b'];
const arr2 = ['a', 'b', 'c', 'd'];
const intersection = arr2.filter(x => !arr1.includes(x));
console.log(intersection)
```

我们所做的只是改变`filter`回调来检查`arr2`中的项目`x`是否包含在`arr1`中。

如果不是，我们就把它放在`intersection`数组中。

所以，`intersection`就是`[“c”, “d”]`。

# **两个阵列之间的对称差异**

两个数组之间的对称差异是在其中一个数组中但不在两个数组中的项目集。

为了计算对称差，我们可以写出:

```
const arr1 = ['a', 'b', 'e'];
const arr2 = ['a', 'b', 'c', 'd'];
const symDiff = [...new Set([...arr1, ...arr2])].filter(x => (!arr1.includes(x) && arr2.includes(x)) || (arr1.includes(x) && !arr2.includes(x)))
console.log(symDiff)
```

我们通过将一个包含来自`arr1`和`arr2`的条目的数组传递给`Set`构造函数，将所有数组项放入一个集合中。

这将从组合数组中移除任何重复的元素。

然后，我们用外展操作符将集合转换回数组。

然后我们用这个调用`filter`:

```
(!arr1.includes(x) && arr2.includes(x)) || (arr1.includes(x) && !arr2.includes(x))
```

由回调函数返回，以获取仅在`arr1`或仅在`arr2`中的所有元素。

因此，`symDiff`应该是`[“e”, “c”, “d”]`。

# 结论

我们可以用集合和数组方法计算数组之间的各种差异。

*更多内容看* [*说白了。在这里注册我们的*](http://plainenglish.io/) [*免费周报*](http://newsletter.plainenglish.io/) *。*