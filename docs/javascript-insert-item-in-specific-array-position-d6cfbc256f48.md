# JavaScript:在特定数组位置插入项目

> 原文：<https://javascript.plainenglish.io/javascript-insert-item-in-specific-array-position-d6cfbc256f48?source=collection_archive---------5----------------------->

您是否在寻找类似于: **array.insert(item，index)** 的内容？如果有，这里有几个回答你的问题！

![](img/2979013e5c108bcbbb1e9e6ff8a5c1d6.png)

# 接合

很多时候我都在想，为什么他们把这种方法叫做“拼接”？当然，这种方法被称为 splice，因为你可以用它做很多事情！您可以使用 splice 插入甚至删除数组中的特定项目。如果你想了解更多关于[如何从数组](https://medium.com/geekculture/how-to-remove-a-specific-item-from-array-46668d873a8e?sk=c413651a5e3fc2872d3ff0ade7a08234)中删除特定物品的信息，点击链接了解更多。

现在，回到我们的故事，如何将一个项目插入到数组中的特定位置。

```
arr.**splice**(index, 0, item);
```

使用上面的语法，您将能够在选择的索引中插入一个给定的项，而不删除任何现有的项。这听起来不像我们正在寻找的吗？我们用一个例子来理解一下:

```
var arr = [];
arr[0] = "A";
arr[1] = "B";
arr[2] = "C";
arr[3] = "D";
arr[4] = "E";

console.log(arr.join()); // A,B,C,D,E
arr.splice(2, 0, "BB");
console.log(arr.join()); // A,B,BB,C,D,E
```

# 拼接并应用

如果您使用的是旧的 **EcmaScript-5** ，您可能需要额外做一步来将一个项目插入到数组中。您将再次使用 Splice。但是，您将使用“应用”功能来实现结果。

```
function insertArrayAt(array, index, arrayToInsert) {
Array.prototype.splice.apply(array, [index,0].concat(arrayToInsert));
}
```

上面的 insertArrayAt 函数接受一个父数组，选择必须插入新数组/项的索引，不删除任何项，但进行插入。

```
//To test the above insertArrayAt
var arr = ["A", "F", "G"];
insertArrayAt(arr, 1, ["B", "C", "D"]);
console.log(arr); //A B C D E F G
```

那么，您何时以及为什么要使用 Splice？

**拼接变异原数组。如果您不希望插入操作改变原始数组，那么您需要遵循一种不同的方法。**

# 薄片

Slice 是数组原型中的一个函数。它可以用来在数组中添加/删除项目，而不改变原始数组。我们如何实现这一目标？作为最小化整个工作的一部分，我在 JavaScript **ES6** 中使用了 spread 操作符。

```
const items = [1, 2, 3, 4, 5]

const insert = (arr, index, newItem) => [
  // part of the array before the specified index
  ...arr.**slice**(0, index),
  // inserted item
  newItem,
  // part of the array after the specified index
  ...arr.**slice**(index)
]

const result = insert(items, 1, 10)

console.log(result)
```

我非常欣赏这种向数组中添加新项的方法，因为您可以修改上面的函数来支持一次插入多个项。

```
const items = [1, 2, 3, 4, 5]

const insert = (arr, index, **...newItems**) => [
  // part of the array before the specified index
  ...arr.**slice**(0, index),
  // inserted items
  **...newItems,**
  // part of the array after the specified index
  ...arr.**slice**(index)
]

const result = insert(items, 1, 10, 20)

console.log(result)
```

通过改变第三个参数[newItems],我们可以 T10 一次添加零个或多个条目 T11 到父数组中，并生成一个新的。这多酷啊？

想单行做？

```
const newArray = [...parentArray.**slice**(0, index), ...insertArray, ...parentArray.**slice**(index)];
```

# **减少**

最后，您可以使用数组原型列表中的另一个方法 **Reduce** ，将一个项目插入数组。

```
const arr = ["A", "C", "D"];const insert = (arr, item, index) =>
  arr.**reduce**(function(s, a, i) {
    i === index ? s.push(item, a) : s.push(a);return s;
  }, []);console.log(insert(arr, "B", 1));
```

解码上述函数:

1.  **s** :表示蓄能器，最初为空
2.  **a** :表示当前数组项
3.  **i** :表示数组项的当前索引
4.  **s.push(item，a)** :如果需要插入该项的索引与“I”匹配，我们将该项和当前项一起推入累加器 s
5.  **s.push(a)** :如果当前索引 I 不等于所需索引，则将当前项 a 推入累加器 s。

**结论**

现在你知道了，如何在数组中添加一个或另一个元素。你可以用**拼接**、**切片**或**缩小**。array prototype 中的三大功能可以帮助您。

如果你喜欢我的话，就照着做，继续学习。JavaScript 总是很有趣！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)