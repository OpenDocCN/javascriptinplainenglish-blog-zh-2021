# 如何让 TypeScript 函数接受索引类型作为参数

> 原文：<https://javascript.plainenglish.io/how-to-let-a-typescript-function-accept-an-index-type-as-parameter-3cb538ac4175?source=collection_archive---------11----------------------->

## TypeScript 中类型键的完美解决方案

![](img/62060f13713b02b2140d0d5e46901093.png)

Photo by [Maksym Kaharlytskyi](https://unsplash.com/@qwitka?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您得到错误“*元素隐式具有“any”类型，因为类型“string”的表达式不能用于通过 TSLint 或 Visual Studio 代码索引 TypeScript 中的类型*”?这是你的解决方案👍

有时，您希望用一个通用函数从一组键值对中获取特定的属性。但是如何在 TypeScript 中正确地输入呢？

让我们看看这个示例函数。TSLint 不会接受这个。

您将得到类似“*元素隐式具有“any”类型的错误，因为“string”类型的表达式不能用于索引“Vaccination”类型。*”。

给出错误是因为您不能保证`dataProp`参数具有来自`Vaccination`接口的属性。当我们把它保持为一个`string`类型时，当在`Vaccination`接口中没有找到一个属性时，它会给出错误。

这个`Vaccination`界面看起来像这样。

那么如何才能正确解决这个错误，还能像`item[dataProp]`一样使用呢？

超级简单。这里就用`keyof Vaccination`吧。通过`keyof`，我们可以知道我们只接受来自`Vaccination`接口的属性作为函数参数。

> 如果你想更深入地研究 TypeScript，我强烈推荐 Jose Granja 的故事“[掌握 TypeScript 的映射类型](https://betterprogramming.pub/mastering-typescripts-mapped-types-5fa5700385eb)”。

# 结论

[学习基本和高级类型的 TypeScript](https://levelup.gitconnected.com/typescript-for-beginners-97b568d3e110) 将非常有利于防止浏览器中的错误。你喜欢打字稿吗？还是觉得太过了？

*更多内容看* [***说白了***](http://plainenglish.io)