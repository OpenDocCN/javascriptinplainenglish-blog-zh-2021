# JavaScript 算法:将字符串转换为字符数组

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-convert-string-to-an-array-of-characters-197f3f64ab79?source=collection_archive---------15----------------------->

## 创建一个将字符串转换为字符数组的函数。

![](img/1e6e12d6599af3ac83e8fb33816b1bd5.png)

Photo by [Susan Holt Simpson](https://unsplash.com/@shs521?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将编写一个名为`arrChar`的函数，它将接受一个字符串`text`作为参数。

给你一个包含一系列文本的字符串。该函数的目标是返回一个包含该字符串中所有字符的新数组。数组应该排除字符串中的所有空白。

示例:

```
arrChar("I don't need calcium. I am calcium.")//output: ["I","d","o","n","'","t","n","e","e","d","c","a","l","c","i","u","m",".","I","a","m","c","a","l","c","i","u","m","."]
```

虽然输出很难阅读，但如果您查看每个字符，就会发现它们都来自字符串。注意，数组输出不包含任何空白字符。

首先，我们将创建一个名为`removeWhitespace`的变量。在我们删除了所有存在于`text`中的空白字符后，这个变量将包含我们的新字符串。

为了去除空白字符，我们将使用`replace()`方法和正则表达式。

```
let removeWhitespace = text.replace(/\s/g, "");
```

正则表达式中的`\s`字符指向任何空白字符。我们用一个空字符串替换这些字符。

接下来，我们将使用`Array.from()`方法把我们的字符串变成一个单个字符的数组。

`Array.from()`所做的是从一个类数组或可迭代对象创建一个新的浅拷贝数组实例。在这种情况下，我们的 iterable 对象是新的`removeWhitespace`字符串。我们把它赋给一个叫做`newArr`的变量。

```
let newArr = Array.from(removeWhitespace);
```

我们也可以使用`removeWhitespace.split("")`来达到同样的结果。

我们通过返回`newArr`来完成我们的函数。

```
return newArr;
```

下面是完整的函数:

如果您发现这个算法很有帮助，请查看我的其他 JavaScript 算法解决方案文章:

[](/javascript-algorithm-calculate-sum-of-numbers-in-a-string-dd007da460b7) [## JavaScript 算法:计算字符串中数字的总和

### 计算以逗号分隔的字符串形式接收的数字的总和。

javascript.plainenglish.io](/javascript-algorithm-calculate-sum-of-numbers-in-a-string-dd007da460b7) [](https://levelup.gitconnected.com/javascript-algorithm-array-average-d917d9b0a1c1) [## JavaScript 算法:数组平均值

### 计算数组中数字的平均值。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-array-average-d917d9b0a1c1) [](https://levelup.gitconnected.com/javascript-algorithm-array-plus-array-19e17c70e9fe) [## JavaScript 算法:数组加数组

### 写一个计算两个数组之和的函数。

levelup.gitconnected.com](https://levelup.gitconnected.com/javascript-algorithm-array-plus-array-19e17c70e9fe)