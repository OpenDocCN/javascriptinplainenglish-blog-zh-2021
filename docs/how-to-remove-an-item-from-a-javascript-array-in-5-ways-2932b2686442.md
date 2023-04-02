# 如何用 5 种方法从 JavaScript 数组中移除一个项目

> 原文：<https://javascript.plainenglish.io/how-to-remove-an-item-from-a-javascript-array-in-5-ways-2932b2686442?source=collection_archive---------12----------------------->

![](img/21f1fe4cc895c56e954f55262e13666b.png)

How to remove an item from a JavaScript array in 5 ways

> 有许多方法可以从 JavaScript 数组中移除项目。在这篇文章中，我们将看看 5 种方法来做到这一点。

出于这样或那样的原因，有时您希望从 JavaScript 数组中移除项目。嗯，有很多选择，但是有了很多选择，也就意味着有很多可能出错的空间。这就是你在这里的原因。

像任何其他编程语言一样，JavaScript 允许程序员使用数组对象，是的，对象。强调将数组作为对象的原因是因为 JavaScript 数组是对内存中地址的实际引用。因此，**你在这个数组上所做的任何改变**，都将在你使用它的过程中保持不变。

好了，有了这个简单的介绍，接下来的事情就是介绍我们在这篇文章中将要用到的方法。我们将使用内置的和通用的方法来完成工作。所以，事不宜迟，我们开始吧！

另外，免责声明，下面的顺序是随机的，不基于任何偏好。而且，每种方法都会被标记为是**在位**还是**不在位**。

## 1.内置 array.filter()

**模式:格格不入。**

这个方法基本上接收一个条目列表，然后使用一个**决定函数**来决定什么将被保留，什么将从数组中删除。

然后它创建一个新的数组(因此一个 JavaScript 数组对象的新地址),您可以将它分配给正在过滤的数组。

通过这种方式，JavaScript array filter 为您提供了将结果放入一个新的 JavaScript 数组或分配给应用该操作的原始数组的选项，以删除您不想要的结果。

例如:

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

首先，我们创建一个从 1 到 10 的简单列表。然后我们得到一个要求，我们只需要显示上面列表中的偶数。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// now we want to remain with even numbers from the above array
numbersOneToTen = numbersOneToTen.filter(num => num % 2 === 0);
```

我们知道偶数可以被 2 整除，所以我们使用模运算符。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// now we want to remain with even numbers from the above array
numbersOneToTen = numbersOneToTen.filter(num => num % 2 === 0)

// now let's print it out
console.log(numbersOneToTen);

// we should see
// [ 2, 4, 6, 8, 10 ]
```

现在，当我们记录时，我们应该只剩下偶数，因为我们从 JavaScript 数组过滤结果中**重新分配**出新数组给我们应用过滤的原始数组。

**好的，问题** **给你**。如果我们没有将结果重新分配给 **numbersOneToTen** 数组，您认为会发生什么？好吧，给你个提示，**在位** vs **不在位**。

好了，现在开始下一个。

## 2.内置 array.slice(可选 Start，可选 End)

**模式:错位**

这是一个内置方法，如您所见，它接受 optionalStart 和 optionalEnd，用于返回数组的一部分。

**NB:**optional start 和 optionalEnd 的索引是从零开始的，这意味着它们从 0 开始。

所以，让我们用这个例子:

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

我们再一次创建一个假设的数字数组。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// now we use slice
numbersOneToTen = numbersOneToTen.slice(3, 8);
```

这里，我们指定开始为 3，结束为 8。因此，关于 slice 的 optionalStart 和 optionalEnd，需要注意的**重要的**一点是，得到的数组将**包含开始的项，不包含结束的项**。

因此，我们的 JavaScript 数组将包含索引 3 处的项目和索引 8 之前的项目。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// now we use slice
numbersOneToTen = numbersOneToTen.slice(3, 8);

// now let's print it out
console.log(numbersOneToTen)

// we should see
// [ 4, 5, 6, 7, 8 ]
```

如你所见，我们的列表从 4 开始，一直到 8。因为 4 在索引 3(从 0 开始)，8 在索引 7(从 0 开始)。

**提示:** JavaScript 数组切片设置要包含的内容的边界。

