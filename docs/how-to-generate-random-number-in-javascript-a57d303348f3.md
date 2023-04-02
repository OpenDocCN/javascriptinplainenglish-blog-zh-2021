# 如何在 JavaScript 中生成一个随机数

> 原文：<https://javascript.plainenglish.io/how-to-generate-random-number-in-javascript-a57d303348f3?source=collection_archive---------14----------------------->

![](img/61352aeefb79004a85b31602fbb1eec0.png)

How to generate random number in Javascript

> 要在 JavaScript 中生成随机数，只需要几个内置方法。我们将使用数学模块的随机和地板方法。

有时，出于某种原因，您可能希望在 JavaScript 中生成随机数。不用为此绞尽脑汁，数学模块提供了两个有用的内置方法，这就是我们将要使用的方法。

我们将在 JavaScript 中使用的第一种生成随机数的方法是 **Math.random()** 。然后我们将使用 **Math.floor()** ，这样我们就可以得到一个随机值。

## Math.random()

Math.random()将给出我们想要的值。不过值得注意的是，这个方法会给你一个在 **0 到 1** 之间的随机值。

所以，这意味着我们需要将十进制数值转换成整数。为此，我们需要将 Math.random()的结果乘以我们希望我们的值位于其下的最大整数。

例如，如果我们想要 100 以下的随机值:

```
let randomValueUnder100 = Math.random() * 100;
console.log(randomValueUnder100);
```

然而，如前所述，这将为我们提供十进制值，这就是下一部分结束 Javascript 中生成随机数的循环的原因。

## Math.floor()

该方法接受一个参数，然后将参数向下舍入到最接近的整数。

比如说:

```
let val = Math.floor(1.23);
console.log(val);
```

你的输出将是 1。

因此，我们将使用它来舍入我们生成的值，如下所示:

```
let randomValueUnder100 = Math.random() * 100;
let val = Math.floor(randomValueUnder100);
console.log(val);
```

现在，你应该看到一个整数。

当然，您也可以使用 Math.ceil()并传入 randomValueUnder100 ，但是正如您所猜测的，这将向上舍入值，但是我们想要的是向下，小于 100。

## 结论。

就这么简单。

现在，由于 Math.random()和 Math.floor()方法，您已经了解了如何在 Javascript 中使用 get 随机数。

好了，这就是这首曲子。

编码快乐！

> 有兴趣学习 **JavaScript** 吗？在我的网站上查看类似的精彩文章:[沉迷于代码> JavaScript](https://bingeoncode.com/category/javascript)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)