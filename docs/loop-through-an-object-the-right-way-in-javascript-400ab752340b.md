# 如何在 JavaScript 中遍历对象

> 原文：<https://javascript.plainenglish.io/loop-through-an-object-the-right-way-in-javascript-400ab752340b?source=collection_archive---------14----------------------->

![](img/d41d1ff9454721d5ef2da5a45b240d04.png)

Photo by [Markus Spiske](https://www.pexels.com/@markusspiske) on [Pexels](https://www.pexels.com)

## 利用 Object.entries 的力量

我知道你可能在想什么，对于如此看似微不足道的事情来说, *right* 意味着什么？出于本文的目的， *right* 被定义为当您的代码需求不可避免地发生变化时，以一种既能产生一致性又能最小化代码重构的方式处理问题。此外，我希望您通过更清楚地陈述其意图，了解为什么这种方法可以产生更清晰、更易于理解的代码。

# 对象.条目

Object.entries 是一种方法，它采用可以是对象或数组的参数，并返回一个数组，该数组包含分别位于索引 0 和 1 处的每个键值对的数组。

Object.entries demo

# 填补对象.条目

在我们开始之前，重要的是要注意，预测到使用旧的“过时”浏览器的人将会使用你的站点是一个好习惯。本文大量使用了 ECMAScript 2017 (ES8)中引入的 Object.entries。如果你是在 Angular 这样的现代框架中开发，它可能已经为 Object.entries 添加了一个 shim。如果不是，请随意将下面的代码复制并粘贴到你的项目中，以允许旧浏览器使用这种方法运行你的应用程序。

Object.entries shim

# 回拨方法

使用回调来循环具有可读性优势，但是我们失去了使用*继续*和*中断*来跳过或停止循环完成的能力。

Instantiate our vehicles dictionary and loop through it

回调方法允许我们更清楚地陈述我们的意图，尤其是考虑到我们可能需要在遍历数组之前转换或操作数组。例如，假设我们只想在这个对象中循环通过本田制造的车辆，我们可以很容易地做到这一点

Remove vehicles that aren’t made by Honda, and remove entries where they have no vehicles, then loop through the results

# For-of 循环

例如，我们可能希望使用 *continue* 和 or *break* ，我们可以对 Object.entries 使用简单的 For 循环

# 结论

使用 Object.entries 允许我们轻松地迭代对象和数组中的键值对，而不必担心必须调用*object . hasownproperty(property name)*来确保我们不会意外地迭代对象原型链中的属性，而不是 for-in 循环。

在 JavaScript 中应该避免 for-in，因为它们既迭代对象原型中的属性，也偶尔不按顺序迭代。Object.entries 没有这样的限制，并且足够灵活，在我们需要迭代的任何时候都很有用。