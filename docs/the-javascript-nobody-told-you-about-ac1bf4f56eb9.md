# 没人告诉你的 JavaScript

> 原文：<https://javascript.plainenglish.io/the-javascript-nobody-told-you-about-ac1bf4f56eb9?source=collection_archive---------1----------------------->

![](img/57d63a4124edfcb4962ec4fd2d37801f.png)

我在大学生活的大部分时间里都在使用 JVM 语言，比如 Java 和 Kotlin。具有讽刺意味的是，我大学毕业后的第一份工作是 ReactJS 开发人员。过去 4 年我害怕和逃避的语言现在就在我面前。我害怕 JavaScript 的原因主要是因为你也在这里。不容易理解为什么它会以这种方式工作。

差不多一年半过去了，我现在感觉更自信了，希望你在读完这篇文章后也会如此。在这里，我指出了一些我敢肯定你从未想过 JavaScript 中存在的秘密。

## 虚伪的价值观

`undefined`、`null`、`0`、`false`、`NaN`、`‘’`都是假值。你可能已经知道了，但是你知道空字符串也是假的吗？

见下文。

```
console.log('' == false); // true
console.log('' === false); // false
```

## 滤波函数

您一定在数组上经常使用 **filter** 函数。如果你想过滤数组中的虚假值，这里有一个提示。只需在过滤函数内部提供**布尔**。

```
const arr = [1,4,undefined,null,9,NaN,10,''];
console.log(arr.filter(**Boolean**)); // [1,4,9,10]
```

## 排序功能

你对 JavaScript 中的**排序**函数了解多少？它对数组进行排序，对吗？不完全是。

```
const arr = [1,2,20,10,8];
arr.sort(); // [1, 10, 2, 20, 8]
arr.sort((a,b) => a-b); //[1,2,8,10,20]
```

上面第 2 行的输出看起来不像一个排序的数组。为什么？这是因为当我们调用不带参数的 sort 方法时，JavaScript **会将数组的元素转换成 string** 然后按字母顺序排序。疯狂？我知道。

## 交换

很多时候，我有一个交换数组中两个元素或两个变量的用例。我曾经为此写过一个实用函数，但这里有一个 JavaScript 的方法。

```
**Inside arrays** let arr = [1,2,3,4,5];
[arr[4],arr[0]] = [arr[0],arr[4]];
console.log(arr); //[5,2,3,4,1]**Just two variables** let a = 10, b = 20;
[a,b] = [b,a];
console.log(a,b); // 20 10
```

这就是 JavaScript 中**析构**的威力。虽然我使用析构很长时间了，但从来没有这样想过。

## 微调功能

在许多编程语言中，我们在字符串上有一个 **trim** 方法来删除字符串中的任何空白。但是使用 JavaScript trim 并不能删除字符串中的所有空格。见下文。

```
" shivam bhasin  ".trim(); // "shivam bhasin"
"shivam bhasin".trim(); // "shivam bhasin"
```

它**从你的字符串中移除所有的前导和尾随空格**，但不是全部。这让我很困惑，因为我在 Java 中使用过字符串。

## 推送功能

我在代码中大量使用了 push 方法。虽然我最近才知道我们也可以使用 push 来合并数组。

```
const a = [1,2];
const b = [3,4];
a.push(b); // [1,2,[3,4]] **not merged**
Array.prototype.push.apply(a,b); // [1,2,3,4] **merged**
```

在上面的第 4 行中，合并后的数组将在**变量 a** 中。

## isNaN 函数

`isNaN`也是 JavaScript 中最常用的方法之一。它检查给定的参数是否是一个数字。但是对于空字符串和填充字符串，它的行为是不同的。见下文。

```
isNaN(1); // false
isNaN(""); // false
isNaN("a"); // true
isNaN("1"); // false
```

你可能很清楚第 1 行，1 是一个数字，因此它返回 false。但是在第 2 行，JavaScript 将空字符串**视为 0，**是一个数字，因此没有通过 NaN 测试。第 3 行也应该清楚，因为“a”是一个字符串，因此不是一个数字。同样，在第 4 行“1”是一个字符串，但是 JavaScript 在内部**将其解析为数字 1** ，因此它没有通过 NaN 测试。很奇怪，对吧？了解这一点后，我开始在将参数传递给`isNaN`函数之前对它们使用`parseInt()`。

## 对象的动态关键点

有时我不得不根据 API 响应或某种计算给我的对象分配动态键。我们可以这样做。

```
const a = "age";
const b = {
     name: 'shivam',
     [a]: 22, // this will become **age: 22** at runtime
};
```

## 拼接和切片

差不多 3 个月后，我意识到`slice`和`splice`是 JavaScript 中不同的方法。Lol 我知道。以下是它们的不同表现。

```
**slice(s,e);** Here s is the starting index and end is the end index of the new array which will be a sub-array of the original array. **Note that the original array will not be changed when using slice.****splice(i,n);** Here i denotes the starting index and n denotes the number of items to be removed starting from index i. **Note that splice will alter the original array.**
```

## 浮点数

这几乎是难以置信的，但和我呆在一起。浮点数的加法在 JavaScript 中表现得非常怪异。见下文。

```
console.log(0.1+0.2 === 0.3); // false
```

这是因为`0.1+0.2`给出的`0.30000000000000004`不等于`0.3`。还有，

```
console.log(9007199254740992 + 1); // 9007199254740992  
console.log(9007199254740992 + 2); // 9007199254740994
```

这看起来很奇怪，直到我知道根据 IEEE 754 标准，所有的 JavaScript 数字都是用 64 位二进制内部表示的浮点数。你可以在这里阅读更多相关信息[。](https://2ality.com/2012/04/number-encoding.html)

## 运算符的类型

`typeOf`是一个一元运算符，返回一个表示变量原始类型的字符串。我们知道 JavaScript 大部分是对象，所以在大多数情况下，这会返回`object`。这里有几个奇怪的例外。

```
typeOf NaN; // 'number'
```

`typeOf` NaN 是一个看起来很奇怪的数字，但是`NaN`在技术上是一个数字数据类型。但是，它是一种数值数据类型，其值不能用实际数字表示。见下文。

```
const nan1 = 2*'a'; // NaN
const nan2 = 4*'b'; // NaN
nan1 === nan2; // false
```

在上面的例子中，`nan1`和`nan2`都不相等，这意味着它们拥有一些值。只是价值不能用数字来表示，所以它们是 NaN。看到另一个异常，

```
typeOf null; // 'object'
```

如果你在这里成功了，那就太棒了。大多数人在这之前就结束了。但是你对它了解得越多，你就越能意识到这个世界头号编程语言是如何工作的。

这是给你的临别赠言。

## 原始操作>方法

如果你想让你的代码更快，那么试着使用原始操作而不是方法调用。尽可能使用 VanillaJS，它会让你的代码在运行时更快。见下文。

```
const min = Math.min(a,b); // slow
const min = a<b? a: b; // fastarr.push(x); // slow
arr[arr.length] = x; // fast
```

希望你今天学到了新东西。在下面写下你已经知道了多少。此外，如果你认为有什么东西应该在这个列表上，请发表评论。

让你内心的极客赢吧！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)