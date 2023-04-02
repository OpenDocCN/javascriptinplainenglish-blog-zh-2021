# 可以在 JavaScript 字符串和数组上使用的方法

> 原文：<https://javascript.plainenglish.io/javascript-methods-you-can-use-on-both-strings-and-arrays-3b40f4962285?source=collection_archive---------1----------------------->

## 您知道 JavaScript 字符串和数组上都可以使用一些方法吗？让我们来看看这些方法，看看它们之间的异同！

![](img/c8ccfc489fa60e8ba36837475655c8ad.png)

Photo by [Caspar Camille Rubin](https://unsplash.com/@casparrubin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

虽然不可能知道 JavaScript 中的每一个方法，但是知道有一些方法可以用于多种数据类型也很好。

具体到字符串和数组，这些方法有`concat`、`indexOf`、`slice`。在本文中，我们将了解这些方法是什么，如何使用它们，以及在字符串和数组上使用它们的异同。

# `**concat**` **:合并(无损)**

对于调用它的各个数据类型(字符串或数组)，该方法用于合并两个或多个数据类型，返回一个新版本而不改变原始版本。更具体地说，返回的对象包含它所调用的字符串/数组的所有元素，对于每个参数，依次是参数的元素或参数本身。特别是对于数组，如果一个参数是一个嵌套数组，它不会取出嵌套数组，而只是将它从它所在的数组中移除(一级深度)。否则，对于字符串，如果参数不属于字符串类型，则在连接之前会将其转换为字符串值。

**趣闻**:对于数组，`concat`将原数组的对象引用复制到新数组中，这样原数组和新数组都引用同一个对象！因此，如果修改了被引用的对象，新数组和原始数组都可以看到这些更改。但是，对于字符串，对原始字符串或返回字符串的更改不会影响其他字符串。

**性能说明**:具体到字符串，强烈建议使用赋值运算符(+、+=)，而不是`concat`方法。

```
// no nested arrays
const array1 = ['a', 'b', 'c']
const array2 = ['d', 'e', 'f']
const array3 = [‘g’, ‘h’, ‘i’]
const array 4 = array1.concat(array2, array3)console.log(array4)
// ["a", "b", "c", "d", "e", "f", "g", "h", "i"]// nested array
const array1 = ['a', 'b', 'c']
const array2 = ['d', 'e', 'f', [‘g’, ‘h’, ‘i’]]
const array3 = array1.concat(array2)console.log(array3)
// ["a", "b", "c", "d", "e", "f", ["g", "h", “i”]]// strings
const str1 = 'Hello'
const str2 = 'World'console.log(str1.concat(' ', str2))
// "Hello World"console.log(str2.concat(', ', str1))
// "World, Hello"
```

# **indexOf:查找项目的索引(非破坏性)**

对于数组和字符串，`indexOf`检查每个元素是否与指定值相等，并返回第一个匹配的索引。但是，如果您要搜索的元素不存在，则返回-1。

`indexOf`接受要搜索的`searchValue`的一个参数，也可以选择开始搜索的索引。对于字符串，`searchValue`是要搜索的字符串值，如果没有提供值，将默认搜索`undefined`。另一方面，对于数组来说，`searchValue`只是要搜索的元素。

如果包含索引的第二个参数来开始搜索，并且索引大于或等于数组/字符串的长度，则返回-1，这意味着不会搜索该对象。但是，如果第二个参数是负的，数组/字符串仍然是从前到后搜索的。

```
// arrays
const animals = ['turtle', 'bison', 'horse', 'duck', 'bison']console.log(animals.indexOf('bison')) // 1
console.log(animals.indexOf('giraffe')) // -1
console.log(animals.indexOf('bison', 2)) // 4 b/c starts from index 2// strings
const paragraph = 'The quick brown fox jumps over the lazy dog. If the dog barked, was it really lazy?'const searchTerm = 'dog'
const indexOfFirst = paragraph.indexOf(searchTerm)console.log(`The index of the first "${searchTerm}" from the beginning is ${indexOfFirst}`);
// "The index of the first "dog" from the beginning is 40"console.log(`The index of the 2nd "${searchTerm}" is ${paragraph.indexOf(searchTerm, (indexOfFirst + 1))}`)
// "The index of the 2nd "dog" is 52"
```

# **切片:复制(非破坏性)**

如果你只是想复制一个数组或字符串，你不需要传入任何参数。也就是说，您可以选择包含要复制的起始索引(包含)和结束索引(不包含)。这种方法经常在`splice`上使用，因为它避免了变异原件的“副作用”。

如果您没有传入任何参数，默认情况下将复制整个原件。如果任一索引为负，它从结尾或最后一个元素开始提取(方法`length`—index)。另一方面，如果传入的参数大于实际数组(例如，一个包含 5 个元素的数组/字符串，但传入的参数从 10 开始，到 50 结束)，返回值将为空。

```
// arrays
let iceCream = [“vanilla”, “chocolate”, “strawberry”, “green tea”]let startIndex = 1
let endIndex = 2let copyOfIceCream = iceCream.slice(startIndex, endIndex)console.log(copyOfIceCream) // ["chocolate"]
console.log(iceCream) // ["vanilla", "chocolate", "strawberry", "green tea"]// only chocolate is in the new array because endIndex is non-inclusive! If the endIndex was 3 instead, we would have a return ["chocolate", "strawberry"]// strings
const str = 'The quick brown fox jumps over the lazy dog.'console.log(str.slice(31)) // "the lazy dog."
console.log(str.slice(4, 19)) // "quick brown fox"
console.log(str.slice(-4)) // "dog."
console.log(str.slice(-9, -5)) // "lazy"
```

# **结论**

总而言之，有三种非破坏性的方法可以用在字符串和数组上:

*   `concat`，合并两个字符串/数组
*   `indexOf`，根据搜索值查找项目的索引
*   `slice`，复制字符串/数组

也就是说，尽管可以在字符串上使用`concat`,但建议使用赋值操作符来完成同样的操作，知道这一点很重要。

非常感谢您的阅读！如果您对更多的字符串方法感兴趣，请查看 Megan Lo 的“[在 JavaScript 中何时使用这些字符串方法](https://dev.to/mehmehmehlol/when-to-use-these-string-methods-in-javascript-3m4h)”。你也可以看看我的帖子，“[一切 JavaScript 数组&数组方法！](https://waverley-place.medium.com/everything-javascript-arrays-array-methods-5e5809ffa4ad)”了解 JavaScript 数组和数组方法的更多信息。

# 想要更多吗？查看其他资源！

## 数组:

📖[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/Array](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array)
📖[https://Waverley-place . medium . com/everything-JavaScript-arrays-array-methods-5e 5809 FFA 4 ad](https://waverley-place.medium.com/everything-javascript-arrays-array-methods-5e5809ffa4ad)

## 字符串:

📖[https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Global _ Objects/String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
📖[https://dev . to/mehmehmehlol/when-to-use-these-string-methods-in-JavaScript-3m4h](https://dev.to/mehmehmehlol/when-to-use-these-string-methods-in-javascript-3m4h)

[*更多内容尽在 plainenglish.io*](http://plainenglish.io/)