# 如何检查 JavaScript 对象数组中是否存在对象值，如果不存在，如何向数组中添加一个新对象？

> 原文：<https://javascript.plainenglish.io/how-to-check-if-an-object-value-exists-within-a-javascript-object-array-and-if-not-add-a-new-2e87e7053335?source=collection_archive---------17----------------------->

![](img/47d11f648cde1e60397eadaaee44b7a3.png)

Photo by [Sam Moqadam](https://unsplash.com/@itssammoqadam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望检查 JavaScript 对象数组中是否存在对象值，如果不存在，就在数组中添加一个新对象。

在本文中，我们将看看如何检查一个对象值是否存在于一个数组中，如果不存在，插入一个新的条目。

# 使用 Array.prototype.some 方法

我们可以使用`some` JavaScript 方法来检查 JavaScript 数组中是否存在给定条件的条目。

我们可以使用`push`方法向数组中添加一个新条目。

要使用它来检查具有给定条件的条目是否存在，并在条目不存在时添加条目，我们可以编写:

```
const arr = [{
  id: 1,
  username: 'fred'
}, {
  id: 2,
  username: 'bob'
}, {
  id: 3,
  username: 'ted'
}];const add = (arr, name) => {
  const {
    length
  } = arr;
  const id = length + 1;
  const found = arr.some(el => el.username === name);
  if (!found) {
    arr.push({
      id,
      username: name
    });
  }
  return [...arr];
}const newArr1 = add(arr, 'ted')
const newArr2 = add(arr, 'james')
console.log(newArr1);
console.log(newArr2);
```

我们有一个`arr`数组，我们想检查带有给定`username`的条目是否存在，如果不存在，就添加一个带有给定`username`的新条目。

为此，我们创建了`add`函数，该函数使用`arr`数组进行检查，使用`name`进行查找。

在函数中，我们获取`arr`的`length`，并将`id`设置为`length + 1`。

然后我们用回调函数调用`arr.some`,返回`el`数组条目是否满足条件`el.username === name`,并将结果赋给`found`

如果`found`为`false`，则意味着`username`等于`name`的条目不存在。

因此我们用一个新条目调用`arr.push`，给定的`name`作为`username`。

然后我们返回一个`arr`的副本来确保我们没有修改原来的`arr`数组。

因此，`newArr1`是:

```
[
  {
    "id": 1,
    "username": "fred"
  },
  {
    "id": 2,
    "username": "bob"
  },
  {
    "id": 3,
    "username": "ted"
  }
]
```

而`newArr2`是:

```
[
  {
    "id": 1,
    "username": "fred"
  },
  {
    "id": 2,
    "username": "bob"
  },
  {
    "id": 3,
    "username": "ted"
  },
  {
    "id": 4,
    "username": "james"
  }
]
```

# 结论

我们可以使用`some` JavaScript 方法来检查 JavaScript 数组中是否存在给定条件的条目。

我们可以使用`push`方法向数组中添加一个新条目。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)