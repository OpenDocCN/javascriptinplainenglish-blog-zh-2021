# 学习 JavaScript:循序渐进的方法

> 原文：<https://javascript.plainenglish.io/learning-javascript-a-sequenced-approach-1fcfae5a41ff?source=collection_archive---------7----------------------->

## 第 1 部分:变量和数据类型

![](img/6dce970c8acbd2b5100d6b8a17eaa2d7.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习如何使用编程语言的第一步(除非您使用的是函数式编程语言)是学习如何声明变量并将数据赋给它们。除此之外，您还应该了解可以存储在变量中的数据类型。

在本文中，我将向您介绍如何在 JavaScript 中声明数据并将数据赋给变量。我也给你介绍两个程序模板——*Read，然后提示*和*变量交换*。我还将向您展示一些语法模板，您应该与程序模板一起学习。

让我们开始吧。

# JavaScript 数据类型

JavaScript 被称为*弱类型*语言，因为 JavaScript 变量可以保存任何类型的数据。这与*强类型*语言相反，在后者中，一旦变量被赋值，它就只能存储相同值类型的数据。

尽管 JavaScript 是弱类型的，但它仍然有数据类型。只是语言在幕后处理数据输入的杂务，所以程序员不必担心。大多数程序员认为这是一件喜忧参半的事情。

基本的 JavaScript 数据类型有:

*   数字
*   线
*   布尔型
*   目标

这些并不是唯一的 JavaScript 数据类型，但是它们是你在第一次学习 JavaScript 时应该熟悉和理解的。

# JavaScript 变量

在 JavaScript 中处理数据的一种方法是将数据存储在一个变量中，然后以某种方式操纵该数据。变量是存储数据的内存位置的名称。创建变量有一些规则。第一条规则是变量必须以字母字符开头。第一个字符应该是小写字符，因为大写字母用于 JavaScript 中的其他内容。

在第一个字母字符之后，其余的字符可以是其他字母和数字，符号如$和%，以及下划线字符。一般来说，不要在变量名中使用任何符号是一个很好的经验法则，因为它们会降低程序的可读性。在另一篇文章中，我会有更多关于可读性的内容。

一旦你知道了变量的名字，你就可以在程序中使用它了。这样做的第一步是声明变量并给它赋值。这里有一个模板，描述了在 JavaScript 中变量应该如何声明和赋值:`*let variable-name = expression;*`

以下是一些例子:

```
let salary = 40000;
let name = "Paul McCartney";
let ratio = 2 + .02;
let flag = false;
```

对于那些熟悉 JavaScript 的人来说，你可能会注意到我并没有教你如何用`var`关键字声明变量。使用 var 进行变量声明有几个问题已经用关键字`let`解决了，所以我将只演示使用 let 创建新变量。在后面的文章中，我将讨论`var`关键字及其问题。

出于连续性的考虑，我还应该提到，您可以声明一个新的变量，只需将数据赋给它，根本不需要使用`let`关键字，就像这样:

```
salary = 30000;
name = "Mike";
```

如果您想以这种方式处理变量，您可能想切换到 Python。我将继续教导变量应该使用`let`关键字来声明和分配数据。

像这样的一行:

```
salary = 30000;
```

称为赋值语句。该语句用于存储变量中的值。赋值语句有一个语法模板。这是:

*变量名=表达式；*

注意赋值语句使用等号。这并不是要表达“平等”，如“工资等于 30000。”取而代之的是，赋值语句表达了一个动作——“薪金得到值 30000。”

如果您愿意，可以在赋值之前声明一个变量，如下所示:

```
let salary;
let name;
```

这种情况并不常见，因为更常见的是在需要变量时声明变量并赋值。现在大多数程序员喜欢在程序中最接近第一次使用时声明变量，而在过去，程序员在程序开始时声明程序需要的所有变量，然后在程序的后面给它们赋值。

# 提示，然后读取模板

在我们开始跟踪变量之前，让我向您介绍一下我将用于变量跟踪和顺序学习过程中的其他步骤的程序模板。这个模板叫做*提示符，然后读*。

当您希望您的程序是交互式的，以便程序从用户那里获得所需的数据时，可以使用此模板。你并不总是需要在你的程序中使用这个模板，因为有时候你会直接给变量赋值而不需要用户的参与。

这里是*提示符的伪代码描述，然后阅读*模板:

*提示用户输入一个值
将该值存储在一个变量中*

在演示这个模板之前，我必须向您介绍一个 JavaScript Spidermonkey 函数— `readline()`。`readline()`功能暂停程序的执行，并允许用户向程序中输入数据。然后，当用户点击回车键时，输入的数据被存储在一个变量中。

下面是一个演示该函数如何工作的示例程序:

```
let name = readline();
```

当程序运行时，当用户在键盘上打字时，执行暂停。当用户按下回车键时，输入的任何内容都会存储在变量中。

现在让我们看看如何在程序中使用这个模板。假设您想在程序中存储用户的名字和姓氏。您的程序需要告诉用户首先输入他们的名字，存储数据，然后输入他们的姓氏并存储数据。下面是实现这一点的伪代码:

*提示用户输入他们的名字
让用户输入他们的名字并将其存储在变量中
提示用户输入他们的姓氏
让用户输入他们的姓氏并将其存储在变量中*

现在我们准备写一个实现这个伪代码的程序。这是:

```
putstr("Enter your first name: ");
let first = readline();
putstr("Enter your last name: ");
let last = readline();
```

注意:`putstr()`函数将文本(参数)写入屏幕，而不添加换行符。`print()`函数将文本写入屏幕并添加一个换行符。

现在我们知道了如何将文本(字符串)数据输入到程序中，让我们看看如何将数字数据输入到程序中。我们必须采取额外的步骤。当您使用`readline()`功能从键盘上检索数据时，数据被作为字符串检索。这对于文本来说没问题，但是对于数字数据就不行了。原因如下。

下面是一个简短的程序，要求用户输入两个数字，以便将它们相加:

```
putstr("Enter the first number: ");
let number1 = readline();
putstr("Enter the second number: ");
let number2 = readline();
let sum = number1 + number2;
print(sum);
```

下面是我们运行这个程序时发生的情况:

输入第一个数字:2
输入第二个数字:3
23

用户输入数字，但是当它们被“加”在一起时，你得到的是“数字”23。这被称为串联，当`+`操作符用于字符串时，它将两个字符串连接在一起形成一个字符串。

为了解决这个问题，当我们从用户那里获取数字数据时，我们需要使用另一个函数。这个功能就是`parseInt()`功能。这个函数获取数据并将其转换成一个数字，特别是一个整数。

下面是上面添加了`parseInt()`功能的程序:

```
putstr("Enter the first number: ");
let number1 = parseInt(readline());
putstr("Enter the second number: ");
let number2 = parseInt(readline());
let sum = number1 + number2;
print(sum);
```

这是这个程序的一次运行:

输入第一个数字:2
输入第二个数字:3
5

现在当我们把 2 和 3 加在一起，我们得到的是 5 而不是 23。

如果你正在处理浮点数而不是整数，有一个`parseFloat()`函数。这里有一个例子:

```
putstr("Enter the first number: ");
let number1 = parseFloat(readline());
putstr("Enter the second number: ");
let number2 = parseFloat(readline());
let sum = number1 + number2;
print(sum);
```

这里有一个例子:

输入第一个数字:3.14159
输入第二个数字:. 02
3.16159

我们已经学完了本课的第一部分。在第 2 部分中，我们将学习更多关于*提示符的知识，然后使用有序、结构化的方法阅读*模板来学习编程。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更内容于* [***通俗地说就是***](http://plainenglish.io)