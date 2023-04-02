# 想写出更好的 JavaScript？你最好知道这些特征

> 原文：<https://javascript.plainenglish.io/want-to-write-better-javascript-a-few-cool-features-to-help-out-54b80eddf85d?source=collection_archive---------14----------------------->

![](img/c914f9a1d2bdd3e565f371164f75fb61.png)

Photo by [Kevin Ku](https://www.pexels.com/@kevin-ku-92347?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/black-farmed-eyeglasses-in-front-of-laptop-computer-577585/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

在 JavaScript 中，我们可以使用一些内置的功能，这将使我们的生活变得更加轻松。从 spread 操作符到 nullish 合并，我想回顾一下我在使用 JavaScript 期间学到的一些更酷的东西。

# **无效合并运算符**

无效合并运算符(`??`)是一种逻辑运算符，当其左侧操作数为`null`或`undefined`时，返回其右侧操作数，否则返回其左侧操作数。这是一种设置默认值的好方法。

Nullish coalescing

# **可选链接**

可选的链接操作符(`**?.**`)使您能够读取一个位于连接对象链深处的属性值，而不必检查链中的每个引用是否有效。这将使我们的代码更整洁，我们可以得到相同的结果，而不用对每个属性进行连锁检查，如果您检查几个级别的值，这可能会变得混乱。

Optional Chaining

# **修剪开始&修剪结束**

trim start 方法将删除字符串开头的任何空白，而 trim end 方法将删除字符串结尾的任何空白。值得注意的是，这不会改变正在执行这些方法的字符串的值。

Trim start and Trim end

# **跨页语法**

当一个对象或数组中的所有元素都需要包含在某种列表中时，可以使用 Spread 语法。例如，如果需要将一个数组中的所有值包含到另一个数组中，可以使用 spread 语法(…)。正如你在下面看到的，我们可以获取数组 cars，并将其传递给`addedCars`，而`addedCars`数组将等于`cars`数组中的内容。

Spread syntax

# 结论

虽然这些只是过去几个迭代中引入的许多新特性中的几个，但我发现这些是我自己最常用的几个。

我希望这篇文章是令人愉快的。如果你有任何反馈，发表评论，让我知道我可以改进的地方。如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于 [Fetch API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) 、 [React](/level-up-your-react-skills-with-the-use-of-composition-766a41f544c9) 、 [TypeScript](https://jgrice01.medium.com/typescript-understanding-the-basics-a2264759cd2d) 、[SASS](https://medium.com/codex/writing-better-sass-with-dynamic-class-generators-e486a0413d0d)&[electronic](https://jgrice01.medium.com/want-to-build-desktop-apps-using-js-say-hello-to-electron-4f862c3b4e38)的文章。感谢您的阅读，祝您愉快！

*更多内容请看*[***plain English . io***](http://plainenglish.io)