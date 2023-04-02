# 如何在 JavaScript 中将任意函数转换成箭头函数

> 原文：<https://javascript.plainenglish.io/how-to-convert-any-function-to-an-arrow-function-in-javascript-afb0c87e411d?source=collection_archive---------3----------------------->

同样的结果，更少的代码。了解将任何类型的传统 JavaScript 函数转换为箭头函数的过程，使您的代码更加紧凑和强大。

![](img/6c2df580423b1ef00b5422928f135c09.png)

说到 JavaScript，众所周知，它是一种重功能的语言。它充满了不同的使用、重用、传递函数等方式。

所有这些都是有充分理由的。函数提供了一种高度模块化的方式来构建应用程序逻辑。如果你改变你的函数，你只是改变了给定数据的转换。

这种数据隔离不仅使编写应用程序变得容易，还使您的代码更加可测试和健壮。因为无论何时何地运行代码，只要提供相同的输入，就会得到相同的输出，不管运行环境或其他变量如何。

如果你想获得更多这样的教程，你可以通过下面的链接成为中级会员。如果你选择通过链接成为会员，一部分会员费也将支持像这样的教程，对你没有额外的费用。

[](https://dogaozgon.medium.com/membership) [## 通过我的推荐链接加入媒体

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

dogaozgon.medium.com](https://dogaozgon.medium.com/membership) 

最受欢迎的前端库之一 React.js 也在 React 16.8 中引入了一种称为“挂钩”的东西，允许前端开发人员在开发用户界面时只使用函数式编程。这一变化无论如何都不算小，因为它改变了创建用户界面的方式，并使整个文件结构更加模块化和可重用。

用 React.js 开发 web 应用的前端时，有很多时候你会发现自己需要一个函数，但是你只需要一次。有时这些函数太短了，以至于用名字定义和使用它们就像编写笨拙的代码。情况可能就是这样，尤其是如果你已经知道你可以使你的代码更加简洁易读。

但是，如何使您的函数更加紧凑，同时在下次查看代码时保持它们同样易于理解呢？

## 箭头功能来拯救

当在 React.js 中使用其他函数时，箭头函数的威力确实大放异彩，这在 react . js 中是很常见的事情。

这种模块化的代码编写方式也使得修改变得容易，出现错误的可能性更小。让我们先看一个关于箭头函数的示例代码，然后一行一行地解释我们如何一步一步地实现它。

```
const someNumbers = [1, 2, 3, 4];
```

假设我们有一个简单的数组，并且我们想要 console.log 另一个数组，它具有数组中每一项的值的两倍。对于 JavaScript 中的传统函数，我们可以通过下面的代码来实现:

```
//Using traditional functionsfunction double(num1){return num1 * 2;}console.log(someNumbers.map(double));
```

但是，如果我们使用箭头函数，我们可以用下面的代码获得相同的结果:

```
// Using an arrow functionconsole.log(someNumbers.map(num1 => num1 * 2));
```

具有传统功能:

1)我们首先要写关键字“function”告诉 javascript 我们要定义一个函数。

2)然后我们给函数起一个名字，以便以后能够重用它。

3)然后我们打开和关闭函数参数的括号。

4)然后我们打开和关闭函数体周围的花括号。

5)然后我们编写“return”关键字来表示我们想从函数体返回什么。

6)现在，我们终于可以将函数名传递给 console.log，这样我们就可以执行我们想要执行的功能。在这种情况下，这是给定数组中的每个数字加倍，并且控制台记录输出。

带箭头功能；然而，这个过程要简单得多。我们可以直接将它写在控制台日志中，它们将简单地执行它们的功能。

关于箭头函数，你应该知道的第一件事是，我们应该看到箭头符号，它由一个等号组成，紧挨着一个大号。比如这个:“= >”注意这些字符之间不能有空格。在这个箭头符号的左边，我们将有函数参数，在它的右边，我们将定义函数体。

当我们将传统的 javascript 函数转换成箭头函数时，我们可以使用以下步骤:

1.  我们可以从传统的函数开始，我们可以删除函数关键字和函数名。然后我们可以在参数和函数体之间添加箭头符号。
2.  在箭头的左边:如果有一个参数，那么我们可以去掉它周围的括号。如果我们有多个参数或者根本没有参数，那么我们应该保留括号。
3.  对于箭头的右边:如果函数只返回一个表达式，那么可以去掉“return”关键字以及函数体周围的花括号。在这种情况下，表达式的结果将自动返回。
4.  如果返回的表达式太大，不能放在一行中，可以用括号括起来。这在 React.js 开发中尤其常用。

