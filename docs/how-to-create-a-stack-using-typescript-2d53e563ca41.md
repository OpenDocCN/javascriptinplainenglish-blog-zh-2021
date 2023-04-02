# 如何使用类型脚本创建堆栈

> 原文：<https://javascript.plainenglish.io/how-to-create-a-stack-using-typescript-2d53e563ca41?source=collection_archive---------13----------------------->

您需要了解的关于 Stacks 的所有信息。

![](img/1d62b87c4b6811472c4e1880eeb3429f.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

理解数据结构对任何开发人员都很重要，不管是什么样的堆栈。这就是为什么在本文中，我将介绍其中一种数据结构。**堆栈。**

# 什么是堆栈？

虽然我已经在我的文章 [4 中讨论了堆栈是什么，但是每个开发人员都应该知道](https://bookeraziz.medium.com/4-data-structures-every-developer-should-know-368d156ea384)数据结构。我将快速复习一下基本概念。

堆栈就像[队列](/how-to-make-a-queue-in-typescript-b56416970670)一样，但是有一个微妙的区别。队列遵循先进先出的概念，堆栈遵循后进先出的概念！

这意味着堆栈不会在先到先得的基础上运行。相反，进入堆栈的最后一个值也是第一个离开堆栈的值！

当你想到一堆时，想想一堆盘子。您放在堆上的最后一个盘子也是您从堆中拿起的第一个盘子。

# 设计我们的堆栈

为了构建我们的堆栈，我们需要实现 5 个基本功能。其中两个功能是构成基本堆栈所必需的。最后三个增加了我们堆栈的额外功能。功能如下:

***推送():*** 推送功能负责在*顶部*添加*新项*

**弹出():**弹出功能负责*返回*和*移除*栈顶元素

**peek()**:peek 功能负责将堆叠顶部的元素*退回，无需*将其移除*。*

**isEmpty()**:isEmpty 函数将返回一个布尔值，以查看堆栈是否为空

**log stack()**:log stack 函数纯粹是为了调试的目的，因为它会将项目数组的所有当前值记录到控制台中。

# 创建堆栈类

第一步是在 TypeScript 中创建一个包含我们所有方法的类。这个类还将保存组成堆栈的项目数组。其代码如下所示:

构造函数中的…params 参数允许我们在初始化时用不同数量的值填充数组。

这给了我们作为开发人员更多的灵活性，因为我们不局限于固定数量的参数。

# 创建推送功能

创建我们的推送函数只需要一行代码和一个方便的 Array 方法。这个数组方法，unshift，将允许我们在堆栈的前面添加新的元素。其代码如下:

# 创建弹出功能

创建 pop 函数也只需要一行代码和另一个数组方法。这次我们将使用 shift 方法从堆栈中返回第一个元素。代码如下:

# 创建我们的 Peek 函数

peek 函数只包括返回数组*中的第一个元素，而不需要*移除它。代码如下:

# 创建我们的 isEmpty 函数

只有当数组长度等于 0 时，isEmpty 函数才会返回布尔值 true。代码如下所示:

如果这个语法让你有点困惑。别担心。这是一个三元运算符，我在我的文章 [*如何使用 JavaScript*](/how-to-create-if-statement-one-liners-using-javascript-e94a7bd96dcd) *创建 If 语句一行程序中对此进行了更深入的讨论。*长话短说三元运算符本质上是一行 if 语句。

# 创建我们的日志项功能

log items 函数是最简单的，它只包含一个 console.log，代码如下:

# 测试我们的堆栈

既然我们已经创建了我们的 stack 类，是时候测试它了。我将在每行提供一些代码和项目数组的值。代码在这里:

每个注释都有当时数组的值，真或假显示数组是否为空。如果你编程正确，你应该在 TypeScript 中有一个工作栈！

# 结论

感谢您阅读完我的文章**‘如何使用 Typescript 创建堆栈’。到目前为止，我希望你至少对什么是栈以及如何在 TypeScript 中创建栈有一个基本的了解。我希望你有美好的一天。**

*更多内容请看*[*plain English . io*](http://plainenglish.io/)