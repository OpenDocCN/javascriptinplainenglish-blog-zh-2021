# 如何在 JavaScript 中删除对象数组中的重复项？

> 原文：<https://javascript.plainenglish.io/how-to-remove-duplicates-from-an-array-of-objects-in-javascript-71ce1bc96265?source=collection_archive---------4----------------------->

![](img/fba433948cf8c224f9a8f7849a590562.png)

Photo by [Richard T](https://unsplash.com/@newhighmediagroup?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们的 JavaScript 代码中有一组对象，它们有重复的对象。

我们可能希望找到重复的内容并删除它们。

在本文中，我们将研究如何从 JavaScript 数组中移除重复的对象。

# 数组.原型.过滤器

我们可以使用 JavaScript 数组的`filter`方法从数组中删除重复的条目。

为了使用它，我们写:

```
const arr = [{
    place: "san francisco",
    name: "jane"
  },
  {
    place: "san francisco",
    name: "jane"
  },
  {
    place: "new york",
    name: "james"
  }
]
const result = arr.filter((thing, index, self) =>
  index === self.findIndex((t) => (
    t.place === thing.place && t.name === thing.name
  ))
)
console.log(result)
```

`arr`中的第 2 个条目是重复的，我们想删除它。

为此，我们用回调函数调用`arr.filter`来检查该项目的`index`是否与`findIndex`返回的索引相同。

如果它们相同，那么它们就是对象的第一个实例。

`findIndex`接受一个回调，该回调返回我们正在寻找的项目的条件。

回调检查`thing.place`是否与`t.place`相同。

对`name`属性进行同样的检查。

`t`是`arr`数组中的项目。

而`self`如果是`arr`数组。

所以我们遍历`arr`数组来检查这个索引是否是满足给定条件的第一个条目的索引。

结果，我们得到:

```
[
  {
    "place": "san francisco",
    "name": "jane"
  },
  {
    "place": "new york",
    "name": "james"
  }
]
```

从`filter`返回并分配给`result`。

# `Using JSON.stringify`

我们可以使用`JSON.stringify`方法将普通的 JavaScript 对象转换成字符串。

这让我们可以一次检查所有的属性，而不是像上一个例子那样对检查进行硬编码。

例如，我们可以写:

```
const arr = [{
    place: "san francisco",
    name: "jane"
  },
  {
    place: "san francisco",
    name: "jane"
  },
  {
    place: "new york",
    name: "james"
  }
]
const result = arr.filter((thing, index, self) =>
  index === self.findIndex((t) => (
    JSON.stringify(t) === JSON.stringify(thing)
  ))
)
console.log(result)
```

通过使用`JSON.stringify`将`t`和`thing`转换为字符串来删除重复项。

然后我们可以用`===`检查 JSON 字符串指令。

我们得到了和以前一样的结果。

# `Using Sets and JSON.stringify`

JavaScript 附带了`Set`构造函数来让我们创建集合，集合是没有重复项的数据结构。

我们可以用它和`JSON.stringify`一起创建一组字符串化的 JavaScript 对象。

然后我们可以用 spread 操作符将集合转换回数组。

然后我们可以用`JSON.parse`将字符串数组转换回对象数组。

所以我们可以写:

```
const arr = [{
    place: "san francisco",
    name: "jane"
  },
  {
    place: "san francisco",
    name: "jane"
  },
  {
    place: "new york",
    name: "james"
  }
]
const result = [...new Set(arr.map(a => JSON.stringify(a)))].map(a => JSON.parse(a))
console.log(result)
```

来做这个。

我们用以下方式将`arr`条目映射到字符串:

```
arr.map(a => JSON.stringify(a)
```

我们将它传递给`Set`构造函数。

这将删除重复项。

然后我们把它展开成一个数组。

最后，我们调用`map`将字符串化的对象数组映射回带有`JSON.parse`的对象数组。

所以我们得到了和以前一样的结果。

# 结论

我们可以用集合、`filter`或 JSON 方法移除 JavaScript 数组中的重复对象。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)