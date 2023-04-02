# JavaScript 算法:向左旋转数组

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-rotate-array-to-the-left-3767dcf60773?source=collection_archive---------1----------------------->

## 编写一个函数，将数组向左旋转一个位置。

![](img/86b2831f8280f6aaf7cba88875f96d46.png)

Photo by [Nick Fewings](https://unsplash.com/@jannerboy62?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`rotateLeft`的函数，它将接受一个数组`arr`作为参数。

给你一个数组。数组中的内容并不重要，因为该函数的目标是将数组中每个元素的位置向左移动一位。数组中的第一项将位于数组的末尾。

```
let arr = [1, 2, 4, 5];
rotateLeft(arr);// output [2, 4, 5, 1]
```

在上面的例子中，数组旋转。数组的新位置应该是其当前位置减一。所以第一个元素放在数组的后面，第二个元素变成第一个元素，第三个变成第二个，依此类推。

你得到了图像。现在，让我们把它变成代码。

因为我们正在旋转数组，所以我们唯一需要做的事情就是将第一个数组项重新定位为数组中的最后一个项。这将使每个数组项的索引减一。为了移除数组中的第一个元素，我们将使用`shift()`方法。

我们将把第一个字符赋给一个名为`first`的变量。

```
let first = arr.shift();
```

`shift()`方法从数组中移除第一个元素并返回移除的元素。这个方法也是可变的，这意味着它改变了数组。如果您要控制台`arr`数组，它将返回数组，但没有原始的第一个元素。

现在我们有了第一个元素，我们将使用`push()`方法把它重新定位到数组的后面。

```
arr.push(first);
```

现在，数组中的所有项都向左移动了一个位置。我们返回我们的新数组。

```
return arr;
```

就是这样。以下是剩余的代码:

如果你想阅读更多的 JavaScript 算法文章，这里有一些最近的:

[](https://levelup.gitconnected.com/javascript-algorithm-pre-populate-an-array-461c758ce903) [## JavaScript 算法:预先填充一个数组

### 我们编写了一个函数，它将输出一个从 1 到 n 的数组，而不使用 for 循环

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-pre-populate-an-array-461c758ce903) [](https://levelup.gitconnected.com/javascript-algorithm-difference-of-two-arrays-5bea5ea50e1f) [## JavaScript 算法:两个数组的区别

### 我们将编写一个函数，返回两个数组的对称差。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-difference-of-two-arrays-5bea5ea50e1f) [](https://medium.com/javascript-in-plain-english/javascript-algorithm-convert-html-entities-99719d8ca118) [## JavaScript 算法:转换 HTML 实体

### 编写一个函数，将选定数量的字符转换成相应的 HTML 实体。

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-convert-html-entities-99719d8ca118)