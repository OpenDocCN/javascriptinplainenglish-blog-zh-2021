# 如何在不创建新数组的情况下，用另一个数组扩展现有的 JavaScript 数组？

> 原文：<https://javascript.plainenglish.io/how-to-extend-an-existing-javascript-array-with-another-array-without-creating-a-new-array-9ec8f5b73094?source=collection_archive---------7----------------------->

![](img/04b9ce6161c9b6a4ca196165181c2ecd.png)

Photo by [Ilse Orsel](https://unsplash.com/@lgtts?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

将另一个数组中的项目添加到 JavaScript 数组中是我们需要做很多的操作。

在本文中，我们将了解如何将现有 JavaScript 数组中的项目添加到另一个数组中。

# 数组.原型.推送

我们可以调用`push`方法向现有数组中添加条目。

我们可以传入任意多的参数，添加任意多的条目。

因此，我们可以使用 spread 操作符在`push`方法中展开数组中的项目，将数组作为参数展开到`push`中。

例如，我们可以写:

```
const array1 = [1, 2, 3]
const array2 = [4, 5, 6]
array1.push(...array2)
console.log(array1)
```

那么`array1`就是`[1, 2, 3, 4, 5, 6]`。

从 ES6 开始，我们可以使用 spread 运算符。

或者，我们可以使用`apply` to with `push`将一个数组中的项目追加到一个现有数组中:

```
const array1 = [1, 2, 3]
const array2 = [4, 5, 6]
array1.push.apply(array1, array2)
console.log(array1)
```

`apply`将`this`的值作为第一个参数。

第二个参数是`push`的参数数组。

因此`array1`与前面例子中的结尾相同。

我们也可以写:

```
const array1 = [1, 2, 3]
const array2 = [4, 5, 6]
Array.prototype.push.apply(array1, array2)
console.log(array1)
```

做同样的事情。

# 数组.原型.串联

此外，我们可以调用`concat`将一个数组中的项目追加到一个现有的数组中。

为此，我们写道:

```
let array1 = [1, 2, 3]
const array2 = [4, 5, 6]
array1 = array1.concat(array2)
console.log(array1)
```

来自`array2`的所有项目被添加到`array1`。

由于`concat`返回一个新数组，我们必须将返回的结果赋回给`array1`。

所以我们得到了和其他例子一样的结果。

# 传播算子

我们可以使用 spread 操作符将一个数组中的项目分散到另一个数组中。

为了使用它，我们写:

```
let array1 = [1, 2, 3]
const array2 = [4, 5, 6]
array1 = [...array1, ...array2]
console.log(array1)
```

我们将来自`array1`和`array2`的项目分散到一个新的数组中。

然后我们将结果赋回给`array1`。

所以我们得到了和以前一样的结果。

# 结论

我们可以使用 spread 运算符或数组方法将数组项添加到另一个数组中。

*更多内容看* [***说白了***](http://plainenglish.io)