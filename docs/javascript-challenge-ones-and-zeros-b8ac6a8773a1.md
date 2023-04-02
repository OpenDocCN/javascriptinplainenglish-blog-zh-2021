# JavaScript 挑战:1 和 0

> 原文：<https://javascript.plainenglish.io/javascript-challenge-ones-and-zeros-b8ac6a8773a1?source=collection_archive---------8----------------------->

## 让我们使用 JavaScript 来解决一个简单的编码挑战。

![](img/12467031edbf229a7a030f7c96ec3010.png)

Photo by [heylagostechie](https://unsplash.com/@heylagostechie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

编码挑战是练习编码技能的好方法。我们都知道，解决问题是所有开发人员的必备技能。这就是为什么你应该总是试图解决编码挑战，因为如果你大量练习，它们也可以提高你解决问题的技能。

在本文中，我们将尝试使用 JavaScript 解决来自 CodeWars 的一个简单的编码挑战。让我们开始吧。

# 说明

我们有一个名为`binaryToNumber`的函数，它接受一个数组作为它的参数。

数组参数应该包含 1 和 0。我们的工作是获取这些数字(1 和 0)，然后将它们从二进制转换成等价的数字形式。

例如:`[0, 0, 1, 0]`被当作是`2`的二进制表示`0010`。

下面是函数示例:

```
const binaryToNumber = arr => {
  //Your Code here.
}; //Examples:
binaryToNumber([0, 1, 1, 0]) should return 6
binaryToNumber([1, 1, 1, 1]) should return 15
binaryToNumber([0, 0, 0, 1]) should return 1
```

如您所见，挑战非常简单。现在我们需要将这些 0 和 1 连接起来，并将它们从二进制形式转换成等价的数字表示。

# 解决办法

我解决这个编码挑战的方法是首先使用`join()`方法加入数组，以获得字符串形式的二进制形式。然后，我将使用方法`parseInt`将二进制形式转换为数字。

*   加入阵列:

```
const binaryToNumber = arr => {
  return **arr.join('');**
};console.log(binaryToNumber([0, 1, 1, 0])); //returns '0110'
```

*   将二进制字符串转换为等效的数字:

现在我们可以使用方法`parseInt()`，在这种情况下它应该有两个参数:我们想要转换的字符串和基数(二进制的基数是 2)。

下面是一个例子:

```
//convert the binary string to number.
**parseInt(arr.join(""), 2);** //This will return a number.
```

以下是这个简单挑战的完整解决方案:

```
//Full solution.
const binaryToNumber = arr => {
  return **parseInt(arr.join(""), 2);**
};binaryToNumber([0, 1, 1, 0]) return 6
binaryToNumber([1, 1, 1, 1]) return 15
```

就是这样，我们把连接的数组转换成一个数字。现在我们使用 JavaScript 解决了这个简单的编码挑战。

# 结论

编码挑战非常有用，因为它们教会你如何寻找解决方案来解决编码问题。所以，如果你想提高解决问题的能力，我会鼓励你尝试这些挑战。

感谢您阅读这篇文章。希望你觉得有用。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，可以* [*订阅*](https://mehdiouss.ck.page/) *我的简讯。*

*你可能也喜欢:*

[](/5-awesome-css-features-that-you-probably-dont-know-63f90e66562) [## 你可能不知道的 5 个很棒的 CSS 特性

### 每个 web 开发人员都应该知道的有用的 CSS 特性。

javascript.plainenglish.io](/5-awesome-css-features-that-you-probably-dont-know-63f90e66562)