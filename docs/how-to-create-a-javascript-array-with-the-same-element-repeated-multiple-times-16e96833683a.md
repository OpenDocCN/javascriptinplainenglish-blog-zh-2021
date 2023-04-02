# 如何创建同一个元素重复多次的 JavaScript 数组？

> 原文：<https://javascript.plainenglish.io/how-to-create-a-javascript-array-with-the-same-element-repeated-multiple-times-16e96833683a?source=collection_archive---------5----------------------->

![](img/4aff0ddf1c9da4839636c0ae03494590.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望创建一个 JavaScript 数组，其中的内容重复多次。

在本文中，我们将看看如何创建一个 JavaScript 数组，其中相同的元素重复多次。

# For 循环和数组. prototype.push

我们可以使用 for 循环运行`push`方法多次向数组中添加一个项目。

例如，我们可以写:

```
const fillArray = (value, len) => {
  const arr = [];
  for (let i = 0; i < len; i++) {
    arr.push(value);
  }
  return arr;
}const arr = fillArray(2, 5)
console.log(arr)
```

我们创建了具有`value`和`len`参数的`fillArray`函数。

`value`是我们要填入数组的数值。

`len`是返回数组的长度。

`arr`是具有重复值的数组。

创建`arr`后，我们使用 for 循环调用`push` `len`次，将同一个`value`推送到`arr`。

在我们调用它之后，我们得到一个返回的数组。

所以`arr`是`[2, 2, 2, 2, 2]`，因为我们用值 2 填充数组五次。

# 数组.原型.填充

另一种用值重复填充数组的方法是使用`fill`方法。

它需要一个带有要填充的值的参数。

我们可以将它与`Array`构造函数结合起来，创建一个给定长度的数组。

例如，我们可以写:

```
const arr = Array(5).fill(2)
console.log(arr)
```

我们调用`Array(5)`来创建一个有 5 个空槽的空数组。

然后我们用 2 调用`fill`，用 2 填充所有空槽。

因此`arr`与前面的例子相同。

# 展开运算符和 Array.prototype.map

另一种创建数组的方法是使用 spread 操作符和`map`方法。

例如，我们可以写:

```
const arr = [...Array(5)].map((_, i) => 2)
console.log(arr)
```

我们用`Array`创建了一个包含 5 个空槽的数组，并将其展开到数组中。

然后我们调用`map`在每个槽中返回 2。

最后，对于`arr`，我们得到了与之前相同的结果。

# 数组. from

`Array.from`是另一种方法，我们可以用它来创建一个数组，用相同的值填充整个数组。

它的工作原理是创建一个空数组并将空槽映射到我们想要的值。

例如，我们可以写:

```
const arr = Array.from({
  length: 5
}, i => 2)
console.log(arr)
```

我们用`Array.from`创建一个长度为 5 的空数组。

然后在第二个参数中，我们传入一个回调函数，将空值映射到 2。

所以我们得到了和以前一样的结果。

# 洛达什

我们可以使用`times`和`constant` Lodash 方法来返回一个从头到尾重复一个值的数组。

为此，我们写道:

```
const arr = _.times(5, _.constant(2));
console.log(arr)
```

`constant`方法确保我们重复元素。

因此`arr`与其他示例的值相同。

我们可以用`fill`方法更容易地做到这一点。

为此，我们写道:

```
const arr = _.fill(Array(5), 2);
console.log(arr)
```

我们将空数组传入第一个参数，并将值传入第二个参数。

# 结论

我们可以使用 JavaScript 数组方法或 Lodash 方法用相同的值填充数组。

*更多内容请看*[***plain English . io***](http://plainenglish.io)