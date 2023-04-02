# 如何替换 JavaScript 数组中的一个项？

> 原文：<https://javascript.plainenglish.io/how-to-replace-an-item-in-a-javascript-array-2cb1a56e36d5?source=collection_archive---------3----------------------->

![](img/463d07c3c59cba04755c0354f424401e.png)

Photo by [Johan Mouchet](https://unsplash.com/@johanmouchet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想要替换 JavaScript 数组中的一个项目。

在本文中，我们将研究如何替换 JavaScript 数组中的一个项目。

# 数组.原型.索引和赋值

我们可以使用 JavaScript 数组的`indexOf`方法来查找数组中给定值的索引。

然后，我们可以使用该索引将新值赋给该索引。

例如，我们可以写:

```
const arr = [523, 353, 334, 31, 412];
const index = arr.indexOf(353);
if (index !== -1) {
  arr[index] = 1010;
}
console.log(arr)
```

我们用我们正在寻找的值调用`arr.indexOf`。

它将返回一个值的第一个实例的索引，如果它存在，否则返回-1。

因此，如果`index`不是-1，那么我们可以像在`if`块中所做的那样，通过赋值来用一个新的值替换给定索引处的值。

所以`arr`现在是:

```
[523, 1010, 334, 31, 412]
```

# 数组.原型.地图

我们可以使用`map`方法返回一个新数组，现有数组的条目映射到新值。

要用它来替换一个或多个值的实例，我们可以写:

```
const arr = [523, 353, 334, 31, 412];
const mapped = arr.map(a => a == 353 ? 1010 : a)
console.log(mapped)
```

我们用一个回调函数调用`map`，该回调函数检查被迭代的值`a`是否为 353。

如果是，那么我们用 1010 代替它。

否则，我们只返回现有的值。

所以`mapped`现在是:

```
[523, 1010, 334, 31, 412]
```

# Array.prototype.indexOf 和 Array.prototype.splice

我们还可以使用 JavaScript 数组的`splice`方法用一个新值替换给定索引处的值。

例如，我们可以写:

```
const arr = [523, 353, 334, 31, 412];
const index = arr.indexOf(353);
if (index !== -1) {
  arr.splice(index, 1, 1010);
}
console.log(arr)
```

我们用同样的方法得到 353 的指数。

但是我们没有赋值，而是用要移除的元素的`index`调用`splice`。

第二个参数中的 1 表示我们移除 1 个元素。

第三个参数是我们用来替换该项的值。

所以`arr`和第一个例子一样。

# 结论

我们可以使用数组方法用另一个值替换给定索引处的对象。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)