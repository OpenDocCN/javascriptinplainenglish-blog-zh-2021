# 如何在 JavaScript 中为 Math.log()指定基数？

> 原文：<https://javascript.plainenglish.io/how-to-specify-the-base-for-math-log-in-javascript-ce6e365a8d92?source=collection_archive---------9----------------------->

![](img/12c9013bc0efd82fd57ce7b826fcc2da.png)

Photo by [Mildly Useful](https://unsplash.com/@usefulcollective?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 Javascript 中，m 的`Math.log`方法只返回我们传入的参数的自然对数。

然而，我们可能想用其他底数的对数进行计算。

在本文中，我们将研究在 JavaScript 中改变对数计算底数的方法。

# 使用基本公式的变化

我们可以用换底公式来改变对数的底数。

为此，我们写道:

```
const log10 = (val) => {
  return Math.log(val) / Math.log(10);
}
console.log(log10(100))
```

我们创建了`log10`函数来计算以 10 为底的数的对数。

在函数中，我们通过将`val`的自然对数除以 10 的自然对数来使用基数规则的变化。

因此，控制台日志将记录 2，因为以 100 为基数 10 的日志是 2。

我们可以通过使函数除了接受取对数的值之外，还接受对数的基数，来使函数更加通用。

例如，我们可以写:

```
const log = (val, base) => {
  return Math.log(val) / (base ? Math.log(base) : 1);
}
console.log(log(100, 10))
```

我们创建了`log`函数，它使用`val`来获取 log of，使用`base`来获取 log。

然后，如果`base`不为 0，我们通过将`val`的自然对数除以`base`的自然对数来改变基本规则。

如果`base`是 0，我们除以 1。

因此，控制台日志将记录 2，因为我们以 10 为基数取 100 的对数。

# 结论

我们可以应用底数变化规则，用 JavaScript 检查对数的底数。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)