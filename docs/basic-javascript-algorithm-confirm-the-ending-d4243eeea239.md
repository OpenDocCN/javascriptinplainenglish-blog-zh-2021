# 基本 JavaScript 算法:确认结尾

> 原文：<https://javascript.plainenglish.io/basic-javascript-algorithm-confirm-the-ending-d4243eeea239?source=collection_archive---------6----------------------->

## 让我们使用 JavaScript 来解决一个基本算法，这将允许我们练习解决问题的技能。

![](img/9cb549a3c2db8bc60c86fa575479b5d6.png)

Photo by [JASUR JIYANBAEV](https://unsplash.com/@djianbaev?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

一般来说，算法是非常有用和重要的，因为它们帮助你作为一个开发者提高解决问题的技能。它们需要遵循一系列的步骤来解决问题或实现特定的结果。为了使求解算法更容易，你需要将它们分解成小部分。那么单独解决每个部分会比解决整个问题容易很多。

在本文中，我们将尝试解决一个简单的算法，该算法在 JavaScript 中确认字符串的结尾。让我们开始吧。

# 说明

我们有一个名为`confirmEnding`的函数，它将`str`和`target`作为它的两个参数。

这里有一个例子:

```
function confirmEnding(**str**, **target**) {// Your code here.}confirmEnding("Mehdi", "di"); //Should return **true**.
confirmEnding("Gracias", "ias"); //Should return **true**.
confirmEnding("Good game", "game"); //Should return **true**.
confirmEnding("Mehdi", "on"); //Should return **false**.
confirmEnding("Gracias", "cas"); //Should return **false**.
```

正如您在上面看到的，确认结束算法检查一个字符串(`str`)是否以给定的目标字符串(`target`)结束。如果字符串`str`的最后一个字符等于目标字符串`target`，函数应该返回`true`。如果没有，应该会返回`false`。

我们可以使用 ES6 方法`endsWith()`来解决这个算法，这样会更容易。但是为了多练习 JavaScript，我们不会用这种方法。

# 求解算法

我解决这个算法的方法是检查目标字符串`target`的长度。例如，如果目标字符串的长度是 2，我们将使用方法`slice`复制字符串`str`的最后 2 个字符。然后，我们将检查最后两个字符是否等于目标字符串。如果是，我们将返回`true`。如果没有，我们就返回`false`。

首先，我们将使用 slice 方法复制字符串`str`的最后几个字符。要复制的字符数应该等于目标字符串`target`的长度。我们还需要定义一个开始索引和一个结束索引来复制`str`的结尾。

让我们看看下面的例子:

```
function confirmEnding(**str**, **target**) {
  let startIndex = **str.length - target.length**;
  let endIndex = **str.length**; //Copy the last characters on the string(str).
  let copiedTarget = str.**slice**(**startIndex**, **endIndex**);}
confirmEnding("Mehdi", "di");
```

*输出:*

```
console.log(**copiedTarget**); //returns: "di" (last 2 characters of str because target's length is 2).// If we called the function with different inputs:
 confirmEnding("Hello world", "Goo");
 console.log(**copiedTarget);** //returns: "rld"
```

正如你在上面看到的，我们使用 slice 方法根据目标字符串`target`复制字符串`str`的结尾。如果你不熟悉切片法，你可以看看我下面的文章:

[](https://medium.com/javascript-in-plain-english/the-difference-between-slice-and-splice-in-javascript-af7043055f36) [## JavaScript 中切片和拼接的区别

### JavaScript 方法:切片与拼接及示例。

medium.com](https://medium.com/javascript-in-plain-english/the-difference-between-slice-and-splice-in-javascript-af7043055f36) 

复制完字符串的结尾后，我们只需要检查它是否等于目标值。

看看下面的例子:

```
function confirmEnding(**str**, **target**) {
  let startIndex = **str.length - target.length**;
  let endIndex = **str.length**;//Copy the last characters on the string(str).
  let copiedTarget = str.**slice**(**startIndex**, **endIndex**);//Check if the copiedTarget is equal to the target.
if(copiedTarget === target){
  return **true**;
}else{
  return **false**;
}
}confirmEnding("Mehdi", "di"); // returns true
confirmEnding("I love JavaScript", "java"); // returns false
confirmEnding("Mehdi", "hdi"); // returns true
```

就这样，现在函数根据目标字符串`target`和复制的字符串结尾`str`的相等性返回`true`或`false`。

# 结论

算法是练习你解决问题能力的好方法。这就是我解决这个简单算法的方法。如果你知道其他解决的方法，请告诉我。

感谢您阅读本文，希望您觉得有用。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*下面是另一篇有用的文章，请点击链接查看:*

[](https://medium.com/javascript-in-plain-english/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba) [## 10 个令人敬畏的前端开发工具来提高您的生产力

### 你可能需要用到的有用的前端开发工具。

medium.com](https://medium.com/javascript-in-plain-english/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba)