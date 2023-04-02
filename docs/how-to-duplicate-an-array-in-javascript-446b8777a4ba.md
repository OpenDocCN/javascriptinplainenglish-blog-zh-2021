# 如何在 JavaScript 中复制数组？

> 原文：<https://javascript.plainenglish.io/how-to-duplicate-an-array-in-javascript-446b8777a4ba?source=collection_archive---------1----------------------->

![](img/ea88a5c74979c2d6e1c8d4fcfd8040cd.png)

Photo by [Joe Green](https://unsplash.com/@jg?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

复制数组是我们在 JavaScript 应用程序中经常要做的事情。

在本文中，我们将看看如何在 JavaScript 中复制数组。

# 环

复制 JavaScript 数组的一种方法是使用循环。

例如，我们可以通过编写以下代码来使用 for-of 循环:

```
const arr = [1, 2, 3]
const clone = []for (const a of arr) {
  clone.push(a)
}
console.log(clone)
```

我们用 for-of 循环遍历`arr`并调用`clone`上的`push`将条目添加到`clone`中。

因此`clone`应该和`arr`有相同的条目。

我们还可以使用 while 循环来遍历数组。

例如，我们写道:

```
const arr = [1, 2, 3]
const clone = []let i = 0;
while (i < arr.length) {
  clone.push(arr[i])
  i++
}
console.log(clone)
```

我们通过方括号中的索引获取项目，并执行相同的`push`操作。

然后我们增加`i`值，在下一次迭代中移动到下一个元素。

此外，我们可以使用普通的 for 循环来做同样的事情:

```
const arr = [1, 2, 3]
const clone = []for (let i = 0; i < arr.length; i++) {
  clone.push(arr[i])
}
console.log(clone)
```

我们把改变索引的逻辑全部放在括号里。

# 数组.原型.切片

如果没有传入参数，`slice`方法将返回我们正在调用的数组的克隆。

例如，我们可以写:

```
const arr = [1, 2, 3]
const clone = arr.slice()
console.log(clone)
```

我们得到了和以前一样的结果。

# 数组. from

`Array.from`方法是一个静态数组方法，它允许我们从另一个数组创建一个数组。

因此，我们可以使用它来创建阵列的克隆。

它的第一个参数是一个数组或一个类似数组的对象，我们希望从它创建派生数组。

第二个参数是一个函数，它让我们映射第一个参数中的对象或数组的值，并将它们映射到不同的值。

例如，我们可以写:

```
const arr = [1, 2, 3]
const clone = Array.from(arr, a => a)
console.log(clone)
```

我们用`arr`数组调用`Array.from`。

函数只是原样返回值。

所以我们得到了和上一个例子一样的结果。

# 数组.原型.串联

`concat` array 实例方法也通过将它所调用的数组与我们传递给参数的数组相结合来返回一个数组。

因此，要使用它来克隆一个数组，我们可以编写:

```
const arr = [1, 2, 3]
const clone = arr.concat([])
console.log(clone)
```

或者:

```
const arr = [1, 2, 3]
const clone = [].concat(arr)
console.log(clone)
```

顺序无关紧要，因为我们只有`arr`和一个空数组。

无论哪种方式，我们都会返回一个`arr`的克隆。

# 传播算子

spread 操作符还允许我们复制一个数组。

例如，我们可以写:

```
const arr = [1, 2, 3]
const clone = [...arr]
console.log(clone)
```

用扩展运算符克隆`arr`。

所以我们得到了和前面例子一样的结果。

# 数组.原型.地图

`map`方法让我们返回一个数组，该数组包含从原始数组映射而来的值。

要返回原始数组的克隆，我们只需传入一个回调函数，该函数按原样返回被迭代的值。

例如，我们可以写:

```
const arr = [1, 2, 3]
const clone = arr.map(a => a)
console.log(clone)
```

用一个调用来调用`map`,该调用返回按原样迭代的值。

我们得到了和以前一样的结果。

# 结论

用 JavaScript 克隆数组有很多方法。

最简单的方法是使用 spread 运算符。

也很快。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***