# JavaScript 中的短路评估

> 原文：<https://javascript.plainenglish.io/short-circuit-evaluation-667d01b54172?source=collection_archive---------17----------------------->

## 解释编程概念，使用 JavaScript 进行短路评估

![](img/239c20cc8ceb2faa285eb54a91369ff8.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是短路评估？

在编程中，许多语言使用所谓的短路评估。短路评估的概念是，当整个语句已经被确定为真或假时，跳过条件语句中布尔表达式的第二部分的评估。

因此，检查使语句为真或为假的表达式后面的部分变得没有必要。如果计算结果为真，编译器就跳过它，继续处理语句中的下一行代码，如果计算结果为假，就退出条件语句。

# 用 JavaScript 实现短路评估

为了实现短路评估，让我们以下面的条件语句为例进行尝试。

首先，我们将`isTimeToCode`和`needsCoffee`变量都设置为真。现在，在表达式中，我们包含了`!`(读作逻辑非运算符)，使我们的`isTimeToCode`变量指向 false 而不是 true。由于我们的布尔表达式`(!isTimeToCode && needsCoffee)`现在说的是假和真，而不是真和真，表达式的`needsCoffee`部分将被跳过，因为没有必要检查它，因为条件无论如何都会评估为假。*所以看起来我们今天不会煮咖啡和编码了！:(*

# 通过短路评估避免错误

让我们来看一个更复杂的例子，看看短路评估在什么情况下会真正派上用场。

例如，我们将这个包含一年中四季名称的 Javascript 对象。

现在以下面的条件语句为例，我们在`seasons`对象中检查季节和月份。

既然`"Fall"`不在我们的`seasons`对象中，你认为这里会发生什么？要投个`[TypeError](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/TypeError)`。

```
Uncaught TypeError: Cannot read properties of undefined (reading 'isMonth')
```

在这种情况下，我们可以利用短路评估。让我们修改我们的表达式，首先检查`"Fall"`是否在我们的`seasons`对象中，然后调用它的`isMonth()`方法。

这里我们使用短路求值，所以如果我们的`seasons`不包含`"Fall"`，我们将忽略条件的后半部分，避免得到`TypeError`。

# 摘要

短路评估是避免在代码中执行额外的或不必要的任务的有用方法。在某些情况下，它也有助于避免错误，例如试图对一些不存在的数据执行操作。

*关于这个话题的更多信息，请查看我在下面提供的资源。*

*   [短路测评(面试蛋糕)](https://www.interviewcake.com/concept/javascript/short-circuit-evaluation?course=fc1&section=general-programming)
*   [编程中的短路评估(极客对极客)](https://www.geeksforgeeks.org/short-circuit-evaluation-in-programming/)
*   [短路评估(维基百科)](https://en.wikipedia.org/wiki/Short-circuit_evaluation#:~:text=Short%2Dcircuit%20evaluation%2C%20minimal%20evaluation,the%20expression%3A%20when%20the%20first)

*更多内容请看*[***plain English . io***](http://plainenglish.io)