# 如何在 JavaScript 中将数组解包成单独的变量？

> 原文：<https://javascript.plainenglish.io/how-to-unpack-an-array-into-separate-variables-in-javascript-eb8d90754380?source=collection_archive---------19----------------------->

![](img/0a43c4c2c5f0984a01b3d1c0c73de02e.png)

Photo by [Carl Flor](https://unsplash.com/@carlflor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通常，我们希望将 JavaScript 数组条目解包到它们自己的变量中。

在本文中，我们将了解如何用 JavaScript 将 JavaScript 数组解包成单独的变量。

# 使用析构语法

我们应该使用 JavaScript 数组析构语法将 JavaScript 数组条目解包到它们自己的变量中。

例如，我们可以写:

```
const [x, y] = ['foo', 'bar'];
console.log(x);
console.log(y);
```

然后我们将`'foo'`分配给`x`，将`'bar'`分配给`y`。

所以`x`是`'foo'`，而`y`是`'bar'`。

我们可以把数组直接赋给左边的变量。

例如，我们可以写:

```
const arr = ['one', 'two'];
const [one, two] = arr;
```

我们将`'one'`分配给`one`，将`'two'`分配给`two`。

此外，我们可以设置一个默认值，以防变量没有赋值。

为此，我们编写如下代码:

```
const [one = 'one', two = 'two', three = 'three'] = [1, 2];
console.log(one);
console.log(two);
console.log(three);
```

我们用左边的赋值语句给`one`、`two`和`three`赋值默认值。

所以`one`是 1，`two`是 2，`three`是`'three'`。

`three`是`'three'`,因为没有分配给它的数组条目。

# 结论

通过使用析构语法，我们可以很容易地将 JavaScript 数组条目解包到它们自己的变量中。

*更多内容尽在* [***说白了***](http://plainenglish.io/)