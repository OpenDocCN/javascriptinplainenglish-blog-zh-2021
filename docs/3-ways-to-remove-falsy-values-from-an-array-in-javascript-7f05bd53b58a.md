# 如何在 JavaScript 中从数组中移除 Falsy 值

> 原文：<https://javascript.plainenglish.io/3-ways-to-remove-falsy-values-from-an-array-in-javascript-7f05bd53b58a?source=collection_archive---------11----------------------->

## 使用 JavaScript 从数组中移除 falsy 值的 3 种方法

![](img/89e12ab86b3b067a5b76c43f682b791e.png)

Photo by [Safar Safarov](https://unsplash.com/@codestorm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中有两种类型的值:假值和真值。作为一名开发人员，你必须知道它们之间的区别，因为很多人误解了它们，认为它们只是真的和假的。因此，在有些情况下，您需要避免 JavaScript 中的虚假值。

这就是为什么在这篇文章中，我们将向您展示用 JavaScript 从数组中删除 falsy 值的 3 种方法。让我们开始吧。

# 1.使用 for 循环

在使用 for 循环从数组中移除 falsy 值之前，让我们先了解一下 falsy 和 truthy 值之间的区别。

JavaScript 中的 Falsy 值是转换成`false`的值。JavaScript 中有六个 falsy 值:`false`、`0`、`NaN`、`""`、`null`和`undefined`。另一方面，真值是转换成`true`的值。除了上述 6 个错误值之外的任何值都是真值。

所以我们有一个名为`removeFalsy`的函数，它有一个数组`arr`作为参数。当我们将包含 falsy 值的数组作为函数的参数传递时，它应该从数组中删除所有的 falsy 值。

为了实现这一点，我们需要在函数内部创建一个新的空数组，并创建一个 for 循环来遍历`arr`，只将真值推送到新的空数组中。

下面是一个例子:

```
function **removeFalsy**(**arr**) {
  //Create a new empty array.
  let newArray = [];

//Loop over the original array(arr) to push truthy values to the  new array.
  **for** (let i = 0; i < arr.length; i++) {
    //If the array item is truthy, push it to the new array.
    **if (arr[i])**{
      **newArray.push(arr[i])**;

    }
  }
  **return newArray**;
}removeFalsy([17, "ate", "", false, 5]); //returns [ 17, 'ate', 5 ]removeFalsy([null, false, 0, NaN, undefined, ""]); //returns []
```

如您所见，通过使用 for 循环，我们能够将所有真数组值推送到一个新数组中。结果，我们得到了一个类似于原始数组`arr`的新数组，但是没有 falsy 值。

# 2.使用 forEach

使用与 for 循环相同的方法，我们可以使用方法`forEach`从数组中删除所有的 falsy 值。

看看下面的例子:

```
function removeFalsy(arr) {
  //Create a new empty array.
  let newArr = []

//Loop over the original array(arr) to push truthy values to the  new array.
 arr.**forEach**(function(item){
 //if the array item is truthy, push it to the new array.
    if(item){
      newArr.push(item);
    }
  });
  return newArr;
}removeFalsy([null, NaN, 5, 6, undefined]) //returns [ 5, 6 ]
```

如您所见，这是相同的方法，只是我们使用了 forEach 方法，而不是 for 循环。

# 3.使用过滤器

filter 方法将回调函数作为其参数。该回调函数返回`true`或`false`。

在这一部分，我们将使用 filter 方法，并将内置的`Boolean`函数传递给它。默认情况下，函数`Boolean`返回`false`。所以我们将从数组中过滤掉所有的 falsy 值。

下面是代码示例:

```
function **removeFalsy**(**arr**) {
  **return arr.filter(Boolean);**
}removeFalsy([null, NaN, 5, 6, undefined]) //returns [ 5, 6 ]removeFalsy([null, false, 0, NaN, undefined, ""]); //returns []
```

如您所见，我们使用内置函数`Boolean`过滤了数组中的所有 falsy 值。我们只用两行代码就实现了我们的目标。

# 结论

这是我知道并使用的三种从数组中移除伪值的方法。如果你知道其他更简单的方法，请告诉我。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/5-useful-javascript-features-that-nobody-is-talking-about-b630838dedba) [## 没有人谈论的 5 个有用的 JavaScript 特性

### 你应该知道的冷门 JavaScript 特性。

javascript.plainenglish.io](/5-useful-javascript-features-that-nobody-is-talking-about-b630838dedba) 

*还有，如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*