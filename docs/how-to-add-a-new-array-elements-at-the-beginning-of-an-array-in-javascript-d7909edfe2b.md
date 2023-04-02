# JavaScript 中如何在数组的开头添加一个新的数组元素？

> 原文：<https://javascript.plainenglish.io/how-to-add-a-new-array-elements-at-the-beginning-of-an-array-in-javascript-d7909edfe2b?source=collection_archive---------13----------------------->

![](img/1f1f65532850196557216ef8ff0c7f60.png)

Photo by [Ekaterina Grishina](https://unsplash.com/@mantikora?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在一个数组的开头添加一个新的数组元素是我们在 JavaScript 应用程序中经常要做的事情。

在本文中，我们将研究如何在 JavaScript 中的数组开头添加新的数组元素。

# 数组.原型.串联

将元素添加到 JavaScript 数组开头的一种方法是使用`concat`方法。

我们用一个包含我们想要添加的元素的新数组调用`concat`。

然后我们将现有的数组作为参数传入。

例如，我们可以写:

```
const array = [1, 2, 3]
const newFirstElement = 4
const newArray = [newFirstElement].concat(array)
console.log(newArray);
```

我们有一个`array`数组，我们想添加一个新的第一个元素。

`newFirstElement`是我们要添加的第一个元素。

为此，我们创建了一个包含`newFirstElement`的新数组。

然后我们用`array`调用`concat`，将`array`连接到我们创建的新数组。

返回两者组合的新数组，所以`newArray`是`[4, 1, 2, 3]`。

# Array.prototype.unshift

JavaScript 数组可用的`unshift`方法是专门为在数组开头添加元素而设计的。

元素的添加是就地完成的，所以它所调用的数组是变异的。

例如，我们可以写:

```
const array = [1, 2, 3]
array.unshift(4);
console.log(array);
```

那么`array`就是`[4, 1, 2, 3]`。

# 传播算子

我们可以使用 spread 操作符将元素从一个数组添加到另一个数组，方法是制作一个副本并将元素放入新的数组中。

例如，如果我们有:

```
const array = [1, 2, 3]
const newArray = [4, ...array];
console.log(newArray);
```

然后来自`array`的所有项目被分散到`newArray`中。

所以，`newArray`就是`[4, 1, 2, 3]`。

# 数组.原型.拼接

将元素添加到数组开头的另一种方法是使用`splice`方法。

`splice`就地改变它所调用的数组。

例如，我们可以写:

```
const array = [1, 2, 3]
array.splice(0, 0, 4);
console.log(array);
```

我们调用索引为`array`的`splice`来改变第一个参数。

第二个参数是我们要从第一个参数中指定的索引开始移除的元素的数量。

最后一个参数是我们想要在第一个参数的索引之前插入的元素。

因此，`array`应该是`[4, 1, 2, 3]`。

# 结论

我们可以使用数组方法或 spread 操作符，通过 JavaScript 将项目添加到数组的开头。

*更多内容看*[***plain English . io***](http://plainenglish.io/)