# JavaScript。at()方法将改变你处理字符串和数组的方式

> 原文：<https://javascript.plainenglish.io/the-javascript-at-method-will-change-the-way-you-handle-strings-and-arrays-403bb68c5fe8?source=collection_archive---------5----------------------->

![](img/109ff7612656d6ff79bb88f3ef27fc5f.png)

JavaScript `.at()`方法是在 ECMA International TC39 的相对索引提案的 8 月发布中引入的，以允许开发人员基于他们的索引获取元素。

在 JavaScript 中选择元素是开发中经常发生的事情，但是，在引入`.at()`方法之前，JavaScript 已经有了从列表的开头或结尾或者在一个字符串中选择元素或字符的方法和技术。

括号符号`[]`通常用于获取特定索引处的元素。但是，这也有缺点。例如，我们不能使用像`arr[-1]`这样的负索引语法来访问列表中的最后一项，这在 Python 中很流行。

因此，开发人员求助于使用`slice()`方法和`length`属性从列表末尾抓取项目。尽管如此，它们也有各自的缺点。

在本教程中，我们将看看 JavaScript `.at()`方法，它的用例，以及与现有方法相比，它如何改善开发人员的体验。

# 可索引对象原型

`.at()`方法位于可转位物体的`prototype`上。

这些可以制定索引条目的对象包括类似于`Array`、`String`和`TypedArray`的类，它们分别是`Array.prototype.at()`、`String.prototype.at()`和`%TypedArray%.prototype.at()`。

因此，我们可以直接在这些可索引对象上执行`.at()`方法。

# 获取列表元素的现有方法

为了了解`.at()`方法的优势，我们将快速浏览一些现有的方法，以便进行比较。这也将作为初学者的复习。

让我们考虑一个名为`arr`的元素数组:

```
const arr = [1, 2, "three", 4, 5, true, false];
```

通过在`arr`数组上使用括号符号`[]`，我们可以获得特定索引处的元素。例如，`arr[0]`返回第一个元素，`1`，依此类推。但是，要从未知长度的末端获取一个项目，我们使用`length`属性或`slice()`方法。

# 使用`length`属性

`length`属性的语法编写如下:

```
arr[arr.length - N];
```

这里，`N`等于从列表末尾开始的第 n 个元素，通过使用该语法，我们可以从列表末尾获取任何元素。

在下面的代码中，我们使用语法来获取`arr`数组的最后一个元素:

```
const arr = [1, 2, "three", 4, 5, true, false];
const lastItem = arr[arr.length - 1];
console.log(lastItem);  // Expected Output: false
```

这样做很好，但是对于一个简单的任务来说，语法可能不方便而且很乏味。此外，在处理函数的返回值时，它的一个缺点是迫使我们在应用语法之前首先将返回值存储在一个变量中:

```
function appendNumber(arr, N) {
  arr.push(N);
  return arr;
}

const tempArr = appendNumber([1, 2, "three", 4, 5, true, false], 6);
console.log(tempArr[tempArr.length - 1]); // Expected Output: 6
```

在上面的代码中，在应用`length`属性之前，`appendNumber()`函数的返回值首先存储在`tempArr`变量中。

# `slice()`方法

