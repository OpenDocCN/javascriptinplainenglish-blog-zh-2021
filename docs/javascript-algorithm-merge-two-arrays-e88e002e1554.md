# JavaScript 算法:合并两个数组

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-merge-two-arrays-e88e002e1554?source=collection_archive---------13----------------------->

## 用 JavaScript 编写两种合并两个数组的方法。

![](img/291a0cbdcef79aa08b90d20d93b81d34.png)

Photo by [Lucas Benjamin](https://unsplash.com/@aznbokchoy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将创建一个名为`mergeArrays`的函数，它将接受两个数组`arr1`和`arr2`作为参数。

该函数的目标是合并两个数组，并返回一个包含合并数组的新数组。我们将研究将两个数组合并在一起的两种方法。一种方法是使用`for...of`循环，另一种方法是使用 JavaScript 方法`concat()`。

示例:

```
let arr1 = [1, 2, 3];
let arr2 = [4, 5, 6];
mergeArrays(arr1, arr2);//output: [1, 2, 3, 4, 5, 6];
```

## 对于…的循环示例

由于我们需要在合并`arr1`和`arr2`之后返回一个新数组，我们将创建一个名为`arr3`的新变量，并为其分配一个空数组。

```
let arr3 = [];
```

接下来，我们将使用`for...of`循环迭代`arr1`并将该数组中的所有元素推入`arr3`数组。

```
for(el of arr1){
   arr3.push(el);
}
```

我们对`arr2`阵列也是如此。

```
for(el of arr2){
   arr3.push(el);
}
```

现在两个数组合并到`arr3`中了，我们可以返回了。

```
return arr3;
```

就这样。以下是完整的代码:

## Concat()方法

JavaScript 中的`concat()`方法更加简单。它已经做了我们希望我们的函数做的事情，即合并两个或多个数组。在上面的例子中，如果您想要合并两个以上的数组，您将需要使用两个以上的`for...of`或 for 循环。

要合并`arr1`和`arr2`，我们只需要写一行:

```
arr1.concat(arr2);
```

这将返回一个新的数组，因此我们将新的数组分配给一个名为`arr3`的变量并返回它。

```
let arr3 = arr1.concat(arr2);
return arr3;
```

以下是完整的功能:

如果您认为这个算法有帮助，请查看我的其他 JavaScript 算法解决方案:

[](https://levelup.gitconnected.com/javascript-algorithm-reverse-a-string-c24d06129f03) [## JavaScript 算法:反转字符串

### 创建两种在 JavaScript 中反转字符串的方法

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-reverse-a-string-c24d06129f03) [](https://medium.com/javascript-in-plain-english/javascript-algorithm-reverse-an-array-without-using-reverse-238c9f58362a) [## JavaScript 算法:在不使用反向的情况下反向数组()

### 编写一个函数来反转一个小数组，而不使用内置的 JavaScript 反转方法。

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-reverse-an-array-without-using-reverse-238c9f58362a) [](https://medium.com/javascript-in-plain-english/javascript-algorithm-rotate-array-to-the-left-3767dcf60773) [## JavaScript 算法:向左旋转数组

### 编写一个函数，将数组向左旋转一个位置。

medium.com](https://medium.com/javascript-in-plain-english/javascript-algorithm-rotate-array-to-the-left-3767dcf60773)