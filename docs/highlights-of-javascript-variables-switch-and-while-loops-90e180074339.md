# JavaScript 亮点——变量、开关和 While 循环

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-variables-switch-and-while-loops-90e180074339?source=collection_archive---------15----------------------->

![](img/1a0faadbc1b740cd088d952353a782d4.png)

Photo by [Hanson Lu](https://unsplash.com/@hansonluu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 局部变量与全局变量

JavaScript 有局部和全局变量。

局部变量只能在块中访问。

和全局变量在整个应用程序中都可用。

使用 JavaScript，我们用关键字`let`和`const`创建局部变量。

它们都是块级的，所以它们都只能在像函数和`if`块这样的块中使用。

`let`创建一个变量，`const`创建常量。

常量在赋值后不能被重新赋值。

但是内容可能还是会变。

常量在创建时必须有一个初始值。

例如，如果我们有:

```
function addNumbers() {
  let theSum = 2 + 2;
}
```

`theSum`仅在`addNumbers`功能中可用。

但是如果我们有:

```
function addNumbers() {
  theSum = 2 + 2;
}
```

那么`theSum`就是一个全局变量。

我们可以在任何地方访问该值。

如果一个变量是全局的，那么它是`window`全局对象的附加属性。

我们应该避免全局变量，因为用相同的名字创建全局变量很容易。

因此，很容易产生矛盾。

而且很难追踪变量是如何变化的。

# Switch 语句

`switch`语句让我们在一条语句中为不同的情况做不同的事情。

例如，我们可以写:

```
switch (dayOfWk) {
  case "Sat":
    alert("very happy");
    break;
  case "Sun":
    alert("happy");
    break;
  case "Fri":
    alert("happy friday");
    break;
  default:
    alert("sad");
}
```

我们检查`dayOfWk`的值，让我们在它有给定值时做不同的事情。

如果`dayOfWk`是`'Sat'`，那么我们显示一个`'very happy'`警告。

如果`dayOfWk`是`'Sun'`，那么我们显示一个`'happy'`警告。

如果`dayOfWk`是`'Fri'`，那么我们显示一个`'happy friday'`警告。

当`dayOfWk`有任何其他值时，运行`default`子句，我们显示`'sad'`警告。

`break`关键字是必需的，这样在发现一个案例后，`switch`语句的其余部分就不会运行。

上面的`switch`语句与以下语句相同:

```
if (dayOfWk === "Sat") {
  alert("very happy");
} else if (dayOfWk === "Sun") {
  alert("happy");
} else if (dayOfWk === "Fri") {
  alert("hapopy friday");
} else {
  alert("sad");
}
```

`switch`语句中的`default`与`if`语句中的`else`相同。

# While 循环

JavaScript `while`循环是我们可以使用的另一种循环。

它让我们在给定条件为`true`时运行一个循环。

例如，我们可以写:

```
let i = 0;
while (i <= 3) {
  console.log(i);
  i++;
}
```

在上面的循环中，当`i`小于或等于 3 时，我们运行该循环。

在循环体内，我们更新了`i`,这样我们就可以结束循环。

我们将循环块缩进两个空格，以便于输入和阅读。

# 结论

JavaScript 有一个`while`循环让我们重复运行代码。

同样，我们应该使用局部变量，避免使用全局变量。

`switch`语句让我们在给定某个变量值的情况下运行代码。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**