# 如何在 JavaScript 中开始和完成 Switch 语句

> 原文：<https://javascript.plainenglish.io/how-to-start-and-complete-switch-statements-in-javascript-edf753f3e68b?source=collection_archive---------19----------------------->

![](img/f347d5db2b7cc29b3d72270c7315db99.png)

# 介绍

switch 语句根据不同的情况执行一段代码。switch 语句是 JavaScript 的“条件”语句的一部分，用于根据不同的条件执行不同的操作。使用开关选择要执行的不同代码块之一。这是对于长的、嵌套的 *if* 和 *else* 语句的完美解决方案。

# 描述

switch 语句评估表达式。然后，表达式的值等于结构中每个事例的值。如果匹配，则执行相关的代码块。switch 语句经常与 break 或 default 关键字一起使用。这两个都是选修。break 关键字向下切换块。这将停止块内更多代码和案例测试的执行。如果省略 break，则执行 switch 语句中的下一个代码块。如果没有大小写匹配，default 关键字需要运行一些代码。开关中只能有一个默认关键字。虽然这是可选的，但是建议我们使用它，因为它可以处理意外情况。

# 如何开始切换语句？

仔细想想这一连串的条件语句。

```
if (dayOfWk === “Sat” || dayOfWk === “Sun”) {alert (“Whoopee!”);li>else if (dayOfWk === “Fri”) {alert(“TGIF!”);li>else {alert(“Shoot me now!”);li>
```

如果是周末，会显示`“Whoopee!”`警告。如果是星期五，将显示“TGIF”警报。如果是工作日，会显示“现在向我开枪”警告。这是可行的，但是有点笨拙和难看，特别是当我们有很多条件要测试的时候。是时候让我们学习一个更优雅的替代方法了，我们可以用它来测试各种条件，switch 语句。我们需要测试的条件越多，我们就越喜欢 switch 语句。此 switch 语句保留了示例以外的功能。

```
switch (dayOfWk) {case “Sat” :alert (“Whoopee”);break;case “Sun” :alert(“Whoopee”);break;case “Fri” :alert(“TGIF!”);break;default :alert(“Shoot me now!”);li>
```

我现在只需要关注上面代码的前三行。以关键字 switch 开头。与之相反的是被测试的变量，在括号里。然后有一个左花括号。

1.  第一个选项，变量 dayOfWeek 的值为“Sat”。以关键字 case 开始。然后是正在尝试的值，“Sat”。然后是空格和冒号。
2.  测试通过时执行的语句—如果 dayOfWeek 实际上具有值“Sat”。这个语句是缩进的。如果测试通过，可以执行任意数量的语句。

# 如何完成 switch 语句？

if 语句的第一行后面是条件为真时执行的语句。switch 语句的工作方式类似。在每个 case 子句下面的行中有一个如果 case 为真就会执行的语句。如果情况为真，则执行的代码再次缩进两个空格。由于通用惯例，它缩进了一些量。对于多少是最好的，意见不一。标准化为两个空格的缩进，这很常见，但远非通用。

那为什么除了最后一个案例之外的所有案例都包含 break 语句呢？JavaScript 有一个不合时宜的巧合是在发现真实案例之后。JavaScript 不仅直接在那种情况下执行语句。它执行其下所有案例的所有语句。因此，在找到真正的原因并执行条件代码后，我们需要通过编写 break 语句跳出 switch 块。例如，如果我们省略了上面代码中的 break 语句，就会出现这种情况:

1.  一个警告显示“万岁！”
2.  第二个警告显示“万岁！”
3.  第三个警告显示“TGIF！”
4.  第四个警告显示“现在向我开枪。”

现在让我们看看第 11 行。

```
default :alert(“Shoot me now!”);li>
```

关键字 default 的作用与 if…else 语句中的 else 类似。如果没有一个条件满足，它后面的代码就会执行。在上面的例子中，如果 dayOfWk 不是“Sat”、“Sun”或“Fri”——如果它是这三个值之外的任何值——就会显示一个警告，说“现在向我开枪”注意 default 后面有一个空格和一个冒号，就像它上面的 case 子句一样。另外，注意没有 break 语句。

这是因为 default 总是排在最后，这意味着它下面没有不合适执行的语句。Default 代码是可选的，就像 switch 语句中 if 语句后的 else 代码是可选的一样。没有默认代码，如果没有一个案例测试为真，什么都不会发生。谨慎的编码人员会在最后一个条件后包含一个 break 语句作为保险，即使在没有默认代码的情况下这可能是多余的。如果我们以后决定在末尾添加一个新的条件，我们就不必为了避免一连串灾难性的语句而在它上面的块中添加一个 break。

*欲了解更多详情，请访问:*

[](https://www.technologiesinindustry4.com/2021/06/how-to-start-and-complete-switch-statements-in-javascript.html) [## JavaScript 中如何开始和完成 switch 语句？-工业 4.0 的新兴技术

### 简介 switch 语句根据不同的情况执行一段代码。switch 语句是…

www.technologiesinindustry4.com](https://www.technologiesinindustry4.com/2021/06/how-to-start-and-complete-switch-statements-in-javascript.html) 

*更多内容看**[***说白了. io***](http://plainenglish.io/)*