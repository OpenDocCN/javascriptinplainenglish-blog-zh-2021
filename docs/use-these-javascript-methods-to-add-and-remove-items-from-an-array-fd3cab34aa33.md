# 使用这些 JavaScript 方法在数组中添加和移除项目

> 原文：<https://javascript.plainenglish.io/use-these-javascript-methods-to-add-and-remove-items-from-an-array-fd3cab34aa33?source=collection_archive---------13----------------------->

## 用 JavaScript 在数组中添加和删除项目。

![](img/b618ec758313622b8a13df2159ed4a4b.png)

Photo by J[exo](https://unsplash.com/@jexo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我看来，JavaScript 是一种伟大且易于使用的编程语言。你可以用它创造几乎任何东西，比如网站、手机应用、游戏、人工智能等等。除此之外，它还有很多有用的方法，我们可以用来处理不同的数据类型，比如数组。

在本文中，我们将发现一些 JavaScript 方法来添加和删除数组中的项目。所以让我们开始吧。

# 推送方法

我想每个 JavaScript 初学者都知道方法`push()`。它基本上允许我们在数组的末尾添加一个项目或元素。

方法`push()`接受一个参数，这是我们想要添加到数组末尾的元素。

这里有一个例子:

```
let colors = ["red", "black", "green"];
**colors.push("yellow");**console.log(colors); //["red", "black", "green", "yellow"]
```

如您所见，黄色被添加到数组的末尾。您可以添加任何类型的数据(数字、字符串、对象……)。

# 该方法不移位

方法`unshift()`是一个数组方法，它允许我们在数组的开头添加项目或元素。

这里是使用方法`unshift()`的另一个颜色示例:

```
let colors = ["red", "black", "green"];
colors.**unshift**("yellow");console.log(colors); //["yellow", "red", "black", "green"]
```

所以在上面的例子中，黄色被添加到数组的开头。如您所见，方法`unshift()`接受一个参数(我们想要添加的元素)。

# 方法改变了

方法`shift()`类似于方法`unshift()`，但是它不是在数组的开头添加元素，而是删除数组的第一个元素。

方法`shift()`没有参数。它仅用于删除第一项。

这里有一个例子:

```
let numbers = [1, 2, 3, 4, 5];
numbers.**shift()**; //it returns the removed element(1).console.log(numbers); //prints: [2, 3, 4, 5]
```

如您所见，方法`shift()`也返回移除的元素，在我们的例子中是 1。

# 流行方法

方法`pop()`用于移除数组的最后一个元素。它不接受参数，返回被删除的元素。

下面是一个例子:

```
let numbers = [1, 2, 3, 4, 5];
numbers.**pop()**; //returns the removed element(5).console.log(numbers); //Prints: [1, 2, 3, 4]
```

我想你现在清楚了。如果你想删除一个数组的最后一个元素，只需使用方法`pop()`。

# 使用拼接添加和移除

与上述方法不同，方法`splice()`在我看来更有用。它允许你在任何你想要的索引上添加或删除数组元素。

方法`splice()`有三个参数:

*   index(必选):这是您需要指定的第一个参数。这是你想要添加和删除元素的数组索引。
*   number(可选):要删除的元素数量。
*   Items(可选):这是第三个参数，您可以在其中写入要添加到数组中的所有元素。

下面是一个使用所有三个参数的示例:

```
let names = ["John", "Alex", "Anna"];
names.**splice(1, 0, "James", "Mehdi")**;console.log(names); //["John", "James", "Mehdi", "Alex", "Anna"]
```

正如你在上面的 names 数组中看到的，我们使用了方法`splice()`并给了它三个参数。在索引 1 处，我们删除了 0 个元素，并添加了姓名詹姆斯和迈赫迪。就这么简单。

在第三个参数中，您可以指定想要添加的任意多个项目。如果愿意，我们也可以选择只使用第一个参数或前两个参数。

下面是一个仅使用一个参数的示例:

```
let names = ["John", "Alex", "Anna"];
names.**splice(2)**;console.log(names); //["John", "Alex"]
```

在上面的例子中，我们只使用了一个参数。我们将其设置为 2，这意味着我们只需要数组的前两个元素。如果要从最后一个元素开始到第一个元素(反方向)，也可以给负数。

# 长度法

数组方法`length`给出了一个数组的长度。但是我们也可以用它来调整数组的大小和移除数组元素。

下面的数组包含 5 个数字(5 个项目)。我们可以将长度设置为数字 2，以删除除前两项之外的所有数组项。

下面是一个例子:

```
let numbers = [66, 55, 34, 90, 9];
**numbers.length = 2;**console.log(numbers); //prints: [66, 55]
```

正如你所看到的，当我们将长度调整为 2 时，我们只得到前 2 项，所有其他项都被删除。所以这也是一种去除元素的方法，但是用处不大。我推荐拼接法。

# 结论

上述方法允许我们在 JavaScript 中添加和删除数组中的项目。每个 JavaScript 开发人员都应该知道这些，因为您总是会遇到需要使用它们的情况。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读**

[](/best-javascript-es2019-methods-that-you-should-know-380cf370c5) [## 你应该知道的最好的 JavaScript ES2019 方法

### 通过示例了解一些有用的 ES2019 方法。

javascript.plainenglish.io](/best-javascript-es2019-methods-that-you-should-know-380cf370c5) [](/5-useful-website-cheatsheets-for-all-web-developers-70290340385) [## 对所有网站开发者有用的 5 个网站备忘单

### 面向所有网站开发者的超赞网站备忘单。

javascript.plainenglish.io](/5-useful-website-cheatsheets-for-all-web-developers-70290340385) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)