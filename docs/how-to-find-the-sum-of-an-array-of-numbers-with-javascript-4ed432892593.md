# 如何用 JavaScript 求一组数字的和？

> 原文：<https://javascript.plainenglish.io/how-to-find-the-sum-of-an-array-of-numbers-with-javascript-4ed432892593?source=collection_archive---------7----------------------->

![](img/671c23a4412417d98ed5947ffe611743.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

寻找一组数字的和是我们在 JavaScript 应用程序中经常要做的事情。

在本文中，我们将看看如何用 JavaScript 计算一组数字的总和。

# array . protocol . reduce

JavaScript 数组的`reduce`方法让我们可以从数组中获取数字，并轻松地将它们相加。

为此，我们写道:

```
const sum = [1, 2, 3, 4].reduce((a, b) => a + b, 0)
console.log(sum)
```

我们通过回叫调用`reduce`来帮助我们把数字加起来。

`a`是累加的结果，是部分和。

`b`是我们正在迭代的项目。

在第二个参数中，我们传入 0 来设置`a`的初始结果。

因此，`sum`为 10。

# 洛达什求和法

Lodash 有专门用于将数组中的数字相加的`sum`方法。

例如，我们可以写:

```
const array = [1, 2, 3, 4];
const sum = _.sum(array);
console.log(sum)
```

用`array`号数组调用`sum`。

# 环

我们可以使用 for-of 循环遍历一组数字，并将它们相加。

例如，我们可以写:

```
const array = [1, 2, 3, 4];
let sum = 0
for (const a of array) {
  sum += a
}
console.log(sum)
```

我们从`array`得到数字`a`，并将它们加到`sum`。

同样，我们可以使用一个`while`循环来遍历数字数组。

为此，我们写道:

```
const array = [1, 2, 3, 4];
let sum = 0
let i = 0;
while (i < array.length) {
  sum += array[i];
  i++
}
console.log(sum)
```

# Array.prototype.forEach

我们还可以使用`forEach`方法循环遍历数字数组，并将所有数字相加。

例如，我们可以写:

```
const array = [1, 2, 3, 4];
let sum = 0
array.forEach(a => {
  sum += a;
});
console.log(sum)
```

我们用回调来调用`forEach`。

然后在回调中，我们用第一个参数获取被迭代的值。

然后，我们将该值添加到`sum`。

# 结论

有几种方法可以用来用 JavaScript 计算一个数字数组中数字的和。

一种方法是使用`reduce`方法。

其他方法包括使用`for-of`循环、`while`循环或`forEach`循环遍历一个数组。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)