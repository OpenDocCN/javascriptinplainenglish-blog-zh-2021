# 编写更好的 JavaScript 的 5 个技巧

> 原文：<https://javascript.plainenglish.io/5-tips-to-write-better-javascript-31c6da86cc72?source=collection_archive---------7----------------------->

## 成为更好的开发人员的指南

![](img/b8ca16f713f9302b6ab345d319af930d.png)

Photo by [Ben White](https://unsplash.com/@benwhitephotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一个初学者，我们试图让我们的代码先工作，但当我们试图成为一个专业人士，我们应该警惕写干净和有效的代码。编写干净的代码需要大量的实践，这是每个 JavaScript 开发人员都必须掌握的技能。在这篇文章中，我将与你分享一堆帮助你提高 JavaScript 技能的技巧。

# 1.使用 includes()避免多重检查

在 if 条件中使用多个 or(| |)和 and(& &)会使代码看起来非常混乱。所以，尽可能地避免它们。这里有一个场景，我们可以用这个简单的替代方法来提高代码的可读性。您可以很容易地替换它:

```
if (value === 'a' || value === 'b' || value === 'c') { ... }
```

通过这个:

```
if (['a', 'b', 'c'].includes(value)) { ... }
```

当您使用这种替代方法时，代码会变得更加整洁，并且您可以避免在 if 中有太多的条件。

# 2.双`!`操作符将任何变量转换成布尔值

`!` (NOT)运算符可以使用两次`!!`，以便将任何变量转换成布尔型(像布尔函数一样)，它帮助我们在使用之前方便地检查对象的存在。

```
const val = null!!val // false
Boolean(val) // falseif (!!val) { } // val is not null or undefined
```

# 3.可选链接

在`javascript`中，在处理对象之前，你需要经常检查对象的一些属性是否存在。很多开发人员都用这个:

```
const val = { a: { b: { c: 5 } } }if (!!val.a && !!val.a.b && !!val.a.b.c) { ... } // val.a.b.c exist
```

你可以使用**可选链接**来避免使用如上所述的多个检查器。

```
const val = { a: { b: { c: 5 } } }if (!!val.a?.b?.c) { ... } // val.a.b.c exist// If the key doesn't exist, it will return undefined
const test = val.a?.b?.c?.d // undefined
```

查看[这篇](https://betterprogramming.pub/how-optional-chaining-made-my-code-awesome-e9c55ba53da?source=friends_link&sk=43bc79a80a0828bcd5efc0be31db4037)文章，更好地理解可选链接。

[](https://betterprogramming.pub/how-optional-chaining-made-my-code-awesome-e9c55ba53da) [## 可选链接如何让我的代码棒极了

### 访问嵌套属性的安全方式，即使属性不存在

better 编程. pub](https://betterprogramming.pub/how-optional-chaining-made-my-code-awesome-e9c55ba53da) 

# 4.在 if 中返回值时避免使用 else

如果有一个通用的返回语句，最好是在块外返回，而不是在 **else** 中返回。永远记住每一行代码都可能导致问题，所以最好尽可能减少它们。我见过很多次类似的代码片段:

```
if (...) { // the condition is not important in this example
  return 'hello'
} else {
  return 'bye'
}
```

您可以将上面的代码替换为:

```
if (...) { // the condition is not important in this example
  return 'hello'
}return 'bye'
```

# 5.避免 forEach，使用更多的过滤器，映射，减少，每一个和一些功能

使用 forEach 是老一套，有多种替代方法比 forEach 更有效，做的工作也更多。我从这篇文章中得到的最好的建议是，作为初学者，我们使用了很多 forEach 函数，但是 JS 提供了很多选择，而且，这些函数是 FP(函数式编程)。

这些功能是什么？我会给你解释什么时候用！

## 过滤器

顾名思义，它允许我们根据您的条件过滤数组中的一些值。

```
const vals = [1, 2, 3, 4]const evenValue = vals.filter(currentValue => {
   return currentValue % 2 == 0 // remove all value that return false with this condition
}) // [2, 4]
```

## 地图

当您需要将项目中的所有项目转换为另一个项目时，请使用映射，例如，如果您想要转换所有的数字并将它们乘以 2。

```
const vals = [1, 2, 3, 4]const valueMultiplied = vals.map(currentValue => {
   return currentValue * 2 // remove all value that return false with this condition
}) // [2, 4, 6, 8]
```

## 减少

最难理解的是，与其他函数不同，`reduce`还有另外一个东西，`accumulator`。

一个好的规则是知道你是否需要使用`reduce`:

> 你需要从你的数组中得到一个单一的值吗？

例如，如果我想将数组中的所有数字相加为一个值，您将需要`reduce`并且`accumulator`就是总和！和任何值一样，您需要初始化它！

```
const vals = [1, 2, 3, 4]const sum = vals.reduce((accumulator, currentValue) => {
   return accumulator += currentValue // you always need to return the accumulator
}, 0) // 10
```

## 一些&每个

我的最爱之一，我不是每天都用它们，但我喜欢它们！

`some`将检查您的所有项目，当其中一个项目符合您的条件时，它将返回`true`，否则将返回`false`。

`every`将检查您的所有项目，当其中一个项目不符合您的条件时，它将返回`false`，否则它将返回`true`。

但是什么时候用呢？

例如，如果您需要确保您的所有项目都符合条件！

```
const vals = [ 2, 4 ]if (vals.every(val => val % 2 === 0)) { } // You are sure that your array contains only even valueconst valsArr = [ 2, 4, 5 ]valsArr.every(val => val % 2 === 0) // return false since array contain an odd value
```

您可以在相反的上下文中使用`some`，例如，如果您想要确保您的数组至少包含一个奇数值。

```
const vals = [ 2, 4, 5 ]vals.some(val => val % 2 !== 0) // return true
```

# 结论

> 一个好的程序员总是在穿过单行道前向两边看。道格·林德

如果我们努力成为一名优秀的开发人员，我们需要尝试并寻找解决问题的最佳方式，因为任何人都可以解决问题，但我们如何解决问题则完全不同。我真的希望我帮助你理解了一些你已经不知道的东西，这有助于你提高自己。如果你有更多的建议或问题，请在评论中问我。

你喜欢这篇文章吗？下面是我的一些其他文章，可以帮助你掌握 JavaScript:

[](/do-you-write-better-javascript-a75e393d8e09) [## 你写的 JavaScript 更好吗？

### 成为一名注重性能的开发人员

javascript.plainenglish.io](/do-you-write-better-javascript-a75e393d8e09) [](/stop-doing-these-this-in-javascript-fd4be22f7a85) [## 停止在 JavaScript 中做这些

### 成为更好的开发人员的一些技巧

javascript.plainenglish.io](/stop-doing-these-this-in-javascript-fd4be22f7a85) [](/are-you-a-good-front-end-engineer-3b2a3078a4be) [## 你是一个好的前端工程师吗？

### 10 必须具备前端开发人员的特质

javascript.plainenglish.io](/are-you-a-good-front-end-engineer-3b2a3078a4be) [](/5-things-about-javascript-you-might-not-know-938ee465a765) [## 关于 JavaScript 你可能不知道的 5 件事

### JavaScript 思想的食粮

javascript.plainenglish.io](/5-things-about-javascript-you-might-not-know-938ee465a765)