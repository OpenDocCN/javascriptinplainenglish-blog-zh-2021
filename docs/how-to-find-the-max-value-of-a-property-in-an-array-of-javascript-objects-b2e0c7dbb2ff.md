# 如何在 JavaScript 对象数组中求一个属性的最大值？

> 原文：<https://javascript.plainenglish.io/how-to-find-the-max-value-of-a-property-in-an-array-of-javascript-objects-b2e0c7dbb2ff?source=collection_archive---------3----------------------->

![](img/f88a326188a4eed0356a256ffb87dfae.png)

Photo by [Grailify](https://unsplash.com/@grailify?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们需要在一组 JavaScript 对象中找到一个属性的最大值。

在本文中，我们将研究如何在 JavaScript 对象数组中找到属性的最大值。

# Math.max

`Math.max`方法是一个静态方法，它让我们从传入的所有参数中找到最大值。

例如，我们可以写:

```
const array = [{
    "x": "8/11/2021",
    "y": 0.026572007
  },
  {
    "x": "8/12/2021",
    "y": 0.025057454
  },
  {
    "x": "8/13/2021",
    "y": 0.024530916
  },
  {
    "x": "8/14/2021",
    "y": 0.031004457
  }
]
const max = Math.max(...array.map(o => o.y))
console.log(max)
```

我们调用`array.map`来返回一个数组，该数组包含数组中每个对象的`y`属性值。

然后我们使用 spread 操作符将所有值作为参数传播到`Math.max`方法中。

然后我们得到`max`是 0.031004457，因为这是整个列表中最大的值。

# `Array.prototype.reduce`

`reduce`方法让我们从一组项目中计算出一个结果。

我们可以用它来寻找数组中某个属性的最大值。

例如，我们可以写:

```
const array = [{
    "x": "8/11/2021",
    "y": 0.026572007
  },
  {
    "x": "8/12/2021",
    "y": 0.025057454
  },
  {
    "x": "8/13/2021",
    "y": 0.024530916
  },
  {
    "x": "8/14/2021",
    "y": 0.031004457
  }
]
const maxObj = array.reduce((prev, current) => (prev.y > current.y) ? prev : current)
console.log(maxObj.y)
```

我们用一个带有`prev`和`current`参数的回调函数调用`reduce`。

`prev`已经计算出目前的结果。

`current`具有正在迭代的`array`的当前值。

我们在回调中返回具有更大`y`值的对象。

所以最后应该返回`y`值最大的对象。

并且`maxObj.y`应该与上例中的`max`相同。

# 数组.原型.排序

从项目数组中找到最大值`y`的另一种方法是用`sort`对数组进行降序排序。

例如，我们可以写:

```
const array = [{
    "x": "8/11/2021",
    "y": 0.026572007
  },
  {
    "x": "8/12/2021",
    "y": 0.025057454
  },
  {
    "x": "8/13/2021",
    "y": 0.024530916
  },
  {
    "x": "8/14/2021",
    "y": 0.031004457
  }
]
const [{
  y: max
}] = array.sort((a, b) => b.y - a.y)
console.log(max)
```

我们用返回`b.y — a.y`的回调来调用`array.sort`。

`a`和`b`是`array`中被比较的对象。

如果回调的返回值是正的，那么项目的顺序就会被交换。

否则，它们保持不变。

我们从左边的第一个元素开始析构`y`值，并将其设置为`max`的值。

并且`max`具有与先前示例相同的值。

# 结论

我们可以通过各种数组方法或带有 spread 操作符的`Math.max`方法从 JavaScript 对象数组中找到属性的最大值。

*更多内容看*[***plain English . io***](http://plainenglish.io)