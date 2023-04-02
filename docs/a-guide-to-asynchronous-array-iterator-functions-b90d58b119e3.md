# 异步数组迭代器函数指南

> 原文：<https://javascript.plainenglish.io/a-guide-to-asynchronous-array-iterator-functions-b90d58b119e3?source=collection_archive---------9----------------------->

## 对于映射、减少、过滤、每一个和一些

![](img/d7ec803b211bbe828d1ed4277c92b5b7.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

JavaScript 的内置数组`map`、`reduce`、`filter`、`every`和`some`迭代器函数是我的第二天性。但是最近，我需要构建一些需要异步回调函数的功能。让我们看看如何实现这一点。

# 地图

`map`遍历数组，使用提供的回调函数计算每个元素的结果，并返回一个新的结果数组。

```
[1, 2, 3].map(i => i * 2);
// [2, 4, 6]
```

如果所提供的函数返回一个承诺，那么`map`将不会解析这个承诺。

```
[1, 2, 3].map(async i => i * 2);
// [Promise, Promise, Promise]
```

但是解决这个问题非常简单。Promise 提供了一个内置的`Promise.all`函数，该函数将解析一个数组中的所有承诺——这正是我们期望从`map`得到的输出。

```
await Promise.all([1, 2, 3].map(async i => i * 2));
// [2, 4, 6]
```

# 减少

`reduce`遍历数组，并根据提供的回调缩减器函数聚合一个值。

```
[1, 2, 3].map((acc, i) => acc + i, 0)
// 6
```

如果提供的函数返回一个承诺，`reduce`将出错。

```
[1, 2, 3].reduce(async (acc, i) => {
  return acc + i;
}, 0);
// Error
```

为什么？因为`acc`是前一次迭代的响应，所以它本身就是一个承诺——并且您不能在一个承诺上聚合。在聚集之前，您需要首先解决`acc`。

```
[1, 2, 3].reduce(async (acc, i) => {
  return (await acc) + i;
}, 0);
// 6
```

# 过滤器

`filter`遍历数组并返回一个新数组，该数组只包含通过回调测试函数的元素。

```
[1, 2, 3].filter(i => i < 3);
// [1, 2]
```

如果提供的过滤函数返回一个承诺，`filter`将不会像预期的那样工作，而是返回整个数组。这是因为异步函数返回一个承诺，但是过滤器函数不解析该承诺。相反，它直接使用 promise，其计算结果为`true`，导致过滤函数在结果中包含该元素。

```
[1, 2, 3].filter(async i => i < 3);
// [1, 2, 3]
```

不幸的是，过滤器不支持承诺，但您可以使用`map`间接获得结果。

```
const array = [1, 2, 3];
const mapResult = await Promise.all(array.map(async i => i < 3));
array.filter((_, idx) => mapResult[idx]);
// [1, 2]
```

首先，使用在之前[提到的异步`map`方法，我们计算元素是否通过过滤功能测试，并解析所有的承诺。这会产生一个布尔数组，然后可以用它来确定原始数组中的哪些元素应该包含在结果中。](#1a14)

# 每一/一些

`every`检查数组中的所有元素是否通过了提供的回调测试函数，`some`检查数组中至少有一个元素通过了测试。

```
[1, 2, 3].every(i => i < 3);
// false[1, 2, 3].some(i => i < 3);
// true
```

就像`filter`一样，如果提供的测试函数返回一个承诺，`every`和`some`就不会像预期的那样工作。相反，他们将总是返回`true`，因为未解决的承诺将评估为`true`。

```
[1, 2, 3].every(async i => i < 3);
// true[1, 2, 3].some(async i => i < 3);
// true
```

解决方案类似于`filter`的解决方案——通过使用异步`map`来评估测试并遍历结果。

```
const array = [1, 2, 3];
const mapResult = await Promise.all(array.map(async i => i < 3));
array.every((_, idx) => mapResult[idx]);
// falsearray.some((_, idx) => mapResult[idx]);
// true
```

这种方法的缺点是迭代中的每个元素都将被解析。一旦第一个`false`和`true`结果分别被计算，则`every`和`some`可以短路并立即存在，从而节省计算时间。为了匹配这种行为，您必须遍历数组，并使用常规的`for`循环一次运行一个测试函数。

```
const asyncFunction = async i => i < 3;let everyResult = true;
for (let i of [1, 2, 3]) {
  if (!(await asyncFunction(i))) {
    everyResult = false;
    break;
  }
}
// everyResult = falselet someResult = false;
for (let i of [1, 2, 3]) {
  if (await asyncFunction(i)) {
    someResult = true;
    break;
  }
}
// someResult = true
```

# 最后的想法

`map`、`reduce`、`filter`、`every`和`some`都可以处理异步回调函数，只需要稍微调整一下。虽然这里没有涉及，但是其他内置数组方法，如`find`、`findIndex`、`forEach`和`reduceRight`也可以使用相同的方法处理异步回调函数。你能想出怎么做吗？

# 资源

*   `[Array.map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)` 文献
*   `[Array.reduce](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)` [文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)
*   `[Array.filter](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)` [文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
*   `[Array.some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)` [文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
*   `[Array.every](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)`文档