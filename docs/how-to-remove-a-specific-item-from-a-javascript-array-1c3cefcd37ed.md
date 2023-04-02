# 如何从 JavaScript 数组中移除特定的项？

> 原文：<https://javascript.plainenglish.io/how-to-remove-a-specific-item-from-a-javascript-array-1c3cefcd37ed?source=collection_archive---------15----------------------->

![](img/368c14110f5f0398c1285ba08e6bd4e4.png)

Photo by [Christina Rumpf](https://unsplash.com/@punk_rock_vegan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从 JavaScript 数组中移除一项是我们经常要做的事情。

在本文中，我们将研究如何从 JavaScript 数组中移除特定的项。

# 索引和拼接方法

从数组中移除一个项目的一种方法是使用`indexOf`方法来获取我们想要移除的项目的索引。

然后，我们可以使用`splice`方法删除具有给定索引的项目。

例如，我们可以写:

```
const array = [1, 2, 3];console.log(array);const index = array.indexOf(2);
if (index > -1) {
  array.splice(index, 1);
}
```

我们有`array`阵列。

然后我们调用`indexOf`来得到`array`中 2 的索引。

然后我们用`index`和 1 调用`splice`来删除从索引`index`开始的 1 个项目。

这意味着如果`index`大于-1，我们将删除`array`中带有`splice`的索引为`index`的项目。

如果项目在`array`中不存在，则`indexOf`返回-1。

# 该过滤方法

我们可以调用`filter`来返回一个没有我们想要移除的项目的数组。

例如，我们可以写:

```
let array = [1, 2, 3];
const value = 3
array = array.filter((item) => {
  return item !== value
})
```

我们有作为数组的`array`和作为要从`array`中移除的值的`value`。

然后我们用回调函数调用`filter`来返回`item !== value`。

这意味着我们希望由`item`返回的数组不包括值为`value`的项目。

所以，`array`应该是`[1, 2]`。

# 移除多个项目

如果我们想要移除多个项目，我们也可以使用`filter`方法，但是使用不同的回调。

要删除多个项目，我们可以写:

```
let array = [1, 2, 3];
const forDeletion = [2, 3]
const value = 3
array = array.filter((item) => {
  return !forDeletion.includes(item)
})
console.log(array)
```

我们用一个回调函数调用`array.filter`,该回调函数检查该项是否不在`forDeletion`数组中。

`forDeletion`是包含要删除的项目的数组。

所以如果它没有包含在`forDeletion`中，那么我们希望保留它们。

由于 2 和 3 在`forDeletion`中，这意味着只有 1 被保存在返回的数组中。

# 结论

数组实例的`includes`、`indexOf`、`splice`和`filter`方法可以方便地删除数组中的项目。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)