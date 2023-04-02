# JavaScript 扩展运算符(…) —基本指南

> 原文：<https://javascript.plainenglish.io/javascript-spread-operator-234af4f7554f?source=collection_archive---------16----------------------->

## 什么是传播运算符，如何使用？

![](img/69f3948fc4972dc58f8a195d7f5f93a6.png)

Photo by [Farzad Nazifi](https://unsplash.com/@euwars?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你有没有见过在现代 JavaScript 代码中使用三个点`(…)`,并且想知道它们为什么会在那里或者使用这样一个符号的原因是什么？

如果是的话，你来对地方了。我们将会看到为什么使用这个符号，以及它背后的目的是什么。

# 传播(…)

Spread 在 2015 年被纳入 ECMAScript。首先，它只能操纵数组。它过去只对数组有效。一段时间后，也就是 2018 年，它开始支持对象，这对程序员来说是一个巨大的优势。

传播符字面上有神奇的力量，也就是说，使用它*感觉*神奇。🎩🌟

现在，在不浪费太多时间的情况下，让我们从一个例子开始来正确理解它。仔细评估以下代码片段:

```
const modalProps  = {
  height: 200,
  width: 400,
  backgroundColor: 'white',
  title: 'Sahil More',
  content: 'Learning about spread operator...'
};

showModal(modalProps);

function showModal(**modalProps**) {
  const extraModalProps = {
    modal: true,
    showBackdrop: true,
    height: **modalProps**.height,
    width: **modalProps**.width,
    backgroundColor: **modalProps**.backgroundColor,
    title: **modalProps**.title,
    content: **modalProps**.content
  };
}
```

正如我们所看到的，这段代码用于显示一个模态，在函数`**showModal()**`中，我们可以看到我们必须添加常量`**modalProps**` 的现有属性，以使模态信息更加丰富。

这就是 spread 操作符发挥作用的地方。

```
function showModal(**modalProps**) {
  const windowConfig = {
    modal: true,
    showBackdrop: true,
    **...modalProps**
  };
}
```

与前面的例子相比，这段代码看起来更简洁。👯希望您现在已经理解了扩展运算符的用法。

## **对数组使用扩展运算符**

> **#1:将一个数组添加到另一个数组中**

```
const n1 = [99, 88, 77];
const n2 = [...n1, 66, 55, 44];

console.log(n2); //=> [99, 88, 77, 66, 55, 44]
```

> **#2:合并多个数组**

```
const n1 = [1, 2, 3];
const n2 = [4, 5, 6];
const n3 = [ 7, 8, 9];const combineArr = **[...n1, ...n2, ...n3]**console.log(combineArr); //=> [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

> **#3:将数组展开成对象**

```
const monthsArr = ['January', 'February', 'March', 'April'];
const monthsObj = { ...monthsArr };

console.log(monthsObj); //=> { 0: "January", 1: "February", 2: "March", 3: "April" }
```

这将把数组索引设置为对象值的键。

## 对函数使用扩展运算符

```
const pixel = [10, 25, '#DDD'];

drawPixel(**...pixel**);

function drawPixel(x, y, color) {
  // pixel drawing logic comes here
}
// x => 10
// y => 25 and
// color => '#DDD' 
```

正如我们所见，我们不需要将每个参数单独传递给函数`drawPixel()`。Spread 操作符也减少并简化了代码。

## 对字符串使用扩展运算符

```
const word = "Sahil";
const arrOfChar = [...word];
console.log(arrOfChar); // ["S", "a", "h", "i", "l"]
```

这不是很棒吗？在几秒钟内将任意字符串分割成一个字符列表。💡

# 结论

基本上，扩展操作符是一个非常有用的特性。这是一个巨大的时间节省，因为它减少了代码所需的行数。当处理一个对象或者一个数组时，它会很方便。

我希望你在这里学到了一些新东西。如果你有其他使用 spread 操作符的快捷方式，请在评论中告诉我:)

喜欢文章就分享。🍧别忘了鼓掌，你们知道该怎么做…👏你也可以在这里给我买一杯咖啡。☕️
欢迎在我的[邮箱](mailto:sahilmore19999@gmail.com)里发表任何建议。📪
订阅下面👇在你的邮箱里收到一些很棒的文章。💥

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***