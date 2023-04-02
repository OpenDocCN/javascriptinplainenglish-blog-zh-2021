# 如何使用 Map、Filter 和 Reduce 使您的 JavaScript 代码更具功能性

> 原文：<https://javascript.plainenglish.io/how-to-make-your-javascript-code-more-functional-using-map-filter-and-reduce-df160d787f71?source=collection_archive---------14----------------------->

## 在本文中，我们将仔细研究这些函数和一些相关的代码示例。

![](img/772200f157b761eed01208ddc9b4f8dd.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，我们通常使用三种流行的方法来执行数据转换:map、filter 和 reduce。

在本文中，我们将仔细研究这些函数和一些相关的代码示例。

# 。地图( )

`map()`方法获取一个数组，循环遍历该数组，在每次迭代中，它对当前数组元素应用一个回调函数。该函数将原始数组的值映射到一个新数组，这就是它被称为“map”的原因。

假设我们有一系列美元的银行活动，我们想把它们转换成欧元。

```
const movements = [100, -50, 75, -15]
```

首先，让我们将转换率存储到一个单独的变量中。

```
const usdToEur = 0.84;
```

现在，我们可以在`movements`数组上调用`map()`方法。该方法需要一个回调函数，该函数获取当前数组元素作为参数，在本例中为`mov`。在回调函数中，我们返回原始数组的每个元素乘以转换率。这将创建一个新的数组，每个动作都转换成欧元。

为了简化这个函数，我们可以用箭头函数代替回调函数:

```
const movementsEur = movements.map(mov => mov * usdToEur);
```

除了当前元素之外，`map()`方法还可以访问当前索引和整个数组。

例如，我们可以为每个移动创建一个新的数组，指定移动的位置、值，以及它是存款(`mov > 0`)还是取款(`mov < 0`)。

# 。过滤器( )

顾名思义,`filter()`方法用于过滤原始数组中满足特定条件的元素，这些元素在回调函数中指定。

回到我们的银行变动的例子，假设我们想要创建一个包含所有存款的数组，因此所有的变动都大于 0。只有满足该条件的数组元素才会成为新存款数组的一部分，而其他元素将被过滤掉。

和以前一样，我们可以用箭头函数替换回调函数:

```
const deposits= movements.filter(mov => mov > 0);
```

# 。减少( )

`reduce()`方法用于将数组中的所有元素缩减为一个元素。这种情况的一个例子是将一个数组的所有元素相加。

在我们的示例中，我们可以创建一个函数，通过将存款和取款相加来计算帐户的总余额。

像其他方法一样，`reduce()`函数也获得一个回调函数，但是在这个方法中，第一个参数是一个叫做累加器的东西，而第二个参数是当前元素。

当`reduce()`方法在数组上循环时，它不断将当前元素添加到累加器上，直到循环结束，我们得到所有元素的总和。

值得注意的是，回调函数是`reduce()`方法的第一个参数，它还接受第二个参数，即累加器的初始值，在示例中为 0。

带箭头功能:

```
const balance = movements.reduce((acc, curr) => acc + curr, 0);
```

请在评论中告诉我你将如何使用这三种 JavaScript 方法！

*考虑* [***成为中等成员***](https://ebelinggianmarco.medium.com/membership)**如果你喜欢看这样的故事，并且想帮助我这个作家。每月 5 美元，你可以无限制地访问媒体内容。如果你通过* [***我的链接报名，我会得到一点佣金。***](https://ebelinggianmarco.medium.com/membership)*

**更多内容请看*[*plain English . io*](http://plainenglish.io/)*