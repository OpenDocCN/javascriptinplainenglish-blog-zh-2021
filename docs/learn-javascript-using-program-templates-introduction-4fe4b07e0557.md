# 使用程序模板学习 JavaScript:简介

> 原文：<https://javascript.plainenglish.io/learn-javascript-using-program-templates-introduction-4fe4b07e0557?source=collection_archive---------12----------------------->

![](img/db8bed5bb4e11c2fd467c0e81d04ee7d.png)

Photo by [Artem Sapegin](https://unsplash.com/@sapegin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

编程语言通常通过遵循语言的编程结构的索引来教授。声明和使用变量之后是写算术语句，之后是写 if 语句，之后是写循环等等。

但计算机编程主要是一种解决问题的活动，教授它的一种方式是关注你可以用这种语言解决的问题类型。

在这一系列文章中，我将通过围绕一组程序模板组织课程来教授 JavaScript 编程的基础知识。这些模板最初是在一本名为*设计 Pascal 解决方案*的书中介绍给我的，作者是 Michael J. Clancy 和 Marcia C. Linn。在这篇介绍性文章中，我将定义程序模板并演示其中的几个，以展示如何使用它们更有效地教授 JavaScript 编程。

# 程序模板

引用 Clancy 和 Linn 的话，程序模板是“由学生构建的可重用的编程知识的抽象”今天的程序员可能通过术语“设计模式”更好地了解它们

程序模板由它的描述和目的定义，然后是一些伪代码来说明模板是如何使用的。让我们看一个例子。我要介绍的第一个模板是*提示，然后读*。以下是该模板的描述和用途:

该模板用于向用户请求一个值，并将其读入一个变量。模板的实现是通过向用户写出一个信息性的消息，一个提示，告诉他们输入什么，然后调用一个过程(函数)来接收输入。

下面是*提示符的伪代码示例，然后阅读*:

*打印一条询问数值的消息
读取数值*

在伪代码之后，提供了一些代码示例。以下是一些例子(使用 SpiderMonkey JavaScript 编写):

```
putstr("Enter your name: ");
let name = readline();
putstr("Enter your salary: ");
let salary = parseInt(readline());
```

如果有要显示的输出，将最后执行，如下例所示。

这里是另一个示例程序模板——*输入、处理、输出*模板。

目的:

*输入、处理、输出*模板用于将一些值读入程序，处理这些值，并显示结果。

伪代码:

*输入所有数值
处理数值
输出结果*

代码示例:

```
// break up a three-digit number into separate digits
putstr("Enter a number: ");
let number = parseInt(readline());
let copy = number;
let third = copy % 10;
copy = parseInt(copy / 10);
let second = copy % 10;
copy = parseInt(copy / 10);
let first = copy;
print("First digit:",first);
print("Second digit:",second);
print("Third digit:",third)
```

样本输出:

```
Enter a number: 123
First digit: 1
Second digit: 2
Third digit: 3
```

# 为什么要使用计划模板？

在我的文章中，接下来我将解释代码示例中遇到的任何新的 JavaScript 特性。有时候会有很多解释，尤其是前几篇。正如你在上面的代码示例中看到的，我必须解释一下`putstr()`函数是做什么的，如何使用`let`关键字创建变量，如何使用`readline()`函数从键盘获得输入，以及如何将从`readline()`输入的字符串转换成数值。

这种演示顺序与大多数编程语言的教学方式有很大不同，但如果你想强调编程语言解决问题的本质，而不是仅仅讨论一系列编程语言结构和特性，这种顺序是首选的。

我仍然会一个一个地为读者积累 JavaScript 知识，但是我这样做是为了让读者更好地使用 JavaScript 解决问题。

# JavaScript 将如何呈现

在这些文章中，我将使用 SpiderMonkey JavaScript shell。我发现这个 shell 比更流行的 Node shell 更容易使用，主要是因为在 SpiderMonkey 中输入/输出更容易执行。当然，我提供的所有示例都可以用 Node 编写，除了输入/输出函数之外，不需要做任何更改。

如果你想在《蜘蛛猴》中关注我，请点击[这里](https://archive.mozilla.org/pub/firefox/nightly/latest-mozilla-central/)获取最新版本的 shell。

暂时就这样了。在我的下一篇文章中，我们将从学习如何实现*提示符开始，然后阅读*程序模板。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)