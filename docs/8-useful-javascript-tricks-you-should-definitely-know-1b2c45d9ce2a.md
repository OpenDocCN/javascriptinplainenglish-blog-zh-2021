# 你绝对应该知道的 8 个有用的 JavaScript 技巧

> 原文：<https://javascript.plainenglish.io/8-useful-javascript-tricks-you-should-definitely-know-1b2c45d9ce2a?source=collection_archive---------11----------------------->

## 你可能没见过这些

![](img/43de0a01db01a576b4a1e32f1b9f9144.png)

Photo by [Timothy Dykes](https://unsplash.com/@timothycdykes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我收集了一些 JavaScript 技巧，我相信这些技巧可以让你成为更好的 JavaScript 开发人员。排名不分先后，下面给你八个 JavaScript 窍门！

# 1.交换两个变量

JavaScript 中有一个交换两个变量的单行程序，如下所示:

```
let first = 'hello', last = 'bye';
[first, last] = [last, first];
// first = 'bye', last = 'hello'
```

上面的代码创建了一个[last，first]数组，并立即将它们析构为相反的变量。

所以再也不需要临时变量了！

# 2.移除数组重复项

您不必遍历数组，使用映射，然后创建一个具有唯一值的数组。ES6 中引入的 **Set** 对象类型允许您存储唯一值。与扩展运算符(`...`)一起，您可以使用它来创建一个没有重复值的新数组:

```
const uniqueArray = [...new Set(array)]
```

我们从数组中创建一个集合，因为集合中的每个值都必须是唯一的。然后，我们使用 spread 操作符将集合转换回一个新的数组。

# 3.转换为数字

将值转换成数字，尤其是将字符串转换成数字，是一个常见的需求，并且有许多转换方法。

## 一元+运算符

将字符串类型转换为数字的最简单方法是一元`+`运算符:

```
+"13"  // 13
```

一元加号运算符位于其操作数之前，对其操作数求值，但如果它还不是数字，则尝试将其转换为数字。这里还有几个例子可以说明它是如何工作的:

```
+true  // 1
+false // 0
+null  // 0
```

## 数字

[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number) 是 JavaScript 中用于表示和操作数字的原始包装器对象。当用作函数时，`Number(value)`将字符串或其他值转换为数字类型。如果值不能转换，则返回`NaN`(不是数字)。

```
Number('13')   // 13
Number('1.3')  // 1.3
Number('haha')  // NaN
```

## parseInt

`[parseInt()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseInt)`将一个字符串作为第一个参数和该字符串要转换到的基底。这个方法总是返回一个整数。

```
parseInt('1331', 10)       // 1331
parseInt('8 balls', 10) // 8
parseInt('ballnumber 8', 10)   // NaN
parseInt('13.31', 10)      // 13
```

`parseInt()`试图从一个不仅仅包含数字的字符串中得到一个数字，但是如果这个字符串不是以数字开头，你将得到`NaN`。

## parseFloat

如果我们想保留小数部分，而不仅仅是整数部分，我们可以使用`[parseFloat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)`,它接受一个字符串作为参数并返回等价的浮点数。如果数字不包含小数位，那么它只返回整数值。

```
parseFloat('10.42') // 10.42
parseFloat('10.00') // 10
```

# 4.区间中的随机数

通常当我们需要在一定范围内产生一个随机数时，我们可以使用`Math.random()`。这个函数帮助我们在指定的范围内生成一个随机数。

```
const randomIntFromInterval = (min, max) => Math.floor(Math.random() * (max - min + 1) + min);
```

# 5.轻松管理对象

**析构**是 ES6 的重要组成部分，你可能会经常用到。它允许我们从对象中提取数据，并将提取的数据分配到变量中:

```
const rectangle = { h: 200, w: 400 };
const { h, w } = rectangle;
```

如果需要，我们可以重命名变量，如下所示:

```
const { h: height, w: width} = rectangle;
console.log(height); // 200
```

我们可以做的另一件事是通过一个函数来析构返回的对象，并选择我们想要使用的值:

```
function getPerson() {
  return {
    firstName: 'Harsha',
    lastName: 'Vardhan',
    age: 25
  }
}const { age } = getPerson();
console.log(age); // 25
```

因此，通过析构，我们可以通过返回一个对象并选择需要返回的内容来从一个函数中返回多个值。

以一种不可变的方式移除一个属性需要 spread 的对应方提供的一个小技巧，即 **rest** 操作符，它由三个点(`…`)组成，类似于 **spread** 。然而，在这种情况下，我们将剩余的属性扩展到一个新的对象中。

```
const { age , ...person } = getPerson();console.log(person); // {firstName: "Harsha", lastName: "Vardhan"}
```

现在，`person`对象保存了除了`age`之外的来自原始人物对象的所有属性。

# 6.对象中的动态属性名

ES6 给我们带来了计算属性名，允许对象的属性使用表达式。通过用方括号[]将键括起来，我们可以将变量用作属性:

```
const type = "fruit";
const item = {
  [type]: "apple"
};console.log(item); // {fruit: "apple"}
```

这在您希望动态创建密钥的情况下非常有用。

我们可以用括号符号来访问该值:

```
item[type];   // "apple"
```

# 7.设置默认值以避免错误

大多数初学者都有检查值是否存在的习惯，只有当值存在时才执行操作，当值不存在时返回`null`或其他任何东西。在 JS 中，你不需要这样做，因为有另一个概念，你可以提供默认值。下面是我们如何在 JS 中设置默认值:

## 变量

[**无效合并运算符** (](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) `[??](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)` [)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator) 是一种逻辑运算符，当其左侧操作数为`null`或`undefined`时，返回其右侧操作数，否则返回其左侧操作数。我们可以用它来设置默认值，例如，当我们收到一个尚未设置为数组的列表时:

```
const players = playingEleven ?? [];
```

## 因素

我们可以使用零合并操作符来设置函数中变量的默认值，但是有一种更好的方法- [**默认参数**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) :

```
function calculateArea(width, height = 100) {
    return width * height;
}const area = calculateArea(20);
console.log(area); // 2000
```

这里，我们将`height`的默认值设置为 100，并通过只发送`width`来计算面积。

## 目标

析构对象的另一个技巧是设置默认值:

```
const rectangle = { height: 400 };
const { height = 600, width = 500 } = rectangle;
console.log(height); // 400 - comes from rectangle object
console.log(width);  // 500 - fallback to default
```

ES6 析构默认值仅在值为`undefined`时适用。

# 8.将项目添加到数组中而不发生变化

我们经常想要在没有变化的情况下向数组中添加一个新项，我们可以使用 ES6 [spread 操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)和 [slice](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) 操作符创建一个新数组。

```
onst insert = (arr, index, newItem) => [
  ...arr.slice(0, index), // first half of array
  newItem,                // new item
  ...arr.slice(index)     // rest of array
];

const items = ['H', 'E', 'L', 'O']

const result = insert(items, 2, 'L');

console.log(result); // ["H", "E", "L", "L", "O"]
```

# 结论

这是我想与你分享的一些技巧和诀窍。我希望你能找到一些有用的，值得加入你的日常武器库的东西。如果你喜欢阅读更多类似的技巧，我推荐你在这里关注我，也可以点击下面的链接，在这里 [**实用程序员**](https://medium.com/pragmatic-programmers/table-of-contents-2e70a70c27df) 有一本关于简化 JavaScript 的书在 Medium 上出版。感谢您的阅读！

# 进一步阅读

 [## 目录

medium.com](https://medium.com/pragmatic-programmers/table-of-contents-2e70a70c27df) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)