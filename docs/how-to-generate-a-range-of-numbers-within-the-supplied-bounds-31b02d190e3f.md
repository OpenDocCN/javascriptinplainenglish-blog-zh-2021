# 如何在提供的范围内生成一系列数字？

> 原文：<https://javascript.plainenglish.io/how-to-generate-a-range-of-numbers-within-the-supplied-bounds-31b02d190e3f?source=collection_archive---------17----------------------->

![](img/fa3ca8cc723cb207b7131e736c834f12.png)

Photo by [Dimitri Houtteman](https://unsplash.com/@dimhou?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候我们需要在给定的范围内生成一个数字数组。

在本文中，我们将研究如何在给定的范围内生成一系列数字。

# 数组函数

我们可以使用`Array`构造函数作为常规函数来创建给定大小的数组。

然后我们可以用`keys`方法得到一个数组的索引。

例如，我们可以写:

```
const arr = [...Array(5).keys()];
console.log(arr)
```

我们调用`keys`来返回数组的索引。

我们将这些项目分散到一个数组中。

# 数组. from

`Array.from`方法是一个静态方法，让我们创建一个从另一个数组派生的数组。

我们可以用它来创建一个数字数组，用它来映射我们想要的值。

例如，我们可以写:

```
const lowerBound = 6;
const arr = Array.from(new Array(10), (x, i) => i + lowerBound);
console.log(arr)
```

第一个参数是我们要映射的数组。

第二个参数是映射函数。

`x`是我们正在迭代的第一个参数数组中的条目。

因此，我们得到:

```
[6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

作为`arr`的值。

# 洛达什

Lodash 有`range`方法，让我们可以轻松地创建一个包含一系列数字的数组。

最多需要 3 个参数。

第一个是只有一个参数时要创建的数组的大小。

如果我们传入两个参数，那么第一个数字是起始数字，第二个是结束数字。

如果我们传入 3 个参数，那么第一个和第二个参数就等同于传入 2 个参数。

第三个参数是每个数字之间的增量。

例如，如果我们写:

```
const arr = _.range(10);
console.log(arr)
```

那么`arr`就是`[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]`。

如果我们写:

```
const arr = _.range(1, 11);
console.log(arr)
```

那么`arr`就是`[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]`。

如果我们写下:

```
const arr = _.range(1, 11, 2);
console.log(arr)
```

那么`arr`就是`[1, 3, 5, 7, 9]`。

# 结论

我们可以用`Array`函数创建一个数字数组。

同样，我们可以使用`Array.from`静态方法。

创建数字数组的另一个简单方法是使用 Lodash 的`range`方法。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)