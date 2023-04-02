# 使用程序模板学习 JavaScript:提示，然后阅读

> 原文：<https://javascript.plainenglish.io/learn-javascript-with-program-templates-prompt-then-read-41530a90af4?source=collection_archive---------11----------------------->

![](img/67dc612143fdca20738e39f7fd349e00.png)

Photo by [Danial Igdery](https://unsplash.com/@ricaros?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

将数据放入 JavaScript 程序有两种方法。一种方法是执行直接赋值。另一种方法是从使用该程序的人那里交互地获取数据。我们将主要看第二种输入数据到程序中的方法，虽然我也会讨论如何做作业。

要以交互方式将数据输入程序，我们必须实现提示符，然后读取程序模板。我将在本文中介绍这个模板的工作原理和使用方法。

# 三种常见的 JavaScript 数据类型

编写程序是为了操纵数据。为了编写高效的 JavaScript 程序，我们必须理解这种语言是如何对数据进行分类的。下面是三种数据类型类别。还有更多，但这是我们开始学习 JavaScript 需要的三个。

我们从数字开始。数字数据类型的名称是`Number`。JavaScript 识别两种类型的数字:称为*整数*的整数和称为*浮点数*的浮点数。大多数情况下，这些类别由 JavaScript 内部使用，但偶尔程序员需要知道一段数字数据的类型，比如用户何时输入。我将在本文后面更详细地介绍这一点。

JavaScript 中第二常见的数据类型是文本数据，名为`String`。字符串是由双引号或单引号括起来的任何一组字符。数字也可以是字符串，当它们被归类为字符串时，它们不能用于执行算术运算。

JavaScript 中的下一个数据类型是`Boolean`。此类型用于表示真/假值。布尔数据用于程序中的比较和决策。您不会像使用字符串和数字那样在程序中使用布尔数据，但是理解布尔数据类型仍然很重要。

# 将数据存储在变量中

在我演示如何使用提示符之前，我需要先谈谈 JavaScript 变量。变量是存储数据的内存位置的名称。在内部，内存地址是十六进制值，人类很难处理。给一个内存地址分配一个类似英语的名字要容易得多。

JavaScript 变量应该以字母字符开头，可以包含其他字母字符、数字、符号和下划线字符。

我将在下一节演示如何给变量赋值。

使用*赋值语句*将数据存储在变量中。赋值语句使用关键字 let 以及变量和赋值操作符(`=`)。赋值语句的一般形式是:

*设变量名=数据*

该语句从右向左解释。例如，给定以下赋值语句:

```
let salary = 20000
```

语句如下:“将 20000 分配给可变薪金。”

文本数据也是如此:

```
let name = "Paul McCartney"
```

赋值语句右侧的数据可以是上面示例中的文字数据，也可以是更复杂的表达式，例如:

```
let raise = salary * 1.1
let first_name = "John"
let last_name = "Lennon"
let full_name = first_name + " " + last_name
```

顺便说一句，除了 let 之外，还可以使用其他关键字将数据赋给变量，但是我将推迟到适当的时候再讨论它们。

# 提示，然后读取程序模板

现在，您已经看到了最有可能输入到程序中的数据类型，并且现在要将数据分配给变量，让我们来学习您将用于执行此任务的程序模板。模板名为*提示符，然后读*。

该模板的目的是向用户请求一个值，并将该值从键盘读入程序。发送给用户请求数据的消息被称为*提示*。

该模板的伪代码是:

*打印一条询问数值的消息。
读取数值。*

我们需要一些内置的 JavaScript 函数、关键字和操作符来成功实现这个模板。我们将在每种情况下使用的两个函数是`putstr()`、`print()`和`readline()`。我们需要的关键词是`let`。我们用来读取输入的操作符是赋值操作符。

`putstr()`功能在屏幕上显示一行文本。这里有一个例子:

```
putstr("Enter your name: ")
```

该消息也称为提示，以字符串形式输入，后跟一个冒号，这样用户就知道他们的输入将遵循提示。

`print()`功能将数据显示到屏幕上，然后输入新的一行，这样下一次输出将从当前输出的下一行开始。

`readline()`功能暂停程序的执行，允许用户从键盘输入数据。当用户按下 Enter 键时，数据被读取，此时，在键盘上键入的任何内容都被发送到接收输入的变量。这里有一个例子:

```
let name = readline()
```

我们现在可以将这些放在一起以完全实现*提示，然后读取*模板。以下是一些例子:

```
putstr("What is your name? ")
let name = readline()
putstr("Enter a sentence: ")
let sentence = readline()
putstr("Type a word: ")
let word = readline()
```

现在我将使用`print()`函数将输入回显给用户:

```
js> putstr("What is your name? ")
What is your name? js> let name = readline()
Ringo Starr
js> putstr("Enter a sentence: ")
Enter a sentence: js> let sentence = readline()
Now is the time for all good people to come to the aid of their party.
js> putstr("Type a word: ")
Type a word: js> let word = readline()
Hello
js> print("Hello, ", name)
Hello,  Ringo Starr
js> print("The sentence entered is: ", sentence)
The sentence entered is:  Now is the time for all good people to come to the aid of their party.
js> print("Say hello:",word)
Say hello: Hello
js>
```

# 使用带有数字输入的模板

使用*提示符输入字符串，然后读取*模板很简单，但是输入数字数据需要一些额外的工作。这是因为`readline()`函数自动将用户输入的数据作为字符串返回。对于文本数据，这很好。但是看看当我们使用`readline()`输入数字时会发生什么:

```
js> putstr("Enter your salary: ")
Enter your salary: js> let salary = readline()
20000
js> print("Here is your salary with a $500 bonus:",salary + 500)
Here is your salary with a $500 bonus: 20000500
js
```

发生了什么事？由于`readline()`返回一个字符串给变量，薪水被存储为“20000”。然后，我试着给它加上$500，但是当加法运算符应用于一个字符串时，它执行的是连接而不是加法。串联是将字符串粘在一起的过程，因此解释器将“20000”和 500 粘在一起得到“20000500”。

这个问题的解决方案是将从`readline()`接收的数据转换成数字形式。有两个内置的 JavaScript 函数可以做到这一点:`parseInt()`和 `parseFloat()`。他们是这样工作的。

这两个功能与`readline()`功能一起使用。两者都接受来自 `readline()` 的输入，并将该字符串输入转换成整数或浮点数。

这里有两个例子:

```
putstr("Enter your salary: ")
let salary = parseInt(readline())
putstr("Enter the value for pi: ")
let pi = parseFloat(readline())
```

变量`salary`和`pi`现在是适当的数字，可以用在数学表达式中。例如:

```
js> putstr("Enter your salary: ")
Enter your salary: js> let salary = parseInt(readline())
20000
js> putstr("Enter the value for pi: ")
Enter the value for pi: js> let pi = parseFloat(readline())
3.14159
js> print("10% salary raise",salary * 1.1)
10% salary raise 22000
js> print("area of circle with radius of 5:", pi * (5 * 5))
area of circle with radius of 5: 78.53975
js>
```

# 最后的想法

所有的计算机程序都与数据打交道。有时你可以直接在程序中分配数据，但有时你希望程序的用户输入数据。在这种情况下，您需要实现*提示，然后读取*模板，这样用户就可以准确地知道要输入什么数据，程序才能正常工作。

在我的下一篇文章中，我将介绍一个新的程序模板，它将在你将要编写的每一个计算机程序中使用，即*输入、处理、输出*模板。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容请看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的**[***免费每周简讯在这里***](http://newsletter.plainenglish.io/) ***。****