开发人员也可以[使用](https://blog.logrocket.com/javascript-array-methods/slice) `[slice()](https://blog.logrocket.com/javascript-array-methods/slice)` [方法](https://blog.logrocket.com/javascript-array-methods/slice)使用下面的语法抓取列表的最后一项:

```
arr.slice(-1)[0]
```

这种语法允许负索引，您将在本教程后面的`.at()`方法中看到。

这里的负索引表示从数组末尾的偏移量。例如，`slice(-1)`从后面删除最后一项并返回一个新数组；`slice(-2)`删除最后两个，依此类推。

但是在这里，焦点是最后一项，因此是语法中的`slice(-1)`。然后，`[0]`符号选择该索引处的项目。

使用该语法，我们可以获取`arr`数组的最后一项，如下所示:

```
const arr = [1, 2, "three", 4, 5, true, false];

console.log(arr.slice(-1)[0]); // Expected Output: false
```

与上面的`length`属性不同，这个方法不强迫我们在使用语法之前存储函数的返回值。因此使其更加灵活:

```
function appendNumber(arr, N) {
  arr.push(N);
  return arr;
}

console.log(appendNumber([1, 2, "three", 4, 5, true, false], 6).slice(-1)[0]); // 6
```

尽管如此，语法看起来很奇怪，没有描述它的意图。当然，这也很不方便。

# 为什么不用`arr[-1]`访问最后一个数组元素？

这个问题经常出现在 JavaScript 初学者身上，尤其是如果他们来自 Python 这样的编程语言。

JavaScript 中的`arr[-1]`符号是一个有效的对象属性。记住 JavaScript 中的一切，包括数组，都是对象。所以每当我们使用括号符号时，例如，`arr[0]`，我们用键`0`引用对象的属性。

通过重写对象符号中的`arr`数组，我们得到了这样的结果:

```
const arr = {
  0: 1,
  1: 2,
  3: "three",
  // ...
};

console.log(arr[0]); // Expected Output: 1
```

在上面的代码中，我们没有一个键`-1`。所以，`arr[-1]`返回一个值`undefined`。如果对象属性有一个键`-1`，如下面的代码所示，`arr[-1]`将返回其相应的值:

```
const arr = {
  "-1": "valid"
};

console.log(arr[-1]); // Expected Output: valid
```

这意味着我们不能使用`arr[-1]`来抓取最后一个元素，因为它已经是一个有效的语法了。为了使用负索引语法从列表末尾返回一个元素，我们将使用`.at()`方法。

# `.at()`语法

当使用`.at()`语法时，它接收要返回的项的索引。当传递负索引时，它从列表或字符串的末尾开始计数，并返回找到的项或字符。否则，返回`undefined`:

```
at(index)
```

# `.at()`实践中的方法

如前所述，`.at()`方法接收要返回的项目的索引。在这一节中，我们将讨论它的用例。

让我们重温一下`arr`数组，看看`.at()`方法如何让我们无缝返回一个索引元素:

```
const arr = [1, 2, "three", 4, 5, true, false];

console.log(arr.at(0)); // Expected Output: 1
console.log(arr.at(2)); // Expected Output: "three"
console.log(arr.at(-1)); // Expected Output: false
console.log(arr.at(-3)); // Expected Output: 5
```

当一个正索引传递给`.at()`方法时，它返回该索引处的元素。对于负索引，它从列表中的最后一个元素开始倒数，并返回该元素。

在上面的代码中，`at(-1)`从数组末尾开始计数 1，并返回`false`，这是找到的元素。同理，`at(-3)`从末尾数三，返回`5`。

像数组一样，我们可以对字符串做同样的事情:

```
const str = "The last alphabet is z";

console.log(str.at(0)); // Expected Output: T
console.log(str.at(-1)); // Expected Output: z
```

正如我们所见，这种方法使用起来很愉快。仅仅用`.at(-1)`，我们就得到`str`字符串的最后一个字符。如果我们对`length`属性执行同样的任务，我们会有一个更长的语法，就像这样:

```
console.log(str[str.length - 1]); // Expected Output: z
```

# 处理函数的返回值

与`length`属性不同的是，`.at()`方法不会强迫我们在使用函数之前将返回值存储在变量中。

下面的代码输出推入数组的最后一个元素:

```
function appendNumber(arr, N) {
  arr.push(N);
  return arr;
}console.log(appendNumber([1, 2, "three", 4, 5, true, false], 6).at(-1));
// Expected Output: 6
```

在代码中，`.at()`方法直接应用于返回值，而无需先将值存储在变量中。

# `.at()`方法接受带小数的数字

当一个带小数的数字传递给`.at()`方法时，它会考虑小数点前的值，并返回该索引处的项。

让我们来看看下面的代码:

```
const arr = [1, 2, "three", 4, 5, true, false];
console.log(arr.at(0.6)); // Expected Output: 1
console.log(arr.at(-3.6)); // Expected Output: 5
```

在上面的代码中，第一个控制台输出索引为`0`的项目，而第二个控制台从数组末尾开始计数 3，并输出找到的项目。

当我们想要随机选择一个索引元素时，这是有益的。这可以用一个石头剪子布游戏项目来演示。我们可以使用`.at()`方法语法来为计算机确定一个随机选择。

下面的代码说明了我们如何应用`.at()`方法来随机选择计算机的选项:

```
const computerOptions = ["rock", "paper", "scissors"];
const randomIndex = Math.random() * computerOptions.length;console.log(computerOptions.at(randomIndex));
```

![](img/bab98d33ef4d8190993fa9dd8aa0529c.png)

```
const arr = [1, 2, "three", 4, 5, true, false];
console.log(arr[0.6]); // Expected Output: undefined
```

`.at()`方法为我们省去了使用`Math.floor`对随机数取整的额外步骤。

# 结论

正如我们在本教程中所看到的,`.at()`方法在根据索引抓取项目时非常有用。与先前存在的方法相比，它使用起来也很简洁。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)