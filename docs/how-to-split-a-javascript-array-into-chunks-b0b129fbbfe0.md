# 如何将一个 JavaScript 数组拆分成块？

> 原文：<https://javascript.plainenglish.io/how-to-split-a-javascript-array-into-chunks-b0b129fbbfe0?source=collection_archive---------16----------------------->

![](img/8c6100b6db50c118ab6b8d3be222f454.png)

Photo by [Eric Welch](https://unsplash.com/@eric_welch?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想在代码中将 JavaScript 数组分成块。

在本文中，我们将研究如何将 JavaScript 数组分割成块。

# 数组.原型.切片

我们可以使用`slice` array 实例方法来提取一个带有开始和结束索引的数组块。

起始索引处的项目包括在内，但结束索引处的项目不包括在内。

例如，我们可以写:

```
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
const chunk = 2;
let tempArray = []
const result = []
for (let i = 0, j = array.length; i < j; i += chunk) {
  tempArray = array.slice(i, i + chunk);
  result.push(tempArray)
}
console.log(result)
```

我们有一个想要分成块的`array`数组。

`chunk`指定每个组块的长度。

`tempArray`有提取的数组块。

我们有一个 for 循环，让我们遍历`array`来提取数据块。

在每次迭代中，我们将`i`增加`chunk`以跳到下一个块的开始。

然后在循环体中，我们用`i`和`i + chunk`调用`slice`来返回每个块。

并且我们用`tempArray`调用`push`将其添加到`result`数组中。

因此，`result`是:

```
[
  [
    1,
    2
  ],
  [
    3,
    4
  ],
  [
    5,
    6
  ],
  [
    7,
    8
  ],
  [
    9,
    10
  ]
]
```

# array . prototype .`concat and` array . prototype . map

我们可以使用`concat` array 方法将一个或多个项目添加到一个数组中。

我们可以使用`map`将原始数组的值映射到数组块中。

例如，我们可以写:

```
const array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
const chunk = 2;
const result = array.map((elem, i) => {
  return i % chunk ? [] : [array.slice(i, i + chunk)];
}).flat()
console.log(result)
```

我们拥有与前一个例子相同的数组和块大小。

然后我们用回调函数调用`array.map`，检查索引`i`是否能被`chunk`整除。

如果是，那么我们用回调函数`slice`返回数组块。

否则，我们返回一个空数组。

然后我们调用`flat`来展平返回的数组，将数组展平一级以得到我们想要的。

由于我们必须遍历整个`array`，这比 for 循环效率低。

所以，`result`应该和我们之前的一样。

# 结论

我们可以用各种 JavaScript 数组方法将一个数组分割成块。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)