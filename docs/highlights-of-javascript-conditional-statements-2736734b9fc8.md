# JavaScript 亮点—条件语句

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-conditional-statements-2736734b9fc8?source=collection_archive---------17----------------------->

![](img/7e560392cb5ccbb7812ed653e22d287e.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# if 语句

If 语句让我们有条件地运行代码。

例如，我们可以写:

```
const answer = prompt("Where's the capital of Italy?");
if (answer === "Rome") {
  alert("Correct!");
}
```

添加接受问题答案的提示。

然后我们在第`if`条语句中检查它。如果`answer`是`'Rome'`，那么我们显示`'Correct!'`警报。

一个`if`语句，如果后面跟一个我们要检查的布尔表达式。

如果布尔表达式返回`true`，那么我们运行花括号之间的代码。

我们应该总是使用`===`来检查值的相等性，因为它检查类型和值。

简单的`if`语句可以不加括号，也可以全部写在一行中。

但是花括号更方便阅读，因为它更清晰。

# 比较运算符

`===`运算符是比较运算符。

这是等式运算符。

它用来比较两个事物，看它们是否相等。

我们可以使用等式运算符来比较任意两个表达式的返回值。

例如，我们可以写:

```
if (totalCost === 81.50 + 100) {
```

或者

```
if (fullName === firstName + " " + "wong") {
```

字符串比较区分大小写，因此只有当两种情况相同时，字符串才被视为相同。

如果我们想检查两个表达式是否相同，那么我们可以使用`!==`不等式比较运算符。

所以如果我们有:

```
"Rose" !== "rose"
```

然后返回`true`，因为他们有不同大小写的字母。

JavaScript 提供了更多的操作符。

它们包括用于大于号运算符的`>`。

`<`是小于运算符。

`>=`是大于或等于运算符。

`<=`是小于或等于运算符。

我们可以通过书写来使用它们:

```
if (2 > 0) {
if (0 < 2) {
if (2 >= 0) {
if (2 >= 1) {
if (0 <= 2) {
if (1 <= 2) {
```

# if…else 和 else if 语句

如果我们要检查不止一个案例，那么我们可以使用`else`关键字来添加更多案例。

例如，我们可以写:

```
const answer = prompt("Where's the capital of Italy?");
if (answer === "Rome") {
  alert("Correct!");
} else {
  alert("Wrong!");
}
```

`else`关键字在`answer`不是`'Rome'`时运行的块之前。

如果我们有更多的案例，那么我们可以添加`else if`语句。

例如，我们可以写:

```
const answer = prompt("Where's the capital of Italy?");
if (answer === "Rome") {
  alert("Correct!");
} else if (answer === "Vatican") {
  alert("Close!");
} else {
  alert("Wrong!");
}
```

我们跑的东西是`answer`是`'Vatican'`。

如果`answer`不是`'Rome'`或`'Vatican'`，那么我们运行最后一个程序块。

# 结论

JavaScript 有`if`和`else`关键字，让我们创建语句，让我们有条件地运行代码。