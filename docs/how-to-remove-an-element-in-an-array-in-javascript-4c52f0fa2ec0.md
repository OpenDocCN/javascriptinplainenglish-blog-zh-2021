# 如何在 JavaScript 中移除数组中的元素？

> 原文：<https://javascript.plainenglish.io/how-to-remove-an-element-in-an-array-in-javascript-4c52f0fa2ec0?source=collection_archive---------17----------------------->

![](img/1b158faf62a2d73c3ac4c36dfd04b2d6.png)

Photo by [Adrian Swancar](https://unsplash.com/@a_d_s_w?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 删除数组中的一个元素。

在本文中，我们将研究如何用 JavaScript 移除数组中的元素。

# 使用 Array.prototype.splice 方法

我们可以使用 JavaScript array `splice`方法从数组中移除一个项目。

例如，我们可以写:

```
const arr = [1, 2, 3]
arr.splice(1, 1)
console.log(arr)
```

用`splice`从`arr`中移除索引为 1 的项目。

`splice`的第一个参数是要删除的项目的索引。

第二个参数是从第一个参数中的索引开始要移除的项目数。

因此控制台日志显示`arr`为`[1, 3]`。

# 结论

我们可以用 JavaScript 数组的`splice`方法从 JavaScript 数组中移除一个项目。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)