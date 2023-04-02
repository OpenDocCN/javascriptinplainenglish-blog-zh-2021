# 如何在 JavaScript 中使用 for-of 循环获取循环计数器或索引？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-loop-counter-or-index-using-for-of-loop-in-javascript-111e7e320d4e?source=collection_archive---------18----------------------->

![](img/78761ce897c483216060e4ee307b16e4.png)

Photo by [Anthony Fomin](https://unsplash.com/@aginsbrook?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

for-of 循环是 JavaScript 附带的一个易于使用的循环，它让我们可以轻松地遍历数组和可迭代对象。

然而，没有办法直接得到被循环的元素的索引。

在本文中，我们将研究如何在 JavaScript 中用 for-of 循环获得循环计数器或索引。

# array . prototype .`forEach`

迭代数组时获取索引的一种方法是使用`forEach`方法。

我们可以传入一个回调函数，在第二个参数中循环传递项目的索引。

所以我们可以写:

```
const arr = [565, 15, 642, 32];
arr.forEach((value, i) => {
  console.log('%d: %s', i, value);
});
```

我们用一个回调函数调用`forEach`，这个回调函数的`value`和`arr`中的值被迭代。

`i`有`value`的索引。

所以我们得到:

```
0: 565
1: 15
2: 642
3: 32
```

# 数组.原型.条目

JavaScript 数组也有`entries`方法来返回包含项目索引和项目本身的数组。

例如，我们可以写:

```
const arr = [565, 15, 642, 32];
for (const [i, value] of arr.entries()) {
  console.log('%d: %s', i, value);
}
```

我们从数组条目中析构索引和值，然后用控制台日志记录这两个值。

所以我们得到:

```
0: 565
1: 15
2: 642
3: 32
```

结果。

# 结论

在每次迭代中，有几种方法可以用来遍历数组并访问索引和条目的值。