# 编程中货币的最佳类型是什么？

> 原文：<https://javascript.plainenglish.io/what-is-the-best-type-for-currency-in-programming-83709ad38e5e?source=collection_archive---------5----------------------->

## 是浮动的吗？整数？小数？还是字符串？

![](img/c0397870b013dcb0d00f0b1e1fb0f195.png)

Photo by [Alexander Mils](https://unsplash.com/@alexandermils?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

没有**最好的类型**，但是有最差的。你知道大多数编程语言中的`0.1 + 0.2 != 0.3`吗？但是，我不会在本文中对此进行深入探讨。查看下面的文章了解更多信息。

[](https://betterprogramming.pub/why-is-0-1-0-2-not-equal-to-0-3-in-most-programming-languages-99432310d476) [## 为什么大多数编程语言中 0.1 + 0.2 不等于 0.3？

### 它等于 0.3000000000000004

better 编程. pub](https://betterprogramming.pub/why-is-0-1-0-2-not-equal-to-0-3-in-most-programming-languages-99432310d476) 

# 浮动/双精度

实际上，`float`和`double`是最糟糕的货币类型，因为它们不精确。与货币相关的计算必须精确，同时`float`和`double`会导致致命的问题。比如`0.1 + 0.2 != 0.3`的问题。

通常，`float`被用在图形库中或者可以忍受舍入问题的地方。

与许多其他编程语言不同，JavaScript 没有定义不同类型的数字，如整数、短整型、长整型、浮点型等。

遵循国际 IEEE 754 标准，JavaScript 数字总是存储为双精度浮点数。

# 整数

除了 JavaScript 之外，`int`在所有编程语言中都可用。`int`比`float`更适合货币。原因是你不必处理四舍五入的问题。

## 怎么会？

前端向后端发送货币相关数据时，金额必须是**美分**格式，例如`RM1.10 * 100 = 110sen`。当后端响应前端时，它应该乘以 100。

## 缺点

密苏里州的税率为 4.225%。如果你使用`int`，那么它需要更多的计算。比如`$1.10 * 4.225% = $0.046475`。如果是分格式`110¢ * 4.225% = 4.6475 cent`。这种情况下，你打算怎么处理？计算将变得更加复杂。

其次，`int`在大多数编程语言中有一个最小的可表示值范围。常见的 min-max `int`是 21.5 亿。钱可能超过一万亿

# 小数

`decimal`是一种合适的货币类型，因为它具有较高的精确度，并且易于避免舍入误差。然而，大多数语言没有`decimal`的类型

合适的数据类型在很大程度上取决于语言及其功能。

以下是我所知道的 JavaScript 解决方案:

1.  JavaScript 可以使用库 [bignumber.js](https://github.com/MikeMcl/bignumber.js/) 、 [accounting.js](https://github.com/openexchangerates/accounting.js/) 等。
2.  用`(0.1 * 10 + 0.2 * 10) / 10 === 0.3`解决浮点问题

# 需要注意的事项

想象一下，如果你有一个大规模的团队，用不同的语言开发服务。你打算怎么解决？每种语言都有其局限性。`decimal`不错，但是 JavaScript 里没有。你将需要一个额外的依赖或者手工制作一个`decimal`的类。

对于我的公司，我们使用`int`来解决它。我不鼓励你使用`int`作为货币，因为它适合我们的用例。在马来西亚，我们没有超过两位数的税率。我们使用的大多数语言都足以支持最少九万亿次(JavaScript 的 MAX_SAFE_INTEGER)甚至九万亿次。

即使 MySQL 的数据类型在用`DECIMAL(15,2)`，如果语言不支持 decimal 类型，还是会转换成 float。

我们在 Go 中使用`customtype`表示货币，下面的代码表示我的 HoD [SianLoong](https://medium.com/u/561fe5470f73?source=post_page-----83709ad38e5e--------------------------------)

![](img/9a8ff26ab18dc6eb432b2742a6080459.png)

Screenshot from [Language Guide (proto3)](https://developers.google.com/protocol-buffers/docs/proto3#scalar)

上面的截图是 protobuf 的类型会生成对应的类型。正如你所看到的，`int`有可能变成`string` PHP，因为它的最大值`int`是 21.5 亿。为了保持数据的准确性，超过 21.5 亿的数字将放在`string`而不是`int`

最后但同样重要的是，本文并不偏向我提到的任何一种类型。这取决于您的用例。如果你有什么想法，请发表评论，尽管批评，这样我们可以互相学习。

你可能想看看我的部门主管写的这篇精彩的文章

[](https://sianloong90.medium.com/how-to-optimise-your-sql-database-to-handle-million-records-part-1-748d68f2dee1) [## 如何优化您的 SQL 数据库来处理百万条记录—第 1 部分

### 数据处理可能会很混乱，尤其是当我们处理大量数据的时候。多年来，我们意识到…

sianloong90.medium.com](https://sianloong90.medium.com/how-to-optimise-your-sql-database-to-handle-million-records-part-1-748d68f2dee1) 

# 参考

1.  [https://developers.google.com/protocol-buffers/docs/proto3](https://developers.google.com/protocol-buffers/docs/proto3)
2.  [http://net-informations.com/q/faq/float.html](http://net-informations.com/q/faq/float.html)
3.  [https://stack overflow . com/questions/5356123/why-dont-applications-typically-use-int-to-internal-represent-currency-values](https://stackoverflow.com/questions/5356123/why-dont-applications-typically-use-int-to-internally-represent-currency-values)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)