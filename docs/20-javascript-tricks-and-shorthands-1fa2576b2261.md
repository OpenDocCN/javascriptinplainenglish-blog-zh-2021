# 20 个 JavaScript 技巧和捷径

> 原文：<https://javascript.plainenglish.io/20-javascript-tricks-and-shorthands-1fa2576b2261?source=collection_archive---------5----------------------->

## 学习这些编写专业 JavaScript 代码的优雅技巧和捷径。

![](img/8d53c0d090ac38a9656e0c263643d830.png)

Photo by [Martin Shreder](https://unsplash.com/@martinshreder?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我为你收集了一系列有用的 JavaScript 技巧，让你的代码看起来更加优雅和专业。我希望你喜欢它！

# 1.一行 If-Else

在 JavaScript 中，可以使用三元条件运算符来压缩 if-else 语句。

例如:

请记住，这种简写是为了使代码更简洁。只有当它清楚地使表达更容易理解时，才使用它。

# 2.零合并

如果左侧为空，则空合并运算符`??`返回右侧。否则，它返回左边的值。这很有用，因为它允许您省略冗长的 if 检查。

零合并的语法是:

```
someValue **??** defaultValue
```

例如:

输出:

```
Nothing found
Nothing found
```

# 3.可选链接

在 JavaScript 中，可以用点符号访问对象的属性和方法。

例如:

```
fruit.color
```

但是如果你试图访问一个未定义对象的属性，你会看到一个错误。为了避免这种情况，您需要确保在访问对象的属性之前定义该对象:

```
**const** color = fruit && fruit.color;
```

但是这个看起来不甜。您可以通过在点符号前添加一个问号来使用可选链接，如下所示:

```
**const** color = fruit?.color;
```

让我们看一个真实 JS 对象的例子:

输出:

```
undefined
undefined
```

# 4.将任何值转换为布尔值

在 JavaScript 中，您可以将任何内容转换为布尔值。这是因为，实际上，JavaScript 中的所有东西要么是“真的”，要么是“假的”。

要将任何东西转换为布尔值，请使用双感叹号`!!`。

例如:

# 5.传播

您可以使用扩展操作符`...`将一个数组的元素扩展到另一个数组中。

例如，让我们使用 spread 运算符将两个数字数组合并在一起:

向数组中添加元素时，也可以用 spread 操作符替换`.push()`方法。

例如:

# 6.使用扩展运算符进行析构

你可以使用扩展操作符`...`来分解一个对象的剩余值。

为了演示，让我们创建一个`student`对象。让我们将`name`和`age`属性赋给变量，将剩余的属性赋给第三个变量:

# 7.从数组中删除重复项

通过将数组转换为集合，然后将集合中的值重新添加到数组中，可以删除数组的重复项。

这是可行的，因为集合是项目的**唯一集合**。

换句话说，一个集合中不能有两个相同的值。因此，将一个数组转换为一个集合会删除隐藏在幕后的重复项。

例如:

```
**const** nums = [1,1,1,1,3,4,5]
**const** uniqueNums = [...**new** Set(nums)];
```

这是做同样事情的另一种方法:

```
**const** nums = [1,1,1,1,3,4,5]
**const** uniqueNums = Array.from(**new** Set(nums))
```

*顺便说一下，如果你需要一系列独特的物品，为什么不用一套呢？*

# 8.短路评估中的&&运算符

你使用 if-checks 来检查一个表达式的值是否为真吗？

您可以使用 short-circuit `&&`操作符进行同样的简化。

例如:

输出:

```
Yeah
Yeah
```

# 9.将值嵌入到字符串中

您可以将一个变量嵌入到一个字符串中，方法是将字符串放在反斜杠内并使用`${}`。

例如:

这些琴弦有时被称为“类固醇琴弦”。

# 10.对象属性分配

如果希望对象键与值同名，可以省略对象文字。

例如:

# 11.默认值

在 JavaScript 中，可以有一个带有默认参数值的函数。

这样，无论是否为参数提供值，您都可以调用该函数。

让我们看一个例子:

# 12.用一行声明变量

您可以将变量声明合并成一行，而不是每个声明使用一行。

例如:

# 13.作为数组的对象值

使用`Object.values()`方法将一个对象的所有值收集到一个数组中。

例如:

# 14.查找数组中的元素

使用内置的`find()`方法来查找符合特定标准的元素。

例如:

# 15.是数组中的一个元素吗？

您可以使用`includes()`方法，而不是使用`indexOf()`方法来检查元素是否在数组中。

例如:

# 16.多重条件检查

使用`includes()`方法避免条件链。

例如:

# 17.用一行代码分配多个值

您可以使用析构在一行代码中分配多个值。

例如:

这也适用于对象:

# 18.交换两个变量，不带第三个变量

使用析构从数组中提取值。这可以应用于交换两个变量而不交换第三个变量。

例如:

# 19.Math.pow()速记

您可以使用`**`操作符作为简写，而不是使用`Math.pow()`函数对数字进行幂运算:

# 20.Math.floor()速记

您可以使用`~~`操作符作为简写，而不是使用`Math.floor()`函数来向下舍入数字:

# 结论

感谢阅读。我希望你喜欢它。

编码快乐！

# 也阅读

[](https://artturi-jalli.medium.com/web-development-buzzwords-in-2021-65f21bc0e1b4) [## 2021 年网络发展流行语

### 学习网页开发人员和网页设计人员的日常语言

artturi-jalli.medium.com](https://artturi-jalli.medium.com/web-development-buzzwords-in-2021-65f21bc0e1b4) [](https://betterprogramming.pub/how-to-transform-javascript-functions-into-memory-efficient-generators-e402af77cdc4) [## 如何将 JavaScript 函数转换成节省内存的生成器

### 开始在 JavaScript 中使用 yield

better 编程. pub](https://betterprogramming.pub/how-to-transform-javascript-functions-into-memory-efficient-generators-e402af77cdc4) [](/closures-in-javascript-made-simple-afb0c7dab5f1) [## JavaScript 中的闭包变得简单

### 理解 JavaScript 中闭包和作用域的简单指南

javascript.plainenglish.io](/closures-in-javascript-made-simple-afb0c7dab5f1) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)