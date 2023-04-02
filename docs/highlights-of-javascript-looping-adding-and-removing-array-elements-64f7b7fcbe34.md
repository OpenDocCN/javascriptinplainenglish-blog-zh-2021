# JavaScript 亮点——循环、添加和移除数组元素

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-looping-adding-and-removing-array-elements-64f7b7fcbe34?source=collection_archive---------13----------------------->

![](img/422bcf51585598ef7a51926092203ee8.png)

Photo by [Nick Fewings](https://unsplash.com/@jannerboy62?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 添加和删除元素

我们可以用 JavaScript 轻松地添加和删除数组元素。

要添加元素，我们只需给想要的数组索引赋值。

例如，我们可以写:

```
let animals = [];
animals[0] = "dog";
animals[1] = "cat";
animals[2] = "mouse";
```

我们通过创建一个变量并将其赋给一个空数组来创建`animals`数组。

然后我们给给定的索引`animals`赋值。

我们可以对任何索引这样做，并且索引不必是连续的或有序的。

为了从数组中删除最后一项，我们调用了`pop`方法:

```
animals.pop()
```

向数组添加元素的另一种方法是使用`push`方法:

```
animals.push("fish", "bird");
```

`push`向数组末尾添加元素。

要删除数组的第一个元素，我们可以`shift`:

```
animals.shift();
```

为了在数组的开头再添加一个元素，我们调用`unshift`:

```
animals.shift("fish", "bird");
```

`splice`方法在数组中的任意位置插入一个或多个元素:

```
pets.splice(2, 2, "pig", "duck", "emu");
```

第一个参数是要插入的起始索引。

第二个是要删除的项目数。

随后的参数是我们想要插入的项目，以代替移除的项目。

`slice`方法让我们在任意位置复制一个或多个连续的元素，并将它们放入一个新的数组中。

例如，我们可以写:

```
let pets = animals.slice(2, 4);
```

从`animals`中复制索引 2 到 3 的项目并返回该数组。

第一个参数是起始索引副本。第二个是要复制的结束索引后的 1。

第二个索引本身不包括在范围内。

# 对于循环

JavaScript 提供了循环，所以我们可以重复运行代码。

为此，我们可以使用`for`循环:

```
for (let i = 0; i <= 10; i++) {
  if (city === cleanestCities[i]) {
    console.log("It's one of the cleanest cities");
  }
}
```

`for`循环由标题、继续运行循环的条件和更新索引的语句组成。

在循环体内，我们可以随心所欲。

在上面的例子中，我们检查了`city`是否等于`cleanestCities[i]`。

如果是`true`，我们会在控制台记录一条消息。

循环索引用于访问数组项，也用于将循环移向结束条件，即`i <= 10`。

如果`i`大于 10，则循环停止。

我们还可以在`for`循环中设置标志，以便记录一些信息/

例如，我们可以写:

```
let matchFound = false;
for (let i = 0; i <= 10; i++) {
  if (city === cleanestCities[i]) {
    matchFound = true;
    console.log("It's one of the cleanest cities");
  }
}
```

一旦我们发现来自`cleanesCities`的值等于`city`，我们就将`matchFound`设置为`true`。

# 结论

我们可以用 JavaScript 数组方法添加和删除元素。

同样，我们可以用一个`for`循环遍历数组元素。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**