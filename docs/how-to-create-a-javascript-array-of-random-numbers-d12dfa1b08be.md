# 如何创建随机数字的 JavaScript 数组

> 原文：<https://javascript.plainenglish.io/how-to-create-a-javascript-array-of-random-numbers-d12dfa1b08be?source=collection_archive---------12----------------------->

![](img/a1ad0f2042e424ae8949b667489a49fe.png)

Photo by [Susan Holt Simpson](https://unsplash.com/@shs521?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> 创建一个随机数字的 JavaScript 数组非常容易。我们将使用一些方法和几行代码来实现这一点！

有时，您可能会发现自己需要创建一个随机数字的 JavaScript 数组。嗯，这并不像听起来那么难。为此，我们将在 JavaScript 中使用完全内置的方法。

为了创建一个随机数字的 JavaScript 数组，我们将采取**两个步骤。**第一步是创建实际的数组，另一步是用随机数填充数组。

因此，在我们的示例中，我们将在取款机上使用一个假设的数组，该数组处理随机的票号，以便这些数字随后被发送给用户。

这样一个随机数字的 JavaScript 数组只需要在给定的**最大值**和给定的**最小值**之间有一个正整数。

## 1.定义 JavaScript 数组。

我们首先需要的是我们需要的实际阵列。此数组将具有最大数量的票证编号，这与最大可能的票证编号相同。为了做到这一点，我们将会这样做:

```
let maxTicketNumber = 1000;
let minTicketNumber = 0;
let ticketNumbers = Array(maxTicketNumber).fill(0);
```

上面的代码会给我们一个随机的 **ticketNumbers** 数组，它只是一个外壳，有尽可能多的空位。然后，我们将使用 **Array.fill()** 在我们的 JavaScript 随机数数组中填充最初的**零**。

## 2.生成随机数。

现在，该是有趣的部分了，使用数学模块来创建随机数，并填充出 ticketNumbers JavaScript 随机数数组。

因为我们已经有了 ticketNumbers 数组，它有空槽，我们将简单地把它转换成一个实际上有随机槽的数组。为此，我们将使用 **Array.map()** 方法。

在我们的**范围内。map** 方法，我们将包装代码，它将把我们的 ticketNumbers 转换成随机数数组。嗯，就是这么简单，就像这样:

```
let maxTicketNumber = 1000;
let minTicketNumber = 0;
let ticketNumbers = Array(maxTicketNumber).fill(0);

ticketNumbers.map(_ => {
  // our random generation code will go here
});
```

举个例子，array.map()是做什么的。它接受一个输入并将其转换为另一个 ***事物*** 并返回该事物，因此我们分配给地图结果的数组中应该有新的 ***事物*** 。这只是总结，不在本指南的讨论范围内。

## 3.添加随机数字代码的 JavaScript 数组。

所以，我们现在将更新最后一个代码片段，让它给我们随机数。这就是我们使用 **Math.random()** 和 **Math.floor()** 方法的地方。

如果您不熟悉上述方法，我们将在页面底部链接一个教程。但是，我们更新的代码应该如下所示:

```
let maxTicketNumber = 1000;
let minTicketNumber = 0;
let ticketNumbers = Array(maxTicketNumber).fill(0);

ticketNumbers = ticketNumbers.map(_ => {
  const seed = [Math.random() * minTicketNumber, Math.random() * maxTicketNumber];
  const randomValue = seed[Math.floor(Math.random() * seed.length)];
  return Math.round(randomValue)
});

console.log(ticketNumbers);
```

所以，让我们理解是什么改变了。

该行:

```
const seed = [Math.random() * minTicketNumber, Math.random() * maxTicketNumber];
```

会给我们两个数字的数组，一个数字使用 minTicketNumber 处理，另一个使用 maxTicketNumber 处理。

然后，我们需要从处理的值中随机选择一个值，这就是这行代码要做的:

```
const randomValue = seed[Math.floor(Math.random() * seed.length)];
```

这段代码所做的是从**种子**中选取一个值，并且是以随机的方式进行的，这就是为什么我们有 Math.floor(Math.random() * **种子**的原因。长度)作为数组索引。

这将给我们一个完整的数组索引用于查找。你可能很想使用 **Math.ceil()** ，但这可能会有问题，因为它将**向上舍入**，并且可能给出一个我们的 JavaScript 随机数数组中没有的索引。

最后，我们从我们的**返回结果。map()** 方法:

```
return Math.round(randomValue);
```

要测试这一点，请继续尝试记录输出:

```
console.log(ticketNumbers);
```

这会给你一个 JavaScript 随机数数组。

## 结论。

如您所见，拥有一个包含随机数的 JavaScript 数组并不困难。

现在您可以用 JavaScript 创建一个随机数数组，您也已经从 Math 模块学到了重要的方法，以及其他的数组内置方法。

那么，看看以前的文章，它可能会详细解释一些概念。

**快乐编码！**

> 有兴趣学习 **JavaScript** 吗？在我的网站上查看类似的精彩文章:[沉迷于代码> JavaScript](https://bingeoncode.com/category/javascript)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)