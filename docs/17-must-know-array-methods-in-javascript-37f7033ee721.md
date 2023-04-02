# JavaScript 中 17 个必须知道的数组方法

> 原文：<https://javascript.plainenglish.io/17-must-know-array-methods-in-javascript-37f7033ee721?source=collection_archive---------5----------------------->

## 让您在 JavaScript 中处理数组时更加轻松。

![](img/0b39202c3af67b574d57aba45f4d9e1a.png)

Photo by [Tianyi Ma](https://unsplash.com/@tma?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，数组是一种常用的集合类型，可用于存储数据。有多个有用的内置属性和方法可以让您在使用数组时更加轻松。

今天我将向你展示 17 种有用的数组方法。此外，您还将看到一些简单的示例，展示如何实际使用它们。

我们开始吧！

# 1.Array.find()

使用`.find()`方法找到满足标准的数组的第一个元素。例如，让我们在汽车列表中找到第一辆负担得起的汽车:

输出:

```
{
 brand:"Skoda",
 price:15000
}
```

# 2.Array.concat()

您可以使用`.concat()`方法将两个或多个数组合并在一起。例如:

# 3.Array.findIndex()

使用`.findIndex()`方法获得满足标准的第一个元素的索引。例如，让我们找到列表中的第一个数字`3`:

```
**const** nums = [1,2,3,3,3,2,1]
**const** idx = nums.findIndex( num => num == 3 )console.log(idx)
```

输出:

```
2
```

如果没有符合标准的元素，`.findIndex()`方法返回`-1`。

# 4.Array.forEach()

这个超级有用。它可以让你摆脱常规的 for 循环，这种循环有时可能是合适的。

顾名思义`.forEach()`用于对数组的每个元素执行动作*。例如，让我们打印一个数组的所有数字:*

```
**const** nums = [1, 2, 3];
nums.forEach( num **=>** console.log(num) );
```

输出:

```
1
2
3
```

# 5.Array.join()

您可以使用`.join()`方法连接一个字符串数组来形成一个字符串。

比如让我们把单词合并成一个句子。要组成一个句子，你需要用空格将每个单词分开。这可以通过将一个空格作为参数传递给`.join()`方法来实现:

```
**const** words = ["This", "is", "a test"];
**const** sentence = words.join(" "); // separate words by blank spacesconsole.log(sentence)
```

输出:

```
This is a test
```

# 6.Array.map()

您可以使用`.map()`方法对每个元素执行一个操作(即运行一个函数),并将结果放入一个新的数组中。

例如，让我们将一个数字数组转换为一个新的平方数数组:

```
**const** nums = [1,2,3,4,5];
**const** squaredNums = nums.map( number => number * number );console.log(squaredNums);
```

输出:

```
[1, 4, 9, 16, 25]
```

# 7.Array.reduce()

`.reduce()`方法*通过对数组中的每个元素执行一个函数并累加结果，将*数组缩减为*单值*。

例如，让我们计算数组中数字的总和:

```
**const** nums = [1,2,3,4,5,6];
**const** numSum = nums.reduce((sum, num) => sum + num);console.log(numSum);
```

输出:

```
21
```

让我们检查一下上面的代码，以防你不熟悉 reducing。`.reduce()`方法为您提供了两个值:

*   第一个值是累计的“总”值。在这种情况下，称为`sum`。随着`.reduce()`方法处理这些数字，该值逐渐增加。
*   第二个值是 reduce 操作的当前元素。在这种情况下，它被称为`num`。
*   简而言之，`.reduce()`所做的就是遍历数组的每个元素，并将每个值添加到`sum`中，以获得数字的总和。

注意`.reduce()`可以选择一个初始值。例如，出于某种原因，您可以开始计算来自`1000`的数字的总和:

```
**const** nums = [1,2,3,4,5,6];
**const** numSum = nums.reduce((sum, num) => sum + num, 1000);console.log(numSum);
```

输出:

```
1021
```

# 8.Array.flat()

当你有一个多维数组的时候，你可以用`.flat()`方法把它拉平。例如:

```
**const** nums = [0, 1, 2, [3, 4]];console.log(nums.flat());
```

输出:

```
[0, 1, 2, 3, 4]
```

还可以指定要挤压阵列尺寸的深度。举例来说，让我们将这个 4 维数组展平为 2 维:

```
**const** nums = [0, 1, 2, [[[[3, 4]]]]];console.log(nums.flat(2));
```

输出:

```
[0, 1, 2, [3, 4]]
```

# 9.Array.push()

使用`.push()`方法向数组中添加一个新项目。例如:

输出:

```
[1, 2, 3, 4, 5, 6]
```

# 10.Array.pop()

使用`.pop()`方法移除*并返回*数组的最后一个元素。例如:

```
**let** nums = [1, 2, 3, 4, 5, 6]
**const** lastNum = nums.pop()console.log(`Removed ${lastNum}, now the numbers are ${nums}`)
```

输出:

```
Removed 6, now the numbers are 1,2,3,4,5
```

# 11.Array.shift()

若要移除数组的第一个元素，可以使用。shift()方法。例如:

输出:

```
[2, 3, 4]
1
```

# 12.Array.unshift()

`.unshift()`方法将元素添加到从数组的开始的*中，并返回数组的新长度。例如:*

```
**const** nums = [1, 2, 3];
nums.unshift(4, 5);console.log(nums);
```

输出:

```
[4, 5, 1, 2, 3]
```

# 13.Array.filter()

顾名思义，您可以根据一个标准过滤数组的元素。因此，在过滤元素所在的位置创建了一个新数组。

例如，让我们从数字列表中过滤所有偶数:

```
**const** nums = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
**const** evenNums = nums.filter( num => num % 2 == 0);console.log(evenNums);
```

输出:

```
[2, 4, 6, 8, 10]
```

# 14.数组.排序()

使用`.sort()`方法对字符串数组进行排序:

```
**const** fruits = ["Banana", "Apple", "Clementine"]
**const** sorted = fruits.sort()console.log(sorted)
```

输出:

```
["Apple", "Banana", "Clementine"]
```

注意，你不能仅仅使用`.sort()`对一组数字进行排序！相反，你必须为`.sort()`方法*提供一个比较函数*，这样它就知道如何对数字进行排序。

例如，让我们按升序对数字列表进行排序:

```
**const** nums = [1, 2, 3, 4]
**const** sorted = nums.sort((a, b) => a - b)console.log(sorted)
```

# 15.数组. reverse()

要反转一个数组，你可以简单地使用`.reverse()`方法。举个例子:

```
**const** nums = [1, 2, 3, 4]
**const** reversed = nums.reverse()console.log(reversed)
```

输出:

```
[4, 3, 2, 1]
```

# 16.Array.every()

您可以使用`.every()`方法来检查数组的每个元素是否都通过了一个条件。如果是，该方法返回`true`和`false`如果不是。

例如，让我们检查是否所有的人都饿了:

输出:

```
true
```

# 17.Array.some()

`.some()`方法类似于之前的`.every()`方法。不同之处在于，如果数组中的一个或多个元素满足某个标准，则`.some()`返回`true`，否则返回`false`。

例如，让我们检查是否所有的人都饿了:

输出:

```
true
```

# 结论

*感谢阅读。我希望你今天学到了新东西。*

*快乐编码！*

# 你可能会觉得很有见地

[](https://betterprogramming.pub/25-useful-javascript-shorthands-for-web-developers-771ac550a7ba) [## 25 个对 Web 开发人员有用的 JavaScript 简写

### 学习这些惊人的简笔和一行程序来编写干净快速的代码

better 编程. pub](https://betterprogramming.pub/25-useful-javascript-shorthands-for-web-developers-771ac550a7ba) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)