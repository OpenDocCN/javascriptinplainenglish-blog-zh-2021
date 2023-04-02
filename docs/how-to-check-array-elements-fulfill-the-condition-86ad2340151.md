# 检查数组元素是否满足给定条件的最佳方法

> 原文：<https://javascript.plainenglish.io/how-to-check-array-elements-fulfill-the-condition-86ad2340151?source=collection_archive---------21----------------------->

![](img/fcd5aaf44705d75c33a9cf24cf9b0c5f.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有一些方法可以检查数组的元素是否满足给定的条件。例如，是否每个元素都是偶数，或者数组中是否有我想要的元素。让我们看看如何在 JavaScript 中使用它们。

# 1.数组.原型.每

如果您想确保每个元素都满足条件，那么使用`every()`方法是最合适的。

## every()方法说明

`every()`方法为数组中的每个元素执行一次回调函数，直到找到回调函数返回一个 falsy 值的元素。**如果发现这样的元素**,`every()`方法**立即返回 false** 。否则，**如果回调为所有元素**返回真值，则`every()`方法**返回真值**。

看看这个例子。

***注意*** *:在空数组上调用* `*every()*` *方法将对任何条件返回* ***真*** *！看看这个例子。因此，您需要编写额外的代码来防止意外的结果。*

看看这个例子。

# **2。Array.prototype.some**

如果你想检查一个或多个元素是否满足条件，有`some()`方法。

## some()方法描述

`some()`方法对数组中的每个元素执行一次回调函数，直到找到回调函数返回一个*真值*的元素。**如果发现这样的元素**，`some()`方法**立即返回 true** 。否则，**如果回调为所有元素返回一个 false 值，** `some()`方法**返回 false** 。

看看这个例子。

***注意*** *:在空数组上调用* `*some()*` *方法，对于任何条件都会返回****false****！因此，您需要编写额外的代码来防止意外的结果。*

看看这个例子。

# 3.Array.prototype.find 或 Array.prototype.findIndex

您还可以使用这两种方法来检查数组是否包含您需要的内容。但是**我不推荐在你只想检查数组是否包含你需要的东西的时候使用它们**，因为代码不仅仅是给你的。你必须有目的地写代码。

`find()`和`findIndex()`方法完全按照它们所说的去做。如果你用`find()`或`findIndex()`方法检查数组是否包含你需要的东西，那么后来读到这段代码的程序员可能会认为是**去找**你需要的东西，**不去检查数组是否包含**你需要的东西。但是万一你仍然想使用它们，我已经用下面的例子写下了它们的描述。

## find()方法描述

`find()`方法对数组的每个索引执行一次回调函数，直到回调返回一个真值。如果是，`find()` **立即返回该元素**的值。如果回调从不返回真值(**或数组长度为 0** )，则`find()`方法**返回未定义的**。

## findIndex()方法描述

`findIndex()`方法对数组中的每个索引执行一次回调函数，直到找到 callback 返回真值的那个索引。如果找到这样的**元素，** `findIndex()` **立即返回该元素的索引**。如果回调从不返回真值(**或数组长度为 0** )，则`findIndex()`方法**返回-1** 。

# 结论

我今天解释的函数都是相当众所周知的函数，但是**人们不知道数组为空时的返回值**。所以，下次别忘了写我上面解释的附加条件。另外，**不要忘记写代码，同时记住你的意图！**很重要！

我希望这对你有用。感谢您的阅读。编码快乐！

# 参考

*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Array/every](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Array/some](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/some)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Array/find](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Array/find index](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/findIndex)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)