好吧，我们继续下一个！

## 3.内置 array.splice(必需 Start，可选 DeleteCount)

**方式:原地**

这是我们看到的第一个具有原位修改方法的方法。好吧，这是什么意思？这意味着我们不需要分配 JavaScript 数组拼接操作的结果，因为:

*   该方法返回删除的内容，而不是应该留在数组中的内容。
*   修改直接在 JavaScript 数组上完成。

记住这一点，在使用这个方法从 JavaScript 数组中移除时要非常小心。

如您所见，它也接受一些参数。第一个是 requiredStart，这是一个强制的从零开始的索引，表示拼接应该在何时开始。

它还有一个 optionalDeleteCount，这是要删除的项目数量的数值。所以，这不是从零开始的，而是一个实际的单位。例如，如果您将其设置为 1，则 1 个项目将被删除，以此类推。

举个例子:

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

像往常一样，我们声明我们的数组。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// let's remove everything above index 5
numbersOneToTen.splice(4);
```

现在，我们决定删除索引 5 以上的所有内容。注意，我们没有传入 deleteCount，这意味着超过 requiredStart 索引的所有内容都将被删除。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// let's remove everything above index 5
numbersOneToTen.splice(4);

// now let's print it out
console.log(numbersOneToTen);

// we should be left with
// [ 1, 2, 3, 4 ]
```

好了，现在是提问时间，我们有两个问题:

*   如果我们将 numbersOneToTen 赋给 JavaScript 数组拼接的结果，你认为会显示什么？去试试这个。
*   当您尝试不同的 deleteCounts 时会显示什么？好吧，试试看！

旅程继续！

## 4.内置于 array.pop()

**方式:就地**

这是另一个需要从 JavaScript 数组中移除的同步变量。JavaScript array pop 所做的是从数组中移除最后一个元素，并返回该元素。这意味着:

*   不需要将数组赋给 pop()方法的结果。
*   返回值将是一个项，而不是一个数组。

举个简单的例子:

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

我们再次声明我们的 JavaScript 数组。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// by default, pop removes the last item from the array
numbersOneToTen.pop();
```

然后我们在数组上运行调用 pop()方法。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// by default, pop removes the last item from the array
numbersOneToTen.pop();

// now let's print it out
console.log(numbersOneToTen);

// we should see
// [ 1, 2, 3, 4, 5, 6, 7, 8, 9 ]
```

因此，记住，我们不需要向 pop()方法传递参数。

好了，是时候问一个简单的问题了:

*   当你试图在一个空的 JavaScript 数组上调用 pop()会发生什么？
*   当你把 numbersOneToTen 赋值给 pop()的结果时，你看到了什么

好了，现在谈最后一个。

## 5.旧学校重新分配到空数组

**模式:错位**

这种方法只需要将数组分配给一个新数组。因为我们没有直接调用它的方法，所以在我看来，这是一个不合适的方法，因为我们给了它一个新的引用 JavaScript 数组对象(一个空的)

因此，这个方法将完全删除数组中的所有内容。所以有了这样的行为，慎用！

一个简单的例子:

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
```

像往常一样，我们声明我们的数组。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// let's assign to empty array
numbersOneToTen = [];
```

然后我们分配它。

```
// create a new array of numbers one to ten
let numbersOneToTen = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// let's assign to empty array
numbersOneToTen = [];

// now let's print it out
console.log(numbersOneToTen);

// we should now see
// []
```

现在，提问时间:

*   如果我们用常量 numbersOneToTen 代替 let numbersOneToTen，你认为会发生什么？

## 结论

如您所见，从 JavaScript 数组中移除 item 非常简单。你所需要的是了解你的具体需求是什么，然后用正确的方法去做。

**练习**:嗯，你看，在上面的例子中，我们用了 **let numbersOneToTen** ，你为什么不用 **const numbersOneToTen** 来代替。让我知道你会怎么做。

谢谢你的阅读，直到下一篇！

**快乐编码！**

> 有兴趣学习 **JavaScript** 吗？在我的网站上查看类似的精彩文章:[沉迷于代码> JavaScript](https://bingeoncode.com/category/javascript)

*更多内容看* [***说白了. io***](http://plainenglish.io/)