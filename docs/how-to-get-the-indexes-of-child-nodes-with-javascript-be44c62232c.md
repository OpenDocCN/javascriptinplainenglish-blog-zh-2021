# 如何用 JavaScript 获取子节点的索引？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-indexes-of-child-nodes-with-javascript-be44c62232c?source=collection_archive---------5----------------------->

![](img/58c26478f6ec9dd5b476d131a2c713ec.png)

Photo by [Artur Aldyrkhanov](https://unsplash.com/@aldyrkhanov?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我们想用 JavaScript 获取子节点的索引。

在本文中，我们将研究如何用 JavaScript 获取子节点的索引。

# 使用 Array.from 方法

我们可以使用`Array.from`方法将包含所选元素列表的节点列表对象转换为一个数组。

然后我们可以使用数组来获取元素的索引。

例如，如果我们有下面的 HTML:

```
<div>
  foo
</div>
<div>
  bar
</div>
<div>
  baz
</div>
```

然后，我们可以通过编写以下内容来获得 div 及其索引:

```
const divs = document.querySelectorAll('div')
const arr = Array.from(divs)
for (const [index, div] of arr.entries()) {
  console.log(index, div)
}
```

我们用 div 调用`document.querySelectorAll`。

然后我们用`divs`调用`Array.from`，将节点列表转换为数组。

接下来，使用带有`arr.entries`的 for-of 循环返回一个数组，该数组包含每个 div 的索引数组和 div 对象本身。

`index`有索引，`div`有刻度。

# 使用扩展运算符

将节点列表转换为数组的另一种方法是使用 spread 运算符。

例如，如果我们有下面的 HTML:

```
<div>
  foo
</div>
<div>
  bar
</div>
<div>
  baz
</div>
```

然后我们可以写:

```
const divs = document.querySelectorAll('div')
const arr = [...divs]
for (const [index, div] of arr.entries()) {
  console.log(index, div)
}
```

我们得到了和以前一样的结果。

我们只是用 spread 操作符替换了`Array.from`。

# 结论

为了用 JavaScript 获取子元素的索引，我们将包含所选元素的节点列表转换成一个数组。

*更多内容请看*[***plain English . io***](http://plainenglish.io)