# 利用 React 上下文 API 编写更整洁的代码——简介

> 原文：<https://javascript.plainenglish.io/write-neater-code-by-utilizing-the-react-context-api-an-introduc-ti-a6a450b54e11?source=collection_archive---------14----------------------->

![](img/efa0e2eb7ea7ee9b5de89443f9b3a188.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们如何处理数据是至关重要的，React 开发团队想到了一些处理数据的方法。从更新组件的状态，到给组件分配道具，我们有两种可靠的方法来处理这个问题。

但是，如果我们不想对数据进行过于复杂的管理，只想将值传递到需要的地方，而不是进行适当的处理，该怎么办呢？进入上下文 API！

> 上下文提供了一种通过组件树传递数据的方式，而不必在每一层手动向下传递属性。—反应堆文件

context 旨在防止的主要事情是正确的钻探。Prop drilling 是通过将数据值传递到各个层，从组件 A 到组件 Z 获取数据值的过程。因此，如果组件 D 需要一个`value`属性，你必须从组件 A 向下钻至组件 B，然后从组件 B 钻至组件 C，最后从组件 C 钻至组件 D。

如果您使用过 React，您可能对这个概念很熟悉。这可能会变得过于复杂，如果我们不小心的话，就会变成杂乱的代码，React 开发团队通过引入上下文 API 使我们的生活变得简单。

**如何使用上下文 API**

要设置上下文，就像使用`React.createContext()`一样简单。

Creation of context is easy

让我们假设您需要创建各种主题。虽然有十几种方法可以做到这一点，但我们将使用上下文来处理这一点。为此，我们将设置背景颜色和字体颜色。

Our context file for themes

接下来，我们想要实际使用我们新创建的上下文。为此，我们将使用基于类的组件。在我们的渲染方法中，我们将把`this.props`和`this.context`分配给它们各自的变量。然后，我们将返回基于`ourThemes`的样式的`<button />`，这是我们在外部创建并导入的。

The usage of our context file

**提供要消费的值**

一个更实用的方法如下。我们设置我们的功能，并将逻辑限制在它需要做的事情上。在提供者中，我们提供的是消费者将消费的价值。简而言之，我们“提供”了“点击我”的价值，然后我们“消费”了按钮中的价值。

虽然这是两个可能的用例，但是 [React 文档](https://reactjs.org/docs/context.html#contextprovider)给出了大量我们可以使用的其他例子。至于何时使用上下文 API，react 文档说

> **Context** 主要用于不同嵌套层次的许多组件需要访问某些数据的时候。请谨慎使用它，因为它使组件重用更加困难。如果你只想避免通过许多关卡传递一些道具，组件组合通常是比**上下文**更简单的解决方案。—反应堆文件

我希望这篇文章是令人愉快的。如果你有任何反馈，发表评论，让我知道我可以改进的地方。

如果你想看看我的其他帖子，可以在这里找到。我写的都是前端特有的东西，所以我有关于 [JavaScript](/want-to-write-better-javascript-a-few-cool-features-to-help-out-54b80eddf85d) ， [Fetch API](https://avetwhocodes.com/fetching-data-from-an-api-with-the-fetch-api-in-react-5dbe0abcfb41) ， [React](/level-up-your-react-skills-with-the-use-of-composition-766a41f544c9) ， [TypeScript](https://jgrice01.medium.com/typescript-understanding-the-basics-a2264759cd2d) ，[SASS](https://medium.com/codex/writing-better-sass-with-dynamic-class-generators-e486a0413d0d)&[electronic](https://jgrice01.medium.com/want-to-build-desktop-apps-using-js-say-hello-to-electron-4f862c3b4e38)的文章。

*感谢您的阅读，祝您愉快！*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)