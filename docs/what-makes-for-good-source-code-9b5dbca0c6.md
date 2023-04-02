# 什么是好的源代码？

> 原文：<https://javascript.plainenglish.io/what-makes-for-good-source-code-9b5dbca0c6?source=collection_archive---------16----------------------->

## 这里没有单一的答案，但我会提供六个指标。

![](img/2890cf8234e9cfcfb318463bd052be50.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

源代码是应用程序的 DNA。当你在一个网站或软件的引擎盖下寻找时，你可以找到任何东西和一切。有时候是丛林，有时候一切都精致整洁。

作为一名程序员，我可以说这个问题没有唯一的答案。因此，我会给你一些我认为有助于制作好源代码的要点。让我们开始吧。

# **1。清晰的架构**

甚至在查看源代码之前，文件和目录的技术架构就表明了代码是否是定性的。一个好的分解，比如 MVC，使得在文件中很容易找到自己，并分离应用逻辑:数据恢复、控制、管理规则、数据呈现。

在业务层面，项目的分解同样重要。因此，使用模块、插件或包(取决于框架)的概念来分组类似的功能概念通常是有用的。

# **2。有文档记录的源代码**

phpDoc 和行内注释在源代码质量中起着核心作用。评论是我首先检查的指标之一，以获得整体质量的概述。评论时的座右铭:不多也不少。如果太多，代码就会淹没在不必要的信息中；如果太少，我们就不理解它在应用程序中的作用及其逻辑。

一些人认为清晰的代码不需要注释，因为它是可读的。对我来说，这是一个错误。在写的时候是可读的。但是，即使是简单的代码，当它被修改、重构或用于最初不一定想要的目的时，也会变得晦涩难懂。因此，我的建议是明智地、充分地进行注释，以便以后再回过头来看，而不必完全重读源代码。

# **3。共享功能**

高质量的源代码是不重复的代码。在整个开发过程中，开发人员必须考虑代码的分解。代码是整个团队的共同利益，冲突不可避免地会发生，必须通过以下三种方式尽快解决:

*   实施项目，绘制组件图；
*   开发团队成员之间的良好沟通；
*   定期代码审查。

为了避免这种重复，没有什么灵丹妙药:你必须重构。我们可以在一开始就想到一个简单清晰的架构，但是一个 IT 项目并不是固定的。需求可能会发展，随之而来的代码也会发展。

# **4。一个所有人都能理解的源代码**

理解代码有两个方面:源代码的可读性和清晰的分解。首先，源代码是一个易于阅读和理解的文本。文档起着重要的作用，但不是唯一的。源代码的格式也是需要考虑的一个因素。理解一个适当通风的代码比理解一堆线更容易。

# **5。不重复发明轮子的代码**

开发人员系统地重新开发相同的功能有什么意义？路由、用户管理、数据恢复，许多库为您完成了这些工作。插上就行了。因此，在我看来，高质量的代码需要使用一个框架，或者至少是一个带有第三方组件的标准 MVC 类型的架构。

注意，第三方组件的使用是一把双刃剑。正如一个经过验证和维护的库提供了许多服务一样，您不应该被一个不能保证其功能、对扩展的开放性和维护的库所束缚。在这种情况下，如果一个库对您来说很方便，那么好的做法是授予 fork 特权。

# **6。一个单元测试源代码**

最后，好的源代码的最后一个指标是自动化单元测试的覆盖率。尽管它们不能保证代码没有错误或者代码满足需求，但是 Tuas 提供了第一层控制。在选择库时，总是倾向于包含单元测试的库。在开发时，我总是喜欢添加单元测试。

当你说一个好的源代码时，它意味着使一个网站或软件工作的一切。所以不能只看一面，要整体看。我希望这六点能让你更好地理解什么是好的源代码。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)