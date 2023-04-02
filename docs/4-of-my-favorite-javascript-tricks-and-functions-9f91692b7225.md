# 我最喜欢的 4 个 JavaScript 技巧和函数

> 原文：<https://javascript.plainenglish.io/4-of-my-favorite-javascript-tricks-and-functions-9f91692b7225?source=collection_archive---------20----------------------->

## 对任何 JavaScript 开发人员都很有用。

![](img/6b6c7713613dfb1e83b752831a691b2d.png)

taken from javascript.com

在使用不同的 JavaScript 框架做前端工作的几年中，我看到一些不同的函数被频繁使用。无论你用什么语言编写，你都需要知道如何迭代数组，操作数组，以及访问不同的元素。您还将认识到正确处理错误和正确使用条件的重要性。当在 React 应用程序中向 UI 呈现元素时，您经常需要找到不同的方法来以正确的方式显示数据。

我已经试验了其中的一些功能，并选定了一些我最喜欢使用的功能。这里列出了我在前端看到并经常使用的 JavaScript 函数和技巧。

## 映射函数对数组元素执行操作

当遍历一个数组时，通常会想到一个`for`或`while`循环。我发现 [javascript 映射函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)同样有用，而且更容易使用。以下是 for 循环与 map 函数的一个示例:

假设你有一个数组，你想遍历每一个数组，并把它们翻倍。下面是一个 JavaScript for 循环，用于遍历数组中的每个整数并使其翻倍:

```
const numbersArray = [ 1, 2, 3, 4, 5];
for (i = 0; i < numbersArray.length; i++) {
  numbersArray[i] = numbersArray[i] * 2;
}// numbersArray is [2, 4, 6, 8, 10]
```

这是与地图相同的功能:

```
const numbersArray = [ 1, 2, 3, 4, 5];
numbersArray.map(num => {
  return num * 2;
});// numbersArray is [2, 4, 6, 8, 10]
```

我喜欢映射函数，因为它们易于实现。这通常可用于改变数组的部分内容，或者呈现前端库中的元素列表，如 React。您不必担心长度、索引或使用映射函数增加计数器，这就是我喜欢它用于大多数用例的原因。

## 筛选以缩小特定数组元素的范围

通常，我们必须在数组中找到一个对象，或者过滤掉数组的某些部分。您可以在一个数组上使用 [filter()函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)来返回一个满足特殊条件的数组。

假设您需要从一组数字中筛选出偶数:

```
const numbersArray = [ 1, 2, 3, 4, 5];
const evenNumbersArray = numbersArray.filter(number => {
  return number % 2 === 0;
});console.log(evenNumbersArray); // [2, 4]
```

当您不需要每个数组元素时，过滤是必不可少的。也许你只想呈现数组中满足特定条件的一些元素。

[find()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find) 函数与 filter()非常相似。它根据您提供的条件返回所需对象的第一个实例。注意，这将返回一个对象而不是一个数组，所以您需要以稍微不同的方式访问数据。

## 代替 If 语句检查的短路条件

最常见的 Javascript 运行时错误之一是`“Cannot read property ‘x’ of undefined”`错误。有时，在对某个值执行操作之前，您需要检查该值是否存在。如果你试图对一个未定义的对象或数组执行操作，你会得到一个错误。

假设你要对一个数组进行排序。为了避免这种运行时错误，您必须首先确保数组存在。这可以这样做:

```
if (arrayExists) {
  array.sort();
}
```

这一行代码用[逻辑 AND 运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_AND)做了同样的事情:

```
arrayExists && array.sort()
```

如果 arrayExists 返回 false，则不会计算运算的右侧。这有助于在前端工作时确保您不会遇到“未定义的”运行时错误。适当的错误处理应该包括任何时候存在被访问的数据未定义的风险时的这些检查。

## 三元代替 if

如果是有条件地给变量赋值，则不需要 If 语句。

下面是一个笨拙的 if-else 语句:

```
let errorText;
if (isError) {
  errorText = 'An Error Occurred';
} else {
  errorText = 'No Error';
}
```

现在，一行[三进制](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)为同一代码:

```
const errorText = isError ? 'An Error Occurred' : 'No Error';
```

5 行代码压缩到一行？我觉得不错。这个必须是正确使用最令人满意的。

最后，在 JavaScript 中有很多方法可以有效地执行这些操作。这里是我经常使用的一些方法来完成工作。

请记住，语言是随着时间而发展的。新版本出来，新的编程功能成为常态。我的建议是，当你在代码中看到新的代码时，尝试一下，看看你是否喜欢它们！当你阅读其他开发者写的代码时，你知道的这些函数越多，你就会理解的越多。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)