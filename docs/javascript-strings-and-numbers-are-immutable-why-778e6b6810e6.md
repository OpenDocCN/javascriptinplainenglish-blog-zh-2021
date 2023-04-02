# JavaScript 字符串和数字是不可变的——为什么？

> 原文：<https://javascript.plainenglish.io/javascript-strings-and-numbers-are-immutable-why-778e6b6810e6?source=collection_archive---------19----------------------->

![](img/f70af9d441d36f31d274b0158247aa1c.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> 长话短说:JavaScript 中的字符串和数字是通过值传递的，而不是通过引用传递的，因此它们是不可变的

首先，这可能看起来令人困惑，为什么在 JavaScript 中会发生这种情况。但这是因为你首先需要明白**不变性**不同于**再分配**！是的，这是交易的破坏者。

JavaScript 对字符串和数字的处理略有不同。

考虑下面的例子:

```
let someString = 'lorem ipsum';
```

事实上，有些字符串是不可变的，这意味着我们不能改变它。如果我们不重新分配它，那么在它的整个使用范围内，它将永远是‘lorem ipsum’。

你可以尝试的其他表达方式如下，它们将指导你:

```
// we are creating a new string from someString and not changing it
someString.replace('l', 'X')
```

这里的预期是，某个字符串现在将是“llrem ipsum”，但不，它不会，它仍然是“lorem ipsum”

这同样适用于数字，例如:

```
let someNumber = 12345;
```

someNumber 的值将始终是 12345，除非它被重新赋值。您不能修改其值。

## 现实推理

如果你想一下，1 永远是 1，我们不能说在某一点 1 是 2，而在另一点 1 是 3。还有，“A”永远是“A”，不可能是另一个时间点的另一个字母。然而，我们实际上可以改变“1”的含义(变量赋值为 1，表示 2)，同样“A”的含义也是如此

## 抽象推理

假设我们在现实世界中，不关注 JavaScript 字符串和数字。用这个类比。

如果我借给你钱，比如 10 美元，不管你什么时候还我，你都欠我 10 美元，因为我借给你的钱数不会变，不管通货膨胀与否，它仍然是 10 美元，因为 10 美元是我借给你的，你同意还我(按价值传递)

但是，如果我今天决定卖给你一块土地，并且我要求你在 10 年后将它卖回给我，那么你将按照当时所讨论的参考土地的价值(通过参考)将它卖回给我

所以，下次你尝试用 Javascript 字符串和数字做一些有趣的事情，比如试图“修改”它们的值，然后重新分配它们的“代表”(它们的变量。)

> 有兴趣学习 **JavaScript** 吗？在我的网站上查看类似的精彩文章:[沉迷于代码> JavaScript](https://bingeoncode.com/category/javascript)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)