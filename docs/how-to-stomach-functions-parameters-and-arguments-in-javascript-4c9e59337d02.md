# 如何接受 JavaScript 中的函数、参数和自变量

> 原文：<https://javascript.plainenglish.io/how-to-stomach-functions-parameters-and-arguments-in-javascript-4c9e59337d02?source=collection_archive---------13----------------------->

## JavaScript 中函数、参数和自变量的初学者指南

![](img/158cab38916299404ad385afe16eb738.png)

作为一名新的程序员，我努力理解的第一个概念(我的第一个 WTF 时刻)是学习函数、参数和自变量。真正帮助我克服第一个困难的是使用了一个类比，当然是一个涉及食物的类比。

但是在进行类比之前，让我们先定义几个关键术语。

根据[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions),**函数**类似于一个过程——一组执行任务或计算值的语句，但是对于一个符合函数资格的过程，它应该接受一些输入并返回一个输出，在输入和输出之间有一些明显的关系换句话说，函数通常是一小段代码，它执行一系列语句并返回最终结果或值。为了让这个更容易理解，假设您想创建一个制作三明治的函数。它可能看起来像这样:

*注意这段代码是为了说明的目的，为了显示类比，需要一些创造性的自由。*

```
function makeSandwich() { console.log(“Slice bread”) console.log(“Spread condiment on bread”) console.log(“Layer meat and cheese on one slice of bread”) console.log(“Stack other slice of bread on top”)

  return "sandwich" //note this return value is for illustrative purposes
}
```

正如 MDN 定义中提到的，函数也可以接受输入。一般来说，这些输入称为**参数**。你可以把这些看作是占位符*或*变量*，在这里你可以插入特定的值。让我们回到我们的三明治示例，假设我们想要传入用于组装三明治的面包、调味品、肉和奶酪类型的特定值。它看起来会像这样:*

```
function makeSandwich(**bread**, **condiment**, **meat**, **cheese**) { console.log(“Slice **bread**”) console.log(“Spread **condiment** on **bread**”) console.log(“Layer **meat** and **cheese** on one slice of **bread**”) console.log(“Stack other slice of **bread** on top”) return "sandwich" //note this return value is for illustrative purposes}
```

在函数声明中，我们在括号中指定函数的参数(用逗号分隔):

```
(**bread**, **condiment**, **meat**, **cheese**)
```

这些占位符变量在函数体中被引用。因为在这个示例函数中，参数是在字符串中引用的，所以我们需要使用[模板文字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)。模板文字用反斜杠(` `)括起来，可以包含占位符，由美元符号和花括号(${placeholder})表示。

让我们重构我们的函数来使用模板文字:

```
function makeSandwich(**bread**, **condiment**, **meat**, **cheese**) {

  console.log(`Slice **${bread}**`)

  console.log(`Spread **${condiment}** on **${bread}**`) console.log(`Layer **${meat}** and **${cheese}** on one slice of **${bread}**`) console.log(`Stack other slice of **${bread}** on top`) return "sandwich" //note this return value is for illustrative purposes}
```

在其当前状态下，我们有一个功能，允许我们用不同成分的通用参数(或占位符)制作通用三明治。到目前为止，我们刚刚定义了我们的函数。因为没有调用这个函数，所以实际上没有做三明治。当我们调用该函数时，我们可以指定想要在三明治中使用哪些成分。

我可能刚刚看了皮克斯的《卢卡》，也可能没有，所以我很想吃一个意大利风味的三明治。让我们用 ciabatta 面包、香蒜沙司、意大利熏火腿和马苏里拉奶酪做个三明治吧……你饿了吗？当我们调用函数时，这些成分将作为**参数**传递。您可以将实参看作是我们插入到形参占位符中的实际值。让我们调用我们的三明治函数，*传递 ciabatta、香蒜酱、马苏里拉奶酪和意大利熏火腿的参数*。

```
makeSandwich("ciabatta", "pesto", "prosciutto", "mozzarella");
```

当函数被调用并运行时，在我们代码中引用面包的任何地方，我们将使用 ciabatta，调味品将使用 pesto，肉类将使用 prosciutto，奶酪将是 mozzarella。

这里有一个帮助你形象化的工具，但是注意这不是有效的 JavaScript:

```
function makeSandwich(**bread**, **condiment**, **meat**, **cheese**) {
  console.log(`Slice ${**bread ⇒ "ciabatta"}**`) console.log(`Spread ${**condiment ⇒ "pesto"**} on ${**bread ⇒ "ciabatta"}**`)

  console.log(`Layer ${**meat ⇒ "prosciutto"}** and ${**cheese ⇒ "mozzarella"**} on one slice of ${**bread ⇒ "ciabatta"}**`) console.log(`Stack other slice of ${**bread ⇒ "ciabatta"}** on top`) return "sandwich" //note this return value is for illustrative purposes}
```

控制台中的结果将如下所示:

```
Slice ciabattaSpread pesto on ciabattaLayer prosciutto and mozzarella on one slice of ciabattaStack other slice of ciabatta on topsandwich
```

如您所见，在引用我们的参数的任何地方，它们都被替换为特定的参数值。我们可以使用这个函数，通过传递一组不同的参数来制作我们想要的任何类型的三明治:

```
makeSandwich("sourdough", "mayo", "turkey", "Swiss");makeSandwich("wheat", "mustard", "ham", "cheddar");
```

虽然这个例子很吸引人，但让我们来看一个更现实的例子。让我们制作一个简单的函数，将两个数字相加:

```
function addNumbers(x, y){
  return x + y
}
```

在这个例子中，我们的函数(addNumbers)有两个参数，每个参数都是一个数字，并将这两个数字相加。现在让我们调用函数，*传递参数*4 和 5。

```
addNumbers(4, 5);⇒ 9
```

我希望这个类比有助于阐明函数、参数和参数！

*更多内容请看*[***plain English . io***](http://plainenglish.io)