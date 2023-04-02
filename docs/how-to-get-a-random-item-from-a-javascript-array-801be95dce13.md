# 如何从 JavaScript 数组中获取随机项？

> 原文：<https://javascript.plainenglish.io/how-to-get-a-random-item-from-a-javascript-array-801be95dce13?source=collection_archive---------7----------------------->

![](img/b6795cf9ab3d4219f4b651201cf41f62.png)

Photo by [Austin Chan](https://unsplash.com/@austinchan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从 JavaScript 数组中获取一个随机项是我们有时不得不做的操作。

在本文中，我们将研究从 JavaScript 数组中获取随机项的方法。

# 数学.随机

我们可以使用`Math.random`方法从数组中返回一个随机索引。

然后我们可以用它从数组中获取一个元素。

例如，我们可以写:

```
const items = [1, 2, 3]
const item = items[Math.floor(Math.random() * items.length)];
```

由于`Math.random`返回一个介于 0 和 1 之间的数字，我们必须将返回的数字乘以`items.length`来得到一个索引。

此外，我们必须使用`Math.floor`将数字向下舍入到最接近的整数来获得一个索引。

# 洛达什

Lodash 有各种方便的方法可以用来从数组中获取一个随机项。

`sample`方法让我们从一个数组中获得一个随机项。

例如，我们可以写:

```
const items = [1, 2, 3]
const item = _.sample(items);
console.log(item)
```

我们只是把我们想从中获取一个项目的数组作为参数传入。

同样，我们可以使用`random`方法从 0 到给定的数字中选择一个随机数。

例如，我们可以写:

```
const items = [1, 2, 3]
const item = items[_.random(items.length - 1)]
console.log(item)
```

我们只是传入我们想要得到的范围内的最大值。

此外，我们可以打乱整个数组，并从打乱的数组中选取第一个项目。

为此，我们可以使用`shuffle`方法。

例如，我们可以写:

```
const items = [1, 2, 3]
const [item] = _.shuffle(items)
console.log(item)
```

我们用`items`数组调用`shuffle`来返回`items`数组的混洗版本。

然后我们通过析构得到第一项。

# 排序洗牌

我们也可以用`sort`混洗数组。

例如，我们可以写:

```
const items = [1, 2, 3]
const [item] = items.sort(() => 0.5 - Math.random())
console.log(item)
```

通过使用返回-0.5 和 0.5 之间的数字的回调函数调用`sort`来打乱数组。

这让我们可以打乱一个数组，因为当返回的数是正数时，项目被交换。

# 结论

有几种方法可以从 JavaScript 数组中获取随机项。

我们可以使用本地 JavaScript 方法。

或者我们可以使用 Lodash 的方便方法来帮助我们。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)