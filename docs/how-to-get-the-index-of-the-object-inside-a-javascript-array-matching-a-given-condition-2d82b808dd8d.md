# 如何获取 JavaScript 数组中匹配给定条件的对象的索引

> 原文：<https://javascript.plainenglish.io/how-to-get-the-index-of-the-object-inside-a-javascript-array-matching-a-given-condition-2d82b808dd8d?source=collection_archive---------16----------------------->

![](img/fdd78ec30d0854d26ba5edfcea99e983.png)

Photo by [Ricky Kharawala](https://unsplash.com/@sweetmangostudios?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们的代码中，我们经常想要从 JavaScript 数组中获取一个匹配给定条件的对象。

在本文中，我们将研究如何在 JavaScript 数组中找到匹配给定条件的对象的索引。

# `Array.prototype.findIndex`

我们可以使用 JavaScript 数组的`findIndex`方法来获取数组中匹配给定条件的对象的索引。

为了使用它，我们写:

```
const arr = [{
    name: 'james'
  },
  {
    name: 'mary'
  },
  {
    name: 'jane'
  }
];const index = arr.findIndex(x => x.name === "jane");
console.log(index);
```

我们用一个回调函数传入了`findIndex`方法，该回调函数找到了`name`属性值为`'jane'`的项目。

因此，`index`应该是 2。

# Lodash 查找索引方法

如果我们在 JavaScript 项目中使用 Lodash，我们也可以使用它的`findIndex`方法在数组中查找匹配给定条件的对象。

例如，我们可以写:

```
const arr = [{
    name: 'james'
  },
  {
    name: 'mary'
  },
  {
    name: 'jane'
  }
];const index = _.findIndex(arr, x => x.name === "jane");
console.log(index);
```

将数组传递给第一个参数，将回调传递给第二个参数。

对于`index`，我们得到了相同的结果。

我们还可以传入一个带有要搜索的属性的对象。

为此，我们写道:

```
const arr = [{
    name: 'james'
  },
  {
    name: 'mary'
  },
  {
    name: 'jane'
  }
];const index = _.findIndex(arr, {
  name: 'jane'
});
console.log(index);
```

我们得到了同样的结果。

# `Array.prototype.map and Array.prototype.indexOf`

在数组中找到满足给定条件的对象的另一种方法是用`map`方法映射我们正在寻找的属性值。

然后我们可以使用`indexOf`来查找给定值的索引，假设该属性保存一个原始值。

例如，我们可以写:

```
const arr = [{
    name: 'james'
  },
  {
    name: 'mary'
  },
  {
    name: 'jane'
  }
];const index = arr.map(a => a.name).indexOf('jane')
console.log(index);
```

我们调用`map`来返回一个 artay，其中包含每个对象的所有`name`属性值。

然后我们可以调用`indexOf`得到我们想要的东西。

因此`index`应该与其他示例相同。

# 结论

我们可以用各种数组方法获得 JavaScript 数组中满足给定属性值的对象的索引。

*更多内容看* [***说白了. io***](http://plainenglish.io)