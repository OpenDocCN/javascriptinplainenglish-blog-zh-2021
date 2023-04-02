# 使用程序模板学习 JavaScript:从备选方案中选择

> 原文：<https://javascript.plainenglish.io/learn-javascript-with-program-templates-select-from-alternatives-d4f9270f3fac?source=collection_archive---------18----------------------->

## 第 1 部分:学习如何使用“if”语句。

![](img/3610213b151379ecead12f2c550c6a0c.png)

Photo by [Radowan Nakif Rehan](https://unsplash.com/@radowanrehan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你编写的大部分计算机程序都需要根据输入程序的数据做出决策。对于这些情况，您可以使用一个程序模板— *从选项中选择*。有两种 JavaScript 编程结构可以用来实现这个模板——`if`语句和`switch`语句。在本文中，我将向您展示如何使用`if`语句，在下一篇文章中，我将讨论`switch`语句。

# 从备选项中选择模板

*从选项中选择*模板用于根据给定值从一组其他编程动作中选择一个编程动作。下面是一个伪代码示例，它基于将字母等级分配给数字测试分数:

*如果数字测试分数大于或等于 90，指定字母等级 a。
如果数字测试分数大于或等于 80，指定字母等级 b。
如果数字测试分数大于或等于 70，指定字母等级 c。
如果数字测试分数大于或等于 60，指定字母等级 d。
如果数字测试分数小于 60，指定字母等级 f。*

下面是另一个伪代码示例，这次是针对度假胜地活动建议系统:

*如果室外温度大于 80，去游泳。如果室外温度在 65 到 79 度之间，打网球。如果室外温度在 50 到 64 度之间，去远足。如果室外温度低于 50 度，就呆在室内，坐在火边。*

# 条件表达式

从一组选项中进行选择的主要方法是使用 if 语句。该语句测试条件表达式，并根据条件表达式的结果执行不同的代码集。

条件表达式是使用关系运算符对数据值进行比较。关系运算符有:

*   >大于
*   ≥大于或等于
*   < Less than
*   ≤ Less than or equal to
*   == Equal to
*   != Not Equal to

Here are some examples showing how these operators work:

```
js> let x = 23
js> x < 250
true
js> x == 24
false
js> x <= 21
false
js> x != 24
true
```

As you can see, these conditional expressions return a true or false value, also known as Boolean values. This Boolean value is what the 【 statement uses to decide which set of programming statements to execute.

# Using the if Statement

Now let’s look at how we can implement the *使用`if`语句从备选*模板中选择。`if`语句的一般形式是:

*if(条件表达式){
语句执行
}
else {
语句执行
}*

下面是一个示例程序:

```
putstr("Enter a number: ")
let number = parseInt(readline())
if (number % 2 == 0) {
  print(number,"is even.")
}
else {
  print(number,"is odd.")
}
```

条件表达式测试数字是否为偶数。如果是，则执行条件表达式正下方的代码。如果数字不是偶数，则执行 else 子句下的代码。

以下是该程序的一些示例输出:

输入一个数字:24

24 是偶数。

C:\js>js test.js

输入一个数字:23

23 是奇数。

有些问题更难，或者至少涉及更多的决策。假设您必须将字母等级分配给数字分数。数字分数和字母分数的典型范围如下:

90–100 安
80–89 安
70–79 安
60–69 安
0–59 安

数字分数可以有五种可能的等级之一。你不能用简单的 *if-else* 语句来解决这个问题。你需要一个更复杂的 if 语句——if-else if 语句。下面是分配字母等级的工作方式:

```
putstr("Enter a numeric score: ");
let score = parseInt(readline());
let letterGrade = "";
if (score >= 90) {
  letterGrade = "A";
}
else if (score >= 80) {
  letterGrade = "B";
}
else if (score >= 70) {
  letterGrade = "C";
}
else if (score >= 60) {
  letterGrade = "D";
}
else if (score < 60) {
  letterGrade = "F";
}
print("A grade of",score,"is the letter grade",letterGrade)
```

以下是该程序的一些运行情况:

输入数字分数:75
A 级 75 是字母等级 C
输入数字分数:81
A 级 81 是字母等级 B
输入数字分数:57
A 级 57 是字母等级 F
输入数字分数:94
A 级 94 是字母等级 A

# 逻辑运算符

有时候一个决定是基于更复杂的逻辑。例如，你是一家贷款银行，一个人要获得贷款，他需要有一份收入超过 30000 美元的工作，而且必须在这份工作上至少干了两年。这个决定需要使用逻辑*和*:工资必须至少为 30000 美元**和**雇佣期限必须至少为 2 年。

JavaScript 有一个逻辑 AND 运算符— `&&`。为了理解逻辑 and 的工作原理，下面是一个真值表，显示了运算符如何计算条件表达式:

*真与真产生真
真与假产生假
假与真产生假
假与假产生假*

要使用和编写的逻辑表达式为真，两个条件表达式都必须为真。

考虑到这一点，我们来写一个小程序，根据上面给出的条件，判断一个人是否可以获得贷款。程序如下:

```
putstr("Enter your salary: ")
let salary = parseFloat(readline())
putstr("How long (years) have you been employed at this position? ")
let howLong = parseFloat(readline())
if (salary > 30000 && howLong > 2) {
  print("You are qualified for the loan.")
}
else {
  print("Sorry, you are not qualified for the loan.")
}
```

这个程序运行了三次:

输入你的薪水:31000
你在这个职位上工作多久了？2
对不起，你不符合贷款条件。

输入你的薪水:31000
你在这个职位上工作多久了？2.1
你符合贷款条件。

输入你的薪水:29000
你在这个职位上工作了多久(年)？3
对不起，你不符合贷款条件。

第二个逻辑运算符是 or 运算符— `||`。一个使用 OR 的例子:如果你的年薪达到或超过 20000 美元，你可以得到一笔贷款**或者**你可以找一个有同样年薪的人来共同签署这笔贷款。

or 的真值表是这样的:

*真或真产生真
真或假产生真
假或真产生真
假或假产生假*

如您所见，要使 or 条件为真，其中一个或两个条件表达式必须为真。下面是上面例子的 JavaScript 代码:

```
putstr("Enter your salary: ")
let salary = parseFloat(readline())|
putstr("Do you have a co-signor? ")
let cosign = readline()
if (salary > 20000 || cosign == "yes") {
  print("You can receive a loan.")
}
else {
  print("Sorry, you cannot receive a loan.")
}
```

这个程序运行了三次:

输入你的薪水:21000
你有联署人吗？不
你可以获得贷款。

输入你的工资:19000
你有共同签署人吗？是的
你可以获得贷款。

输入你的薪水:18000
你有联署人吗？不
对不起，您不能获得贷款。

如果你仔细研究这个例子的逻辑，你会发现贷款与否的决定取决于申请人的工资。

编写这个程序的另一种方法是使用嵌套的`if`语句，我将在下一篇文章中介绍这些，以及一种不同的 JavaScript 选择方法——`switch`语句。

感谢您的阅读，请回复这篇文章或发邮件给我，告诉我您的意见和建议。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*