# JavaScript 中的两种条件语句

> 原文：<https://javascript.plainenglish.io/the-2-types-of-conditional-statements-in-javascript-ffd14dc96b8b?source=collection_archive---------12----------------------->

## 它们是什么以及何时使用它们

条件语句告诉你的程序，如果某个条件为真，就执行某组命令。在 JavaScript 中，有`if...else`语句和`switch`语句。

![](img/500cde82cdcf71a21595ebdb40a21c13.png)

在非编程领域，条件语句一直都在使用。假设你的朋友让你去杂货店给他们买些冰淇淋。他们告诉你，“如果商店有薄荷巧克力片冰淇淋，请去买。如果商店没有，请买饼干和奶油。如果商店也没有，就给我买巧克力冰淇淋。”换句话说，你的朋友在说:

*   如果商店有薄荷巧克力片冰淇淋:买那个。
*   否则，如果它有饼干和奶油冰淇淋:买那个。
*   否则:买巧克力冰淇淋。

这些语句中的每一个都有一个条件(“商店有薄荷巧克力片冰淇淋”)和一个条件为真时要执行的语句(“购买那个”)。注意这些语句中的**顺序**也很重要。如果可以选择饼干和奶油，你的朋友不想让你买巧克力冰淇淋。

当使用条件语句时，记住您要检查的内容以及这些内容应该以什么顺序检查是很重要的。

## 1.If…else 语句

**if…else 语句**的结构如下:

```
if (condition) {
    statement_1;
} else {
    statement_2;
}
```

如果`condition`是`true`，那么`statement_1`就会执行。否则，如果条件是`false`，那么`statement_2`将执行。

需要注意的是,`else`子句是可选的。此外，您可以使用`else if`按顺序测试多个条件:

```
if (condition_1) {
    statement_1;
} else if (condition_2) {
    statement_2;
} else if (condition_3) {
    statement_3;
} else {
    statement_last;
}
```

当测试多个条件时，仅执行评估为`true`的第一个**条件。**

要执行多条语句，请将它们组合在一条块语句中，如下所示:

```
if (condition) {
    statement_1;
    statement_2;
} else {
    statement_3;
    statement_4;
}
```

例如，假设我们有一个跟踪一周中每天温度的数组。如果到了周末(比如，数组中有 7 个温度)，我们要报告已经过去了整整一周。否则，我们希望记录还没有到周末:

```
let arr = [55, 60, 58, 57, 54];
if (arr.length === 7) {
  console.log("It's been a whole week!");
} else {
  console.log("It's not the end of the week yet.");
}
```

让我们把这个例子再往前推一步，把在[JavaScript 中的 5 种循环](https://medium.com/javascript-in-plain-english/the-5-types-of-loop-in-javascript-8bdb8f8fc1e9)中讨论的一些循环结合起来。如果是周末，我们应该返回那周的平均气温，而不是只记录。

有多种方法可以找到一组数字的平均值。一种是使用一个`for`循环找到数组中每个值的总和，然后除以数组的长度(平均值是总和除以计数)。我们首先初始化一个变量，它等于数组中每个值的总和。因为我们只想找到一整周的平均温度，所以我们将在`if`条件后面的语句中这样做。

```
let arr = [55, 60, 58, 57, 54, 52, 60];
if (arr.length === 7) {
  //initialize sum at 0 because we need to add values to it
  let sum = 0;
  //...
} else {
  console.log("It's not the end of the week yet.");
}
```

然后，我们可以使用一个`for`循环遍历数组的每个值，并将其添加到`sum`。`for`循环将在`0`启动计数器，因为[数组在 JavaScript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#accessing_array_elements) 中是零索引的。它会一直进行到数组的长度，或者说`arr.length`。我们想要检查数组的每个元素，一次一个，所以我们每次都会增加`1`。在`for`循环中，我们希望将数组的当前值加到`sum`中。我们可以用`arr[i]`访问数组的值。

```
let arr = [55, 60, 58, 57, 54, 52, 60];
if (arr.length === 7) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum = sum + arr[i]; // this could also be written as sum += arr[i]
  }
  //...
} else {
  console.log("It's not the end of the week yet.");
}
```

一旦`for`循环执行完毕，`sum`将包含该周每个温度的总和。由于我们想要返回平均温度，我们可以将`sum`除以 7(一周中的天数)，并在控制台记录该值。

```
let arr = [55, 60, 58, 57, 54, 52, 60];
if (arr.length === 7) {
  let sum = 0;
  for (let i = 0; i < arr.length; i++) {
    sum = sum + arr[i]; // this could also be written as sum += arr[i]
  }
  console.log(
    "It's been a whole week! This week's average temperature was " +
      sum / 7 +
      "degrees."
  );
} else {
  console.log("It's not the end of the week yet.");
}
```

## 2.Switch 语句

JavaScript 支持的另一种条件语句是 **switch 语句**。一个`switch`语句评估一个表达式，并根据评估结果，尝试将其与一个指定的`case`匹配。如果一个`case`匹配，那么那个`case`的语句执行。一个`switch`语句如下所示:

```
switch (expression) {
    case label_1:
        statement_1;
        break;
    case label_2:
        statement_2;
        break;
    default:
        statement_default;
        break;
}
```

首先，`expression`被评估。然后，你的程序将寻找一个标签与`expression`的值相匹配的`case`，然后执行相关的语句。如果找不到匹配的标签，您的程序将寻找`default`子句(可选)，并执行相关的语句。如果没有`default`子句，你的程序将简单地退出`switch`语句。

`break`语句告诉你的程序一旦执行了`case`的语句就从`switch`中脱离出来。`break`语句是可选的。如果你不包含它们，你的程序将停留在`switch`语句中，并将执行`switch`语句中的下一条语句。

例如，让我们说你正试图决定穿什么夹克，这取决于天气。如果天气炎热、温暖或寒冷，不同的夹克是合适的:

```
switch (weather) {
  case "Hot":
    console.log("No jacket needed.");
    break;
  case "Warm":
    console.log("Bring a light jacket.");
    break;
  case "Cold":
    console.log("Bring your heavy jacket.");
    break;
  default:
    console.log("You probably should bring a jacket anyway, just in case!");
    break;
}
```

您可能想知道，`break`语句到底是做什么的？使用相同的示例，假设您没有包含任何`break`语句，并且`weather = "Hot"`:

```
let weather = "Hot";
switch (weather) {
  case "Hot":
    console.log("No jacket needed.");
  case "Warm":
    console.log("Bring a light jacket.");
  case "Cold":
    console.log("Bring your heavy jacket.");
  default:
    console.log("You probably should bring a jacket anyway, just in case!");
}
```

输出将是:
`No jacket needed. Bring a light jacket. Bring your heavy jacket. You probably should bring a jacket anyway, just in case!`

这是因为第一个`case`、`"Hot"`的标签与`weather`匹配，所以该语句执行。然后，每个后续的语句都会执行，因为没有`break`告诉你的程序停止。

## 三元运算符

**三元运算符**不是一种条件语句。相反，它是一个检查条件的操作符。这是一行代码，因为它非常简洁，所以经常被用作简单的`if...else`语句的缩短版本。

三元运算符的结构如下:

```
condition ? expressionIfTrue : expressionIfFalse
```

`condition`是一个被求值的表达式。如果`condition`是 [*真值*](https://developer.mozilla.org/en-US/docs/Glossary/truthy) (意思是它是`true`，或者它的值可以转换成`true`)，则执行`expressionIfTrue`。如果`condition`为[](https://developer.mozilla.org/en-US/docs/Glossary/falsy)*(意思是为`false`，或者其值可以转换为`false`，包括`null`、`NaN`、`0`、`""`、`undefined`)，则执行`expressionIfFalse`。*

*例如，假设最初的`if...else`语句检查一个数字是否为正:*

```
*const num = 4;
if (num >= 0) {
  console.log("Positive");
} else {
  console.log("Negative");
}*
```

*条件是`num >=0`，这意味着这就是我们要检查的。使用三元运算符，它将位于问号`?`的左侧。如果这是真的，我们将希望控制台日志`"Positive"`，所以这是`?`之后的第一个表达式。如果是 falsy，我们需要控制台日志`"Negative"`，所以这是第二个表达式，它在冒号`:`之后。*

*我们可以将三元运算符的结果存储到一个名为`positiveCheck`的变量中。然后，我们可以控制台记录该变量的值。*

```
*const num = 4;
const positiveCheck = num >= 0 ? "Positive" : "Negative";
console.log(positiveCheck);*
```

*有些人喜欢三元运算符，因为它们在处理简单的条件语句时节省空间，但并不是每个人都喜欢或使用它们。不管你是否使用三元运算符，重要的是知道它们是什么样子的，以及在遇到它们时如何阅读它们。*

## *结论*

*如果您对 JavaScript 中的条件语句有任何疑问或其他想法，请在评论中告诉我。*

***资源:***

*   *[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Guide/Control _ flow _ and _ error _ handling](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Control_flow_and_error_handling)*
*   *[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/if...否则](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/if...else)*
*   *[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Statements/switch](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/switch)*
*   *[https://developer . Mozilla . org/en-US/docs/Learn/JavaScript/Building _ blocks/conditionals](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/conditionals)*