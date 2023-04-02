# JavaScript 中的引用透明性

> 原文：<https://javascript.plainenglish.io/referential-transparency-in-javascript-48d056eb89b0?source=collection_archive---------8----------------------->

![](img/e61059fe11f99e6d4e9e334698493e22.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

在 JavaScript 中，函数式编程是一种我们创建函数的模型。也就是说，仅仅依靠它输入来完成它的逻辑。这证实了一个函数在被多次调用时，能够成功地返回相似的结果。该函数同样不会改变外部世界的任何数据，这对可缓存和可测试的代码库很重要。

由于所有函数都为相同的输入返回相似的值，因此函数的这一属性被称为引用透明性。在本帖中，我们将详细讨论引用透明性。

![](img/9465afd8554aef9fb3c20d706da8e42f.png)

# 描述

引用透明性用于许多领域，例如数学、逻辑、语言学、哲学和编程。在这些领域中，它的含义都发生了很大的变化。

在数学中，指称透明是表达式的内容。可以用其他的表达来代替。那些有着相似价值观的人无法以任何方式改变结果。

编程中的引用透明性与程序有关。程序是由子程序组成的，而子程序本身就是程序。它也与那些子程序相关。子程序可以用方法来表示。

为了更好地理解，参照透明度见下面的例子。

```
var identity = (i) => { return i }
```

*   我们在上面的代码片段中定义了一个名为 identity 的简单函数。
*   这个函数返回我们作为它输入传递的任何东西。
*   也就是说，如果我们传递 10，它将返回值 10。
*   因为功能仅仅是充当镜子和身份。
*   我们的函数只对传入的参数“I”起作用。
*   我们的函数中没有全局引用。

# 替代模型

*   目前，该函数用于其他函数调用之间，如下所示:

```
sum(4,5) + identity(1)
```

*   通过我们的参照透明性定义，我们可以把上面的陈述变成这样:

```
sum(4,5) + 1
```

*   这时这个过程叫做替代模型。
*   通过，我们可以直接用它的值代替函数的结果。
*   一般来说，由于函数的逻辑不依赖于其他全局变量。
*   这导致了等同的代码和缓存。
*   我们可以轻松地运行上面的函数，几个线程甚至不需要同步。
*   同步的动机来自于线程在等价运行时不应该处理全局数据的细节。
*   [遵循参照透明性的函数](https://www.technologiesinindustry4.com/)只依赖于其参数的输入。
*   因此，线程可以在没有任何锁定机制的情况下运行。
*   同时，对于给定的输入，该函数返回相同的值。
*   我们实际上可能会缓存它。例如，有一个叫做阶乘的函数。
*   计算给定数字的阶乘。
*   Factorial 将输入作为需要计算阶乘的参数。
*   我们都知道 5 的阶乘是 120。
*   如果用户第二次调用 5 的阶乘会怎样？
*   我们看到，如果阶乘函数像以前一样遵循引用透明性，结果将是 120。
*   它只取决于输入参数。
*   我们可以通过记住这些字符来缓存阶乘函数的值。
*   因此，如果第二次调用阶乘，输入为“5”，我们可以返回缓存的值，而不是再次计算。

*欲了解更多详情，请访问:*

[*https://www . technologiesinindustry 4 . com/2021/10/referential-transparency-in-JavaScript . html*](https://www.technologiesinindustry4.com/2021/10/referential-transparency-in-javascript.html)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)