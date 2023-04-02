# JavaScript 中 Array.from()的 5 个用例

> 原文：<https://javascript.plainenglish.io/5-use-cases-for-array-from-in-javascript-a40889115267?source=collection_archive---------3----------------------->

## 通过学习 Array.from()的不同用例来提高您的 JavaScript 知识

![](img/8ccdb3658e7976450db145f1fce5baea.png)

Photo by [rashid khreiss](https://unsplash.com/@rush_intime?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`Array.from()`是一个静态方法，它从具有长度属性的类数组对象和索引元素或可迭代对象(如 JavaScript 中的 Map 和 Set)创建一个新数组。

# 参数是什么？

`Array.from()`方法参数是要转换为数组的类似数组的对象、要对每个项目调用的 map 函数以及在执行 map 函数时使用的 thisArg 值。

## **对象**

这是`Array.from()`方法所必需的。它是一个类似数组的对象，例如具有长度属性和索引元素的对象，可以转换为数组。

## 地图功能

这是一个可选参数。你的`Array.from()`方法里不需要每次都用。但是，您可以将此参数用作映射函数来调用每个数组元素。

## 这个参数

它也是一个可选参数。您可以将这个值用于 map 函数，这是第二个参数。

# 1.从类似数组的对象创建数组

您可以使用`Array.from()`方法从类似数组的对象创建一个数组。例如，你有一个字符串，你想用这个字符串组成一个数组。你可以这样做。

```
Array.from(‘astring’);
// [“a”, “s”, “t”, “r”, “I”, “n”, “g”]
```

您可以从地图创建新阵列。此外，您可以使用`Array.from()`方法为 map 的键和值构造数组。

Gist by [Author](https://medium.com/@onurinanc)

您也可以编写一个函数，将参数作为数组的元素。然后，返回构造的数组。

```
function createArray() {
 return Array.from(arguments);
}createArray(1, 2, 3, 4, 5) // [1, 2, 3, 4, 5]
```

您也可以从用户定义的 iterable 创建数组。

Gist by [Author](https://medium.com/@onurinanc)

# 2.初始化数组

有时，您可能需要用零来初始化数组。使用`Array.from()`方法，可以快速完成。

```
Array.from({length: 5}, x => 0);
// [0, 0, 0, 0, 0]
```

# 3.克隆阵列

JavaScript 中的`slice()`方法可以帮助你创建一个数组的浅层副本。例如，您可以使用不带参数的`slice()`方法克隆一个数组。

```
const updatedGrades = [66, 92, 100, 58, 21, 33];
midtermGrades = updatedGrades.slice();
```

您也可以使用`Array.from()`方法克隆一个数组。

```
const updatedGrades = [66, 92, 100, 58, 21, 33];
const midtermGrades = Array.from(updatedGrades);
```

# 4.查找数组中的唯一项

您可以使用`Array.from()`方法找到数组中的唯一项。为此，您可以将`Array.from()`方法与集合相结合。

```
Array.from(new Set([1, 2, 2, 3, 3, 3, 4, 4, 4, 4]));
// [1, 2, ,3 ,4]
```

# 5.创建您的范围函数

`Array.from()`可以帮助您创建您想要的范围功能。对于类数组对象参数，可以使用类数组`{length:end}`

Gist by [Author](https://medium.com/@onurinanc)

# 结论

JavaScript 中的内置函数对于创建函数是必不可少的。了解内置函数的用例可以提高您的编程技能。您可以快速创建您需要的功能。

`Array.from()`也是一个有用的函数。如果你知道如何使用它，将有利于解决相关问题。

总之，本文中`Array.from()`方法的用例如下:

*   从类似数组的对象创建数组
*   初始化数组
*   克隆阵列
*   查找数组中的唯一项
*   创建您的范围函数，并使用该函数创建英语字母表。