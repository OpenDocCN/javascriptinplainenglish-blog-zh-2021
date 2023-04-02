# JavaScript 中的运算符优先级和结合性

> 原文：<https://javascript.plainenglish.io/operator-precedence-and-associativity-in-javascript-f55e4b8e6cbc?source=collection_archive---------13----------------------->

## 如果你从未听说过**运算符优先级和结合性，**或者你从未真正理解这个概念，那么这篇文章就是为你而写的！

![](img/fe5cf1d2fdf50c3b6925f54de7b637a1.png)

Photo by [Gabriel Heinzer](https://unsplash.com/@6heinz3r?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/)

在代数中，你们都知道乘法和除法的**比加法和减法的优先级**高。

用表达式 **1 + 2 * 3** ，必须先将 **2 * 3** 相乘，然后将 **1** 加到结果上。

嗯，在 **JavaScript** 中，这个概念也是**有效的，**它被简单地称为**运算符优先级。**

## 例子

*   乘法的优先级为 **13** 。
*   加法的优先级为 **12** 。
*   分组(将表达式放在括号中)具有最高的优先级 (19)。

```
console.log(1 + 2 * 3);
The multiplication is done first, the expression turns into
console.log(1 + 6)
The addition is then evaluated, the result is 7console.log((1 + 2) * 3);
The grouped expression is read first, the expression turns into
console.log(3 * 3)
The multiplication is then evaluated, the result is 9
```

评估的顺序也受**操作符关联性**的影响。

**结合律**是表达式求值的方向:**从右到左**或者**从左到右。**

## 例子

赋值运算符是右关联的，这意味着:

```
a = b = 5
is the same as
a = (b = 5)
```

## 例外

❗分组表达式是**不总是**先读。

如果使用条件评估，**将首先检查条件**，然后评估括号之间的表达式。

```
a || (b * c);
'a' is evaluated **first**, then (b * c) is evaluated if 'a' is **false**a && (b < c);
'a' is evaluated **first**, if 'a' is **true** (b * c) is **evaluated**
```

最初发布在我的[博客](https://blog.ludivineachouri.com/)上。查看我的 [Instagram](https://www.instagram.com/la.dev/) 账号，了解更多关于网络开发的知识。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*