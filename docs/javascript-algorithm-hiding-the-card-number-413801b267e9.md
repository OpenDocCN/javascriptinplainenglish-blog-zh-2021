# JavaScript 算法:隐藏卡号

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-hiding-the-card-number-413801b267e9?source=collection_archive---------3----------------------->

## 编写一个函数，只显示信用卡号的最后四位数字。

![](img/7ca26a66b0e99fb22c326dcb38af1fa6.png)

Photo by [blocks](https://unsplash.com/@blocks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`cardHide`的函数，它将接受一个字符串`card`作为参数。

您会得到一个包含代表信用卡号的数字的字符串。该函数的目标是返回一个字符串，其中除了最后四个数字外，所有数字都被星号替换。字符串长度必须保持不变。

示例:

```
cardHide("1234123456785678") // "************5678"
cardHide("8754456321113213") // "************3213"
```

在上面的例子中，您可以看到，当函数返回隐藏的信用卡号时，它隐藏了所有带有星号的值，除了最后四位数字。

为了开始用代码编写，我们将创建一个名为`hideNum`的数组。这是函数将返回的变量。最初，它是一个数组，但我们将把它输出为一个字符串。

```
let hideNum = [];
```

接下来，我们将使用 for 循环来遍历字符串。在循环中，我们用星号替换字符，直到到达字符串中倒数第四个数字或字符。

```
for(let i = 0; i < card.length; i++){
  if(i < card.length-4){
    hideNum.push("*");
  }else{
    hideNum.push(card[i]);
  }
}
```

一旦循环到达那个点，它将把字符串的最后四个字符添加到`hideNum`数组中。

循环结束后，我们得到一个包含部分隐藏的信用卡号的数组。要将数组转换成字符串，我们使用`join()`方法并传递一个空字符串，让该方法知道我们不希望字符之间有任何内容。之后，我们返回字符串。

```
return hideNum.join("");
```

我们的代码到此结束。

*注意，这是**解决这个问题的一种**方式。您可以使用一行正则表达式语句来解决这个问题。我们的目标不是用最有效的一行方法来解决一个算法。目标是解决问题。当你对 JavaScript 有了更多的了解后，你可以改进它，让它变得更好。

下面是该函数的其余部分:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](https://levelup.gitconnected.com/javascript-algorithm-array-plus-array-19e17c70e9fe) [## JavaScript 算法:数组加数组

### 写一个计算两个数组之和的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-array-plus-array-19e17c70e9fe) [](https://levelup.gitconnected.com/javascript-algorithm-title-case-a-sentence-995da42238f0) [## JavaScript 算法:标题大小写一句话

### 我们写了一个将字符串转换成标题大小写的函数

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-title-case-a-sentence-995da42238f0) [](https://levelup.gitconnected.com/javascript-algorithm-take-the-first-n-elements-31c971312ff2) [## JavaScript 算法:取前 N 个元素

### 我们将编写一个函数来返回数组中的前 n 个元素。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-take-the-first-n-elements-31c971312ff2)