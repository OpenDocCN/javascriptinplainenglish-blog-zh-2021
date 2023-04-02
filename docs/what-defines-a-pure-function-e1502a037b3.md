# 什么是纯函数？

> 原文：<https://javascript.plainenglish.io/what-defines-a-pure-function-e1502a037b3?source=collection_archive---------11----------------------->

## 理解 JavaScript 中定义纯函数的独特属性。

![](img/2c453f0557f5582c05fb894daab41111.png)

Photo by [Aurélien - Wild Spot](https://unsplash.com/@wildspot?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

完成 bootcamp 的编码后，我花了大部分时间来加深对 JavaScript 的理解。在我的整个研究过程中，我遇到了各种各样的术语，我知道这些术语，但我自己不能完全定义它们。今天，我们将学习其中一个术语，**纯函数**。

# 什么是纯函数？

简单来说，**函数**是接收输入然后返回输出的过程。一个**纯函数**有两个附加属性。

1.  给定相同的输入，纯函数将*总是*返回相同的输出。
2.  一个纯粹的函数没有副作用。

让我们更深入地研究一下这些具体的品质。

# 1.相同的输入将总是产生相同的输出

看一下下面的代码块。

```
const pureFunction = num => {
  return num * 10;
}pureFunction(5); // 50
```

给定一个参数 5，上述函数将始终返回 50，无论如何。

作为对比，我们来看看下面的函数。

```
const notPureFunction = num => {
  return num * Math.floor(Math.random() * (11 - 1) + 1);
}notPureFunction(5); // 15 (5 * 3)
notPureFunction(5); // 35 (5 * 7)
notPureFunction(5); // 20 (5 * 4)
```

你可以看到我们正在`notPureFunction`的正文中生成一个 1 到 10 之间的随机数。即使输入值相同，我们得到的输出也各不相同。立刻，我们知道它是**而不是**一个纯函数。

# 2.不会产生副作用

一个纯粹的函数必须没有副作用。常见副作用的例子包括:

1.  变异输入
2.  在函数外部修改变量
3.  HTTP 呼叫
4.  `console.log`

下面，我们有一个不纯的函数。它接受两个参数，一个数组和一个要添加到数组中的值。

```
const myBasket = ['apple', 'orange']const addFruitToBasket = (basket, fruit) => {
  basket.push(fruit)
  return basket
}addFruitToBasket(myBasket, 'strawberry') // ['apple', 'orange', strawberry'] 
// myBasket is now equal to ['apple', 'orange', strawberry']
```

当`addFruitToBasket`执行时，函数外部定义的值会改变。这是一个副作用。我们马上知道`addFruitToBasket`是一个不纯函数。

让我们把`addFruitToBasket`调整成一个纯函数。

```
const myBasket = ['apple', 'orange']const addFruitToBasket = (basket, fruit) => {
  const newBasket = [...basket]
  newBasket.push(fruit)
  return newBasket
}addFruitToBasket(myBasket, 'strawberry') // ['apple', 'orange', strawberry'] 
// myBasket is unchanged, still equal to ['apple', 'orange']
```

现在，当`addFruitToBasket`执行时，我们正在创建一个新数组。`myBasket`不受影响，函数之外的任何内容都不会改变。

# 结论

纯函数是函数式编程的主要组成部分。因为它们不会产生副作用，纯函数是非常便携的，可以很容易地到处移动。当给定相同的输入时，纯函数将总是返回相同的输出。这使得它们是可预测的，并提高了可测试性。这些特性允许您生成灵活且易于适应的代码。