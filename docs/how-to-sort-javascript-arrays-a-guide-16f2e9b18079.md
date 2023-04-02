# 如何对 JavaScript 数组进行排序:指南

> 原文：<https://javascript.plainenglish.io/how-to-sort-javascript-arrays-a-guide-16f2e9b18079?source=collection_archive---------10----------------------->

![](img/f8df6673ac5c509fdd03c574f759f004.png)

Photo by [Mick Haupt](https://unsplash.com/@rocinante_11?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

对数组排序应该很简单，对吗？如果我有一个字符串数组，我想按字母顺序排序['苹果'，'香蕉'，'黄瓜'…]。如果我有一个数字数组，我希望它是 1，2，3…等等。虽然对数组中的字符串进行排序很简单，但之后会变得更加混乱。让我们先按字母顺序对数组进行排序，然后再按数字顺序进行排序，并找出一些你可能遇到的问题。

# 按字母顺序排序

假设我们有一个包含一些产品名称的数组。要按字母顺序对数组进行排序，非常简单。只要加上 sort()，数组就会神奇地更新。

```
let myArray = ['banana', 'cucumber', 'apple']
myArray.sort();
console.log(myArray); // ['apple', 'banana', 'cucumber']
```

如果我们想按**降序**对数组排序呢？我不认为这是最漂亮的代码，但这是 JavaScript 提供给我们的

```
myArray.sort().reverse();
console.log(myArray); // ['cucumber', 'banana', 'apple']
```

哇，现在你是一个分类大师了！我为什么要写这篇文章？等等，这是最简单的排序用例。让我们深入一点，但不要*太*复杂；数字

# 数字排序

所以在我们的第一个例子中，我们能够调用不带参数的 sort 方法，因为我们正在比较字符串。为了比较数字，我们需要传入一个**回调函数**，它将允许我们操作一些排序逻辑。

## 错误的方式

为了说明为什么我们需要一个回调函数，让我们先试着不用它来排序。

回到代码，让我们创建另一个数组，但是是一个充满数字的数组。让我们使用上一个例子中使用的 sort()来看看会发生什么。

```
let myNumberArray = [2,3,1];
myNumberArray.sort() // (WRONG WAY)
console.log(myNumberArray) // [1,2,3] (WE GOT LUCKY)
```

等等，我想我们应该做些不同的事情？？看起来它们被分类了？？在这种情况下，他们是(我们很幸运)。欢迎来到 JavaScript 的怪癖。为什么这些分类正确？让我给你一个更好的例子，并解释为什么这并不总是工作

```
let myNumberArray = [200,23,12];
myNumberArray.sort(); (STILL WRONG WAY)
console.log(myNumberArray) // [12, 200, 23] (WRONG)
```

看出区别了吗？这一次，我们有 200 个*和 23 个错点*。当然 23 小于 200，但是它在我们数组的末尾！这是因为 **JavaScript 将数字视为字符串。**它比较两个数字的第一个数字“2”，因为它们相同，所以移动到下一个数字。因为“0”小于“3”，所以它将 200 放在 23 的前面，并忽略 200 的第三个数字。

## 正确的方式

让我们再试一次，但是这一次我们将传递一个**回调函数给排序函数**来得到正确排序的数字。现在我们将传入我之前提到的回调函数。首先，我将以冗长的方式来做，然后我将向您展示一种将它压缩成一行代码的方法。

```
function sortNumbers(number1, number2){
   return number1 - number2;
}let myNumberArray = [200,23,12];
myNumberArray.sort(sortNumbers);
console.log(myNumberArray) // [12, 23, 200] (CORRECT)
```

好吧，这到底是怎么回事？让我解释一下。所以这次我们创建了一个叫做 sortNumbers 的**回调函数**。这个函数有两个参数，数字 1 和数字 2。如果数字 1 比数字 2 的*少*，它将返回一个**负值**。如果它们**相等，你会得到 0** 。如果数字 1 大于 T9，你将得到一个正值 T11。

当 sort 函数得到一个**正值时，**它将交换这两个元素，将较大的值推向数组的末尾。所以在这种情况下，排序函数将执行 200-23，结果是-177。**由于数值为负，200 将上移一个索引，23 将下移**。sort 函数中有一些优化，但是您可以假设 sort 方法将比较所有必要的元素，以便在数组中向上或向下移动它们，直到它被排序。多酷啊！

回到代码，你可能在 StackOverflow 甚至官方文档上看到的是这个。虽然许多人可能知道 ES6 的箭头函数，但这段代码可能会让新程序员感到有点害怕。

```
myNumberArray.sort((a, b) => a - b)
```

这段代码和我们写的没什么不同，但是它使用了 ES6 箭头函数和 *a 和 b* 来代替数字 1 和数字 2。要翻译，让我们一步一步地转换我们的原始代码。首先，我们将转换我们的函数来获取它们的参数。

```
function sortNumbers(a, b){
   return a - b;
}myNumberArray.sort(sortNumbers);
```

看，同样的事情，但是我们在这里使用了简化的变量名。数字 1 现在是 a，数字 2 现在是 b。接下来，让我们转换成箭头语法

```
const sortNumbers = (a,b) => {
   return a - b
}myNumberArray.sort(sortNumbers);
```

快到了。现在我们使用一个 arrow 函数，并将其存储在一个 *const sortNumbers* 中，然后像以前一样将它传递给 sort 函数。最后一步是删除 const，然后一次性声明并传入回调函数

```
myNumberArray.sort((a,b) => a - b)); // This uses the implicit return.
```

瞧啊。我们成功了。我们终于能够用一行代码对一组数字进行排序，*并且我们实际上理解了正在发生的事情*

# 结论

对于 JavaScript 排序，我可以深入研究一百万种更复杂的情况(比如先按一个字段再按另一个字段排序，即先按姓氏再按名字排序)，或者按嵌套的对象属性排序，但是这篇文章已经够长了。我鼓励您四处看看，并使用这些代码示例作为模板来创建更复杂的排序函数。

我希望你喜欢这篇文章。如果你想看到更多这样的帖子，请跟我来，留下一些掌声。如有任何问题，请随时联系我们，祝您编码周愉快！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)