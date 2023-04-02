# 如何在 JavaScript 中舍入浮点数？

> 原文：<https://javascript.plainenglish.io/how-to-round-floating-point-numbers-in-javascript-2a771597c5aa?source=collection_archive---------11----------------------->

![](img/6978cebde8e5e288b8b2920dfb4ffbd1.png)

Photo by [Ricardo Rocha](https://unsplash.com/@rcrazy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们的 JavaScript web 应用程序中，我们经常需要对浮点数进行舍入。

在本文中，我们将研究如何在 JavaScript 中舍入浮点数。

# number . prototype . to fix

JavaScript numbers 有一个`toFixed`方法，它返回一个字符串版本的数字，四舍五入到我们作为参数传入的小数位数。

例如，我们可以写:

```
const rounded = Number((6.6756854).toFixed(1));
console.log(rounded)
```

那么`rounded`就是`'6.7'`，因为我们在 1 中传递给了`toFixed`。

这使得它返回一个四舍五入到 1 位小数的字符串。

# 数学.圆

另一种舍入浮点数的方法是使用`Math.round`方法。

`Math.round`返回四舍五入后的数字而不是字符串。

因此，如果我们想对一个数字进行舍入，并将返回的结果保留为一个数字，就可以使用它。

例如，我们可以写:

```
const number = 6.6756854
const rounded = Math.round(number * 10) / 10;
console.log(rounded)
```

如果我们想四舍五入到小数点后 1 位，那么我们将`number`乘以 10。

然后我们在那个号码上调用`Math.round`。

然后我们除以 10 得到一个整数。

所以`rounded`就是`'6.7'`。

如果我们想四舍五入到小数点后两位，那么我们用 100 代替 10。

如果我们四舍五入到小数点后 3 位，我们用 1000 代替 10，以此类推。

# 数字.原型.精度

我们还可以使用 number 的`toPrecision`方法返回一个四舍五入到给定小数位数的数字。

它还返回一个数字而不是字符串。

例如，我们可以写:

```
const rounded = (6.6756854).toPrecision(2)
console.log(rounded)
```

参数是要舍入到的小数位数。

所以传入 2 作为第一个参数会将我们称之为的数字四舍五入到小数点后两位。

因此，`rounded`为 6.7。

# 数学.地板

我们可以使用`Math.floor`方法将一个数字向下舍入到最接近的整数。

例如，我们可以写:

```
const rounded = Math.floor(6.6756854)
console.log(rounded)
```

那么`rounded`就是 6。

# 数学.细胞

`Math.ceil`方法让我们将一个数字向上舍入到最接近的整数。

例如，我们可以写:

```
const rounded = Math.ceil(6.6756854)
console.log(rounded)
```

而`rounded`是 7。

# 结论

有各种各样的`Math`静态方法和 number 实例方法可以用来按照我们喜欢的方式舍入浮点数。

*更多内容请看*[***plain English . io***](http://plainenglish.io)