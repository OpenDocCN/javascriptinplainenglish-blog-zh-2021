# 用 C 编程获得稳定、易测试和安全代码的最巧妙的方法

> 原文：<https://javascript.plainenglish.io/the-most-skillful-way-to-program-in-c-to-get-stable-easily-testable-and-above-all-secure-code-c9e84ca31c83?source=collection_archive---------14----------------------->

## 安全关键代码的编码规则。

![](img/3bc5dbc655fa378e0a5618104f7b40c1.png)

Photo by [Glenn Carstens-Peters](https://unsplash.com/@glenncarstenspeters?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在用 C 进行编程时，已经建立了一些适用并被认可的基本规则，特别是对于安全关键领域的软件开发。您可以详细了解编码规则——几乎每个有自尊的开发团队都至少有一套非常广泛的规则。这十个要素代表了一套清晰的规则。

## **编码规则 1:仅使用简单的控制结构**

在整个代码中应该只使用简单的控制流结构。特别是，应该避免 goto、直接或间接递归。

这使得代码更加清晰，更易于分析和评估。此外，避免递归会产生非循环代码图，可以更容易地分析堆栈大小和执行时间。

每个函数只允许一次返回跳转，这一事实使规则更加严格。

## **编码规则 2:音符内存分配**

在初始化阶段之后，不应该再有动态内存分配。这是因为 malloc()和 release (free())之类的分配函数以及垃圾收集经常表现出不可预测的行为，所以在实际操作中应该避免这种情况。

此外，程序中的动态内存管理是返回后内存使用错误的一个很好的来源。例如，超出内存区域等。

## **编码规则 3:函数不能超过 60 行**

任何函数都不应超过 60 行，即每个语句和声明一行。该功能应该能够打印在一页纸上。

这条规则只是为了代码的可读性。这听起来很老套，但它对跟踪编写的代码很有帮助——并且能够在有疑问的情况下快速找到并修复可能的安全漏洞。

## **编码规则 4:关注 assert()函数和断言密度**

每个函数的平均断言密度应该至少为 2。这是为了拦截在操作过程中不允许出现的所有特殊情况。断言必须没有副作用，并且应该被定义为布尔测试。在测试失败时调用的 assert()函数本身必须明确地纠正这种情况，例如，产生或返回一个错误代码。

调查显示，具有这种断言的代码测试例如函数、值、返回值等的前置和后置条件。，非常具有防御性，用于快速找到测试中的错误。此外，不受副作用的影响允许稍后在性能关键部分注释掉代码。

## **编码规则 5:在尽可能小的范围内声明数据对象**

所有数据对象都必须在最小的有效区域中声明。

这是隐藏数据的原则，以便不允许来自其他区域的更改。此外，无论是在运行时还是在测试时，它都有助于使代码尽可能简单易懂。

## **编码规则 6:检查和复核功能**

每个调用函数都必须检查被调用函数的返回值(如果有的话)，并且每个被调用函数都必须测试其范围内的所有调用参数。

这条规则可能是被违反最多的规则之一。但是测试，例如，被调用的函数是否成功，肯定是有用的。将返回值视为不相关是否仍然有意义，那么必须对此进行评论。

## **编码规则 7:限制预处理器的使用**

预处理器的使用必须仅限于头文件和简单的宏定义。复杂的定义，如变量参数列表、递归宏定义等。，是被禁止的。此外，条件编译应该保持在最低限度。

不幸的是，使用预处理器会大大增加软件开发和代码检查的混乱。因此，限制是有用的。使用条件编译可以创建的版本数量和相应的编译器开关数量呈指数增长:使用 10 个编译器开关，您会得到 210 = 1024 个不同的版本，所有版本都必须经过测试。

## **编码规则 8:限制指针的使用，但不要模糊它**

指针的使用必须保持在最低限度。基本上，只允许一级解引用。指针不能被宏或 typedef 混淆。禁止指向函数的指针。

对指针的限制应该是可以理解的。然而，尤其不应该妨碍代码检查人员的工作。

## **编码规则 9:代码检查和警告级别至关重要**

必须从第一天开始编译整个代码，以启用所有警告的最高警告级别。代码必须在没有警告的情况下编译。如果可能的话，必须每天用一个以上的代码分析器检查代码，并且没有警告。

这条规则应该仔细遵守，因为警告总是有意义的。如果警告被识别为错误，则必须重写代码，因为这也可能意味着代码检查器不理解该部分。

## **编码规则 10:设置循环上限**

所有循环必须有一个常数作为上限。这是因为代码检查工具必须很容易根据上限静态地确定循环运行的次数。

该规则用于防止无限循环。重要的规则是代码检查器必须能够识别上限。

然而，这个规则有一个例外:对于某些任务(进程调度器、用于无休止地运行程序的框架等)来说，总是存在被无限频繁地显式运行的循环(例如，while (1))。).这些当然是允许的。

满足该规则并在超过该上限时引入错误或纠正的一种可能性是所谓的 assert()函数(也参见硬件描述语言，如 VHDL)。如果超过了这个值，就调用这样一个函数，它可以启动适当的操作。将错误纠正合并到实际的源代码中是可能的，但是明确的介绍只是一个概述。

当你用 C 语言编程时，为了获得稳定的、易于测试的、最重要的是安全的代码，你的方法是什么？我希望这 10 个基本的编码规则开发者应该在通往安全软件的道路上内化。无论你是 C 编程的初学者还是进阶者:对于干净、安全关键的软件，牢记 10 条编码规则总是明智的。

*更多内容看*[***plain English . io***](http://plainenglish.io/)