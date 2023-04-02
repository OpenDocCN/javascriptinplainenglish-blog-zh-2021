# 如何从一个 JavaScript 数组中获取最接近一个数字的数字？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-closest-number-to-a-number-out-of-a-javascript-array-1eb31b18e836?source=collection_archive---------9----------------------->

![](img/1a22b86f2244aa24d3b7800526e0f2a7.png)

Photo by [Carlos Quintero](https://unsplash.com/@c_quintero?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想从 JavaScript 数组中获取与给定数字最接近的数字。

在本文中，我们将研究如何从 JavaScript 数组中获取最接近某个数字的数字。

# 使用 Array.prototype.reduce 方法

从 JavaScript 数组中获取最接近数字的一种方法是使用 JavaScript 数组的`reduce`方法。

为了使用它，我们写:

```
const arr = [2, 42, 82, 122, 162, 202, 242, 282, 322, 362]
const goal = 100
const closest = arr.reduce((prev, curr) => {
  return (Math.abs(curr - goal) < Math.abs(prev - goal) ? curr : prev);
});
console.log(closest)
```

我们有一个包含一堆数字的`arr`数组。

`goal`是我们要在`arr`中寻找最接近的数字。

然后，我们将回调传递给比较`curr — goal`和`prev-goal`之差的绝对值的`reduce`方法。

`prev`是之前最接近`goal`的数字。

`curr`是当前被迭代的数字。

如果`curr`的绝对值比`prev`更接近`goal`，那么我们返回`curr`。

否则，我们返回`goal`。

因此，`closest`是 82。

# 使用 Array.prototype.map 方法

寻找与给定数字最接近的数字的另一种方法是将所有数组条目映射到数组中的数字与目标数字之间的绝对差值。

然后我们就可以用`Math.min`求两个数的最小差。

例如，我们可以写:

```
const arr = [2, 42, 82, 122, 162, 202, 242, 282, 322, 362]
const goal = 100
const indexArr = arr.map((num) => {
  return Math.abs(num - goal)
})
const min = Math.min(...indexArr)
const closest = arr[indexArr.indexOf(min)]
console.log(closest)
```

我们用一个回调函数调用`map`，该回调函数返回`num`和`goal`之间的绝对差值。

然后我们找到与`Math.min`的差异的最小值。

然后我们得到与`indexOf`绝对差值最小的数字的索引，并将其传递给`arr`以得到最接近`goal`的数字。

所以我们得到了和上一个例子一样的结果。

# 结论

我们可以使用 JavaScript 数组和数学方法来获得与 JavaScript 数组中给定数字最接近的数字。

*更多内容请看*[***plain English . io***](http://plainenglish.io)