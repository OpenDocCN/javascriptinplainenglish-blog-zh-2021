# 如何在 JavaScript 中交换两个变量？

> 原文：<https://javascript.plainenglish.io/how-to-swap-two-variables-in-javascript-c306f72100bd?source=collection_archive---------15----------------------->

![](img/e4137fb87c9f7789dde270acd2e3088c.png)

Photo by [Denise Jans](https://unsplash.com/@dmjdenise?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时在我们的 JavaScript 代码中，我们需要交换两个变量的值。

在本文中，我们将看看在 JavaScript 中交换两个变量的值的不同方法。

# 使用析构语法

交换两个变量的值的一种方法是使用析构语法。

例如，我们可以写:

```
let a = 5,
  b = 6;
[a, b] = [b, a];
console.log(a, b);
```

我们定义了分别为 5 和 6 的`a`和`b`值。

然后在第三行，我们使用析构来交换它们的值。

在右边，我们将`b`和`a`放入一个数组中。

然后在右边，我们通过打开`a`和`b`来析构数组条目。左侧的数组。

所以当我们加长最后一行的`a`和`b`的值时`a`是 6 而`b`是 5。

# 使用临时变量

我们还可以使用一个临时变量来帮助交换两个变量的值。

为了使用它，我们写:

```
let a = 1,
  b = 2,
  tmp;
tmp = a;
a = b;
b = tmp;
console.log(a, b);
```

我们定义了`a`和`b`分别为 1 和 2。

接下来，我们将`a`赋给`tmp`临时变量。

然后我们将`b`赋值给`a`。

最后，我们将`tmp`赋值给`b`，用`a`的先前值更新`b`。

因此，`a`现在是 2，`b`是 1。

# 结论

通过使用析构语法或使用临时变量，我们可以用 JavaScript 交换两个变量的值。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)