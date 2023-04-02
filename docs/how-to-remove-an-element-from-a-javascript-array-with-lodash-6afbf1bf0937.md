# 如何用 Lodash 从 JavaScript 数组中移除一个元素？

> 原文：<https://javascript.plainenglish.io/how-to-remove-an-element-from-a-javascript-array-with-lodash-6afbf1bf0937?source=collection_archive---------12----------------------->

![](img/fde9c5bd3d3b729d55ee7cb55efe8f31.png)

Photo by [Wolfgang Hasselmann](https://unsplash.com/@wolfgang_hasselmann?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想用 Lodash 从列表中删除一个元素。

在本文中，我们将研究如何使用 Lodash 从 JavaScript 数组中移除元素。

# 使用 remove 方法

从 JavaScript 数组中移除元素的一种方法是使用 Lodash `remove`方法。

例如，我们可以写:

```
const obj = {
  "objectiveDetailId": 285,
  "objectiveId": 29,
  "number": 1,
  "text": "x",
  "subTopics": [{
    "subTopicId": 1,
    "number": 1
  }, {
    "subTopicId": 2,
    "number": 32
  }, {
    "subTopicId": 3,
    "number": 22
  }]
}
const stToDelete = 2;
_.remove(obj.subTopics, {
  subTopicId: stToDelete
});
console.log(obj)
```

在`subTopicId`设置为 2 的情况下删除`obj.subTopics`条目。

为此，我们调用带有`obj.subTopics`属性的`remove`方法作为第一个参数。

我们传入一个对象，该对象包含我们想要从`obj.subTopics`中删除的带有`subTopicId`的条目。

移除操作将在原位完成。

并且移除的项目将被返回。

因此，`obj`现在是:

```
{
  "objectiveDetailId": 285,
  "objectiveId": 29,
  "number": 1,
  "text": "x",
  "subTopics": [
    {
      "subTopicId": 1,
      "number": 1
    },
    {
      "subTopicId": 3,
      "number": 22
    }
  ]
}
```

除了传入一个对象作为`remove`的第二个参数，我们还可以传入一个谓词函数，其中包含我们想要移除的项目的条件。

为此，我们写道:

```
const obj = {
  "objectiveDetailId": 285,
  "objectiveId": 29,
  "number": 1,
  "text": "x",
  "subTopics": [{
    "subTopicId": 1,
    "number": 1
  }, {
    "subTopicId": 2,
    "number": 32
  }, {
    "subTopicId": 3,
    "number": 22
  }]
}
const stToDelete = 2;
_.remove(obj.subTopics, (currentObject) => {
  return currentObject.subTopicId === stToDelete;
});
console.log(obj)
```

我们用同样的第一个参数调用`remove`。

但是第二个参数被替换为一个谓词函数，它返回我们想要删除的对象的条件。

所以我们得到了和上一个例子一样的结果。

# 结论

我们可以用 Lodash 和`remove`方法从一个对象的数组中移除一个元素。

*更多内容请看*[***plain English . io***](http://plainenglish.io)