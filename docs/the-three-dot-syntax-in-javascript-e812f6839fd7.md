# 如何在 JavaScript 中使用扩展运算符(…)

> 原文：<https://javascript.plainenglish.io/the-three-dot-syntax-in-javascript-e812f6839fd7?source=collection_archive---------17----------------------->

*JavaScript 中的“…”语法有什么作用？我来解释一下(用代码片段)。*

![](img/8ed73a422643515e37d665428894664d.png)

Photo by [Mike Szczepanski](https://unsplash.com/@youngprodigy3?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/three-dots?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

根据 [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals) 的说法，JavaScript 中的三点符号已经被添加到 ECMAScript 2018 的提案中。它的正式名称是**扩展操作符**或**扩展语法**。它到底是做什么的？

> 它允许在需要零个或多个参数(用于函数调用)或元素(用于数组文字)的地方扩展可迭代对象，如数组表达式或字符串。
> - [Mozilla](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)

# 怎么用？

它的工作原理是将数组的所有元素“分散”到你输入的任何地方。这可能是一个新数组、一个函数调用或者一个新对象的创建者。

**它的用途之一是在不改变原始数组的情况下扩展数组。**这是通过将扩展操作符应用于新数组的创建来完成的。

不是添加`arr`作为子数组，而是将它的元素分散到新数组中。**这也可以在函数调用中完成，或者在从类创建新对象时完成。**

它是对 JavaScript 的一个小小的补充，取代了像`concat`这样的函数，使得处理数组更加优雅。它做不了很多你用小的变通办法已经做不了的事情。

然而，由于它非常优雅，现在很多 JavaScript 教程都以它为特色。尤其是在 React 或类似的库领域，它们使用相当多的数组。

# 结论

应该使用扩展运算符吗？是的，如果你想的话。它是一个伟大而优雅的运营商，拥有来自浏览器的巨大支持。**如果使用 Node.js，5.0.0 版**支持数组文字和函数调用，8.3.0 版支持对象创建。Node 的 8.3.0 版本已经在 2017 年 10 月发布，所以很有可能你会很好地使用它。

我希望这篇文章清楚地说明了如何使用 spread 操作符。非常感谢您的阅读，祝您度过美好的一天。

*更多内容尽在* [***说白了***](http://plainenglish.io/)