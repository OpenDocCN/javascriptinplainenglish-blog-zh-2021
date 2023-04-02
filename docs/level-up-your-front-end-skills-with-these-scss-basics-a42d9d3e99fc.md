# 用这些 SCSS 基础知识提升你的前端技能

> 原文：<https://javascript.plainenglish.io/level-up-your-front-end-skills-with-these-scss-basics-a42d9d3e99fc?source=collection_archive---------17----------------------->

![](img/2864a8ac8144d593d80e968f060f7063.png)

Photo by [Marek Piwnicki](https://www.pexels.com/@marek-piwnicki-3907296?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/cold-glacier-snow-wood-5893003/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

在 web 开发的世界中，我们有很多可以使用的库。从 Tailwind、Bootstrap、Foundation 和许多其他网站，有许多可能的选择。虽然这些都是很好的选择，并且各有利弊，但 SASS 是一个很好的工具，因为它是 web 开发人员应该知道的行业标准。SASS 允许 web 开发人员构建非常灵活和可重用的样式，并且可以与任何前端 CSS 框架配对。

根据我过去几年使用 SASS 的经验，我将花几分钟时间来回顾一下 SASS 提供的一些更有用、更有价值的东西。

# 变量

与 Javascript 非常相似，SASS 也有变量。您可以一次性声明这个变量，然后在所有样式表中使用它。这也非常容易做到。见下文

您可以在创建的任何变量前面添加一个$符号。这告诉 SASS 这是一个变量而不仅仅是一个类。然后，您可以在您创建的任何类中使用它。正如你从上面看到的，我创建了一个字体颜色和一个背景颜色，然后把它传递给正文。

在正常情况下，你会有一个独立的文件来存放你所有的变量。这使得内务处理变得非常容易，而且这对您的开发团队也有好处，因为一切都在一个集中的位置！

# 混合蛋白

创建 mixins 允许我们将过于繁琐的 CSS 块组合成一个可重用的代码块。我们可以创建一个主题 mixin，然后使用@include 关键字在需要的地方使用它，这样我们就不必一遍又一遍地重写相同的代码。这使我们的样式表保持干燥，节省我们的时间和头痛。

# 延长

@extend 在我个人看来是 SASS 最有用的部分之一..这允许我们保持代码干燥，并且在这个过程中会使你的生活变得容易。您可以一次编写一组 CSS 属性，然后在需要的地方反复使用它。您将在我们的主 div 前面看到%符号，这实际上意味着这是一个“占位符”类，只有在用@extend 关键字调用时才会使用。如果我们试图在我们的 HTML 结构中调用“primary-div”类，它将不起作用。

如果你想知道@include 和@extend 之间的区别，我会解释的

> mixin 和 extension 之间的关键区别在于，mixin 用于对多次使用的 css 进行分组，而 extension 用于继承或共享来自完全不同的 css 选择器的属性。当元素几乎相同时，扩展最有用。

# 结论

虽然这只是 SASS 提供的众多功能中的 3 个，但我希望这篇文章能让您愉快。如果你有任何反馈，发表评论，让我知道我可以改进的地方。

如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于 [Regex](/how-to-get-a-better-grasp-on-patterns-with-regex-regular-expressions-an-introduction-9f1be83da76) 、 [Context API](/write-neater-code-by-utilizing-the-react-context-api-an-introduc-ti-a6a450b54e11) 、 [JavaScript](/want-to-write-better-javascript-a-few-cool-features-to-help-out-54b80eddf85d) 、 [Fetch API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) 、 [React](/level-up-your-react-skills-with-the-use-of-composition-766a41f544c9) 、 [TypeScript](https://jgrice01.medium.com/typescript-understanding-the-basics-a2264759cd2d) 、&更多关于 [SASS](https://medium.com/codex/writing-better-sass-with-dynamic-class-generators-e486a0413d0d) 的文章。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)