按照上面的步骤，你可以将你的传统函数完全转换成一个箭头函数。请注意，将传统函数转换为工作箭头函数只需要第一步。

然而，应用这些步骤中的 3 个甚至全部 4 个步骤来得到最简洁、可读性高的代码是很常见的。

让我们将这些步骤应用于一些传统函数，以成功地将它们转换为箭头函数。从我们上面转换的函数开始。

此外，您可能也注意到了，我们使用了`map()`方法来应用转换，因为我们将函数传递给 map 方法来应用转换。ES6 引入了 map 方法以及其他一些非常有用的方法。如果你不熟悉地图，我强烈推荐你学习一下。

简而言之，我们将`map()`方法应用于一个可迭代的对象，比如一个数组，并传递给它一个函数。Map 获取我们给它的数组中的单个元素(在本例中是`someNumbers`)并应用函数转换，然后在一个数组中返回结果。所以它接受一个数组，应用函数，并返回结果数组。在这种情况下，它接受`someNumbers`数组，将每个数组元素乘以 2，并返回双精度数的结果数组。说完这些，让我们继续我们的例子:

```
//traditional functionfunction double(num1){
  return num1 * 2;
}// apply step 1:
(num1) => {
  return num1 * 2;
}// apply step 2:
num1 => {
  return num1 * 2;
}// apply step 3:
num1 => num1 * 2;// since we have a short function body, no need to apply step #4
// but we still can, and it will still work
num1 => (num1 * 2);
```

让我们来看几个例子，这样我们也可以涵盖将传统函数转换成箭头函数的其他场景。

具有多个参数的示例:

```
// traditional function
function multiplyTwo(num1, num2) {
 return num1 * num2;
}// first step applied
(num1, num2) => {
 return num1 * num2;
}// second step applied 
//(no change here, because we have multiple arguments)(num1, num2) => {
 return num1 * num2;
}// third step applied(num1, num2) => num1 * num2; // since we have a short function body, no need to apply step no 4
// but we still can, and it will still work
(num1, num2) => (num1 * num2);
```

没有参数的示例:

```
function sayHelloWorld(){
return "Hello, " + "World!";
}// apply step 1:
() => {
return "Hello, " + "World!";
}//apply step 2:
// no change here, because there is no arguments 
// and we keep the parantheses as is () => {
return "Hello, " + "World!";
}// apply step 3:
() => "Hello, " + "World!";// apply step 4:
// since we have a short function body, no need to apply step no 4
// but we still can, and it will still work
() => ("Hello, " + "World!");
```

没有参数和长返回表达式的示例:

```
//traditional functionfunction appendLoremIpsumText(){
return ("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua." + "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
}//apply step 1:
()=> {
 return ("Lorem ipsum dolor sit amet, consectetur adipiscing elit,       sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."     + "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do      eiusmod tempor incididunt ut labore et dolore magna aliqua.");
}//apply step 2:
// no change here, since we had no arguments
()=> {
return ("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua." + "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
}//apply step 3:
()=> (
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua." + "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
);//apply step 4:
() => ("Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua." + "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.");
```

具有较长函数体和 return 语句的函数示例:

```
//traditional functionfunction sayHi(name){
 const message = "Hi " + name;
 return message;
}//apply step 1:
(name) => {
 const message = "Hi " + name;
 return message;
}//apply step 2:
name => {
 const message = "Hi " + name;
 return message;
}//apply step 3:
name => {
 const message = "Hi " + name;
 return message;
}//apply step 4, (since the returned expression can fit easily into //one line no need to change anything here):name => {
 const message = "Hi " + name;
 return message;
}
```

当应用上面的步骤时，不要忘记你不需要应用所有的四个步骤。一旦你应用了第一步，你就在技术上把一个传统函数转换成了一个箭头函数。在这一点上，我建议你自己尝试一些功能，如果你卡住了，你可以随时来这里检查你的步骤和方法。不要害怕犯错误，因为在很多情况下这是你学习的方式。

## 结论

在本文中，您已经看到了如何将任何传统的 JavaScript 函数转换为 arrow 函数的分步指南以及工作代码示例。我希望你能从这篇文章中获得一些价值，并以某种方式帮助你。如果你想要更多这样的教程，你可以在 Medium 上关注我。

如果你对本教程有任何问题，请随时联系我们，或者在这里留言，我会尽快给你答复。带着这样的希望，你从这篇文章中获得了一些价值，我们将在下一篇文章中再见。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区***](https://discord.gg/GtDtUAvyhW) *获得独家获得写作机会和建议。*