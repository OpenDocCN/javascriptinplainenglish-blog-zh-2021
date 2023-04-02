# 学习 JavaScript:循序渐进的方法

> 原文：<https://javascript.plainenglish.io/learning-javascript-a-sequenced-approach-variables-and-data-types-part-2-b97eaae8479e?source=collection_archive---------20----------------------->

## 变量和数据类型—第 2 部分

![](img/5900a2c96fb8e84dda73b7408af98170.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在第 1 部分中，我介绍了 JavaScript 变量和数据类型。在第 2 部分中，我将带您经历学习变量的结构化的、有序的步骤。在本文中，我将用四个步骤演示变量交换程序模板:1)跟踪变量交换示例的代码；2)翻译变量交换的伪代码；3)识别描述变量交换的模板；4)将一个独特的变量交换问题转化为一个有效的 JavaScript 程序。

# 跟踪变量交换示例

学习编程的第一步是能够成功地阅读和理解程序正在做什么。证明这一点的最佳方式是通过变量跟踪。变量踪迹表示在程序的生命周期中存储在程序中所有变量中的值。成功的变量跟踪将在程序的最后一行显示每个变量的最终值。

下面是一个执行变量交换的程序示例:

```
let number1 = 23;
let number2 = 167;
let temp = number1;
number1 = number2;
number2 = temp;
```

下面是这个程序的跟踪结果:

数字 1:23167

数字 2: 167，23

温度:23

该轨迹显示程序以值为 167 的数字 1、值为 23 的数字 2 和值为 23 的 temp 结束。

当学习者能够成功地完成一个变量跟踪时，他们就准备进入下一步:从一个伪代码示例编写代码。

# 用伪代码编写变量交换程序

学习编程的第二步是能够获取伪代码示例中提供的指令，并根据伪代码实现工作程序。下面是一个变量交换程序的伪代码示例:

*从用户处获取一个数字并将其存储在第一个变量中
从用户处获取一个较小的数字并将其存储在第二个变量中
按顺序显示第一个和第二个变量的值
将第一个数字的值存储在临时变量中
将第二个变量的值存储在第一个变量中
将临时变量的值存储在第二个变量中
按顺序显示第一个和第二个变量的值*

然后，学习者利用这些伪代码，通过将每一行伪代码翻译成 JavaScript 代码，生成一个程序。下面是根据这一描述编写的一个程序:

```
putstr("Enter the first number: ")
let first = parseInt(readline());
putstr("Enter a smaller number: ");
let second = parseInt(readline());
print(first, second);
let temp = first;
first = second;
second = temp;
print(first, second);
```

下面是这个程序的一次运行:

输入第一个数字:47

输入一个较小的数字:32

47 32

32 47

显然，这个程序作为第一个变量工作，第二个变量的值被交换了。

# 阅读(并理解)变量交换模板

结构化顺序学习过程的第三步是能够阅读和理解程序模板。做到这一点的最好方法是使用程序模板向学习者提供大量成功和不成功程序的例子。

这是另一个成功的变量互换程序的例子:

```
putstr("Enter a string that starts with the letter b: ");
let string1 = readline();
putstr("Enter a string that starts with the letter a: ");
let string2 = readline();
print(string1, string2);
let tempStr = string1;
string1 = string2;
string2 = tempStr;
print(string1, string2);
```

这是一个变量交换程序，它有一个错误:

```
putstr("Enter the first number: ");
let first = parseInt(readline());
putstr("Enter a smaller number: ");
let second = parseInt(readline());
print(first, second);
let temp = second;
first = second;
second = temp;
print(first, second);
```

变量跟踪将显示错误。假设用户输入 32 和 23:

第一:32，23

第二:23，23

温度:23

变量 second 以 23 结束，变量 first 也是如此。需要再次向学习者展示该模板，然后向其展示一个新问题以尝试解决。

# 编写程序解决变量交换问题

顺序过程中的第四步也是最后一步是给学习者一个原始问题，该问题涉及所讨论的程序模板，并且学习者能够编写一个程序来解决该问题。

下面是一个涉及执行变量交换的问题示例:

Meredith 有两个手电筒，它们的端口可以报告电池剩余电量的百分比。第一个手电筒有更强的光束，梅雷迪思需要在夜间徒步旅行，还有 21%的电量，而第二个手电筒，光束较窄，还有 87%的电量。使用变量 flash1 作为第一个手电筒的电池，flash2 作为第二个手电筒的电池，编写一个程序来切换电池，以便手电筒 1 有更强的电池。

有了这个描述，学习者应该能够编写一个程序来解决手电筒电池切换的问题。这里有一个程序可以做到这一点:

```
let flash1 = 21;
let flash2 = 87;
print("flashlight1: ",flash1, "flashlight2: ", flash2);
let temp = flash1;
flash1 = flash2;
flash2 = temp;
print("flashlight1: ",flash1, "flashlight2: ", flash2);
```

以下是运行该程序的输出:

闪光灯 1: 21 闪光灯 2: 87

闪光灯 1: 87 闪光灯 2: 21

这个输出显示第一个手电筒现在有最大功率的电池，这意味着程序成功地进行了交换。

# 最后的想法

这就结束了我们学习 JavaScript 中变量和数据的结构化顺序方法之旅。我的下一篇文章将讨论 JavaScript 数学运算符的学习，后续文章将演示如何使用我在这里演示的编程学习的四个阶段，并给出一个将数字分解为单个数字的例子。我还将介绍一个新的程序模板:*输入，处理，输出*。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)