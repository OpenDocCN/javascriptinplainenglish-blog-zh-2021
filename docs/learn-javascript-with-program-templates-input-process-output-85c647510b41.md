# 使用程序模板学习 JavaScript:输入、处理、输出

> 原文：<https://javascript.plainenglish.io/learn-javascript-with-program-templates-input-process-output-85c647510b41?source=collection_archive---------16----------------------->

![](img/1df5766c111a9b8ccc32d14f08667781.png)

Photo by [Victor Barrios](https://unsplash.com/@thevictorbarrios?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你写的每个计算机程序做三件事:它接受输入；它对输入做一些事情，并向程序的用户传达输入是如何改变的。有时程序使用所谓的批量处理来执行这个过程，即接收所有输入，然后处理输入，最后输出结果。

这个过程被称为*输入、处理、输出*程序模板，简称 IPO，而 IPO 模板就是本文的主题。

# IPO 模板的伪代码

描述 IPO 模板的伪代码是:

*输入所有的值。
处理数值。
输出处理的结果。*

以这种方式编写的程序被称为进行*批量处理*，因为所有的输入都是一次批量接收然后处理的，而不是在接收其他输入之前接收并处理一些输入。当然，并不是你遇到的所有问题都可以用这种方法解决，但是很多都可以，所以我们需要一个模板来描述这个过程。

# 外壳脚本

在我开始介绍一些 IPO 例子之前，我想先介绍一下 shell 脚本的概念。我在以前的文章中编写的程序都是在 shell 中以交互的格式编写的。这对于尝试编程技术并立即获得结果非常有用，但是对于编写更长的程序来说不方便。这个问题的解决方案是 shell 脚本。

shell 脚本是存储在文件中的 JavaScript 程序语句的集合。然后 JavaScript 解释器逐行执行该文件，就像我们在 shell 中输入行一样。

您可以通过使用任何文本编辑器打开一个文本文件并使用包含“.”的文件名保存该文件来创建 shell 脚本。js”扩展名，以便解释器知道该文件包含 JavaScript 代码。

# 计算薪水

作为第一个例子，让我们编写一个程序来计算一个雇员的简单工资。我们将忽略加班工资、扣除额和税收等因素，而只是根据员工的工资率和工作时间来计算他们的工资总额。

输入是雇员的工资率和他们的工作时间。下面是将这些数据输入程序的代码:

```
putstr("Enter the pay rate: ")
let payRate = parseFloat(readline())
putstr("Enter the number of hours worked: ")
let hoursWorked = parseFloat(readline())
```

处理部分将工资率乘以工作时数:

```
let grossPay = payRate * hoursWorked
```

输出部分将计算结果显示到屏幕上:

```
print("Gross pay:", grossPay)
```

将这些线放在一起，我们得到:

```
// Inputputstr("Enter the pay rate: ")
let payRate = parseFloat(readline())
putstr("Enter the number of hours worked: ")
let hoursWorked = parseFloat(readline())

// Processing
let grossPay = payRate * hoursWorked

// Output
print("Gross pay:", grossPay)
```

接下来让我们看一个使用字符串的例子。该程序将请求用户的全名，然后创建变量以标准的“名，姓”格式和“姓，名”格式存储名称。程序如下:

```
// Input
putstr("Enter your first name: ")
let firstName = readline()
putstr("Enter your middle name: ")
let middleName = readline()
putstr("Enter your last name: ")
let lastName = readline()

// Processing
let firstLast = firstName + " " + middleName + " " + lastName
let lastFirst = lastName + ", " + firstName + " " + middleName

// Output
print(firstLast)
print(lastFirst)
```

下面是这个程序运行一次的输出:

输入你的名字:约翰
输入你的中间名:保罗
输入你的姓:琼斯
约翰·保罗·琼斯
琼斯，约翰·保罗

# 提取数字

作为最后一个例子，这里有一个从一个数字中提取数字的程序。对于这个例子，我将假设所讨论的数字是一个标识号，最后一位数字代表一个校验位。检查是前三个数字加在一起，应该等于最后一个(第四个)数字。

从数字中提取数字的方法是使用模数运算符。如果你不熟悉这个运算符(`%`)，它返回一个数除以另一个数的余数。如果你取一个以 10 为模的数，余数就是这个数的最后一位。例如:

*123 % 10 = 3*

一旦你得到了最后一个数字，你就可以把它从数字中去掉，方法是用 10 除这个数字。我说整数除法是因为你只想要一个整数作为结果，而不是一个浮点数。继续上面的例子:

*123 / 10 = 12* 如果做整数除法

有些语言，比如 C++，默认做整数除法。JavaScript 没有，所以我们需要通过调用`parseInt()`函数来解决这个问题，就像这样:

```
parseInt(123 / 10)
```

记住这一点，我们现在可以使用*输入、处理、输出*模板编写一个程序来从一个数字中提取数字。在以后的文章中，我将演示如何使用数字来检查标识号的有效性。

程序是这样的:

```
// Input
putstr("Enter an identification number: ");
let idNumber = parseInt(readline());// Process
let copy = idNumber; // copying because extracting destroys the original //number
let fourth = idNumber % 10;
idNumber = parseInt(idNumber / 10);
let third = idNumber % 10;
idNumber = parseInt(idNumber / 10);
let second = idNumber % 10;
idNumber = parseInt(idNumber / 10);
let first = idNumber % 10;// Output
print("The first digit is:", first);
print("The second digit is:", second);
print("The third digit is:", third);
print("The fourth digit is:", fourth);
```

下面是该程序的两次运行:

输入识别号码:2387

第一个数字是:2

第二个数字是:3

第三个数字是:8

第四位数字是:7

输入识别号码:9342

第一个数字是:9

第二个数字是:3

第三个数字是:4

第四位数字是:2

# 最后的想法

*输入、处理、输出*模板几乎出现在你编写的每一个程序中，尽管有时顺序并不完全是线性的。有时你的程序会接收一些输入，进行一些处理，也许还有一些输出，然后接收更多的输入，进行更多的处理，产生一些输出，等等。

尽管如此，模板是通用的，因为所有程序都将一些数据作为输入，以某种形式处理这些数据，并使用处理后的数据生成输出。

在我的下一篇文章中，我将介绍一个新的程序模板， *Input One，Process One* ，它将用于介绍 JavaScript 中的循环概念。我将在本文中介绍两个循环结构:`for`循环和`while`循环。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***