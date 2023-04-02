# 如何测试冗余连接的 React 组件

> 原文：<https://javascript.plainenglish.io/how-to-test-a-redux-connected-react-component-242d6a58b9be?source=collection_archive---------14----------------------->

![](img/e75ca0fc7dd3c8770b5e3d2e39c5b4af.png)

Photo by [Battlecreek Coffee Roasters](https://unsplash.com/@battlecreekcoffeeroasters?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Redux 是一个处理全局状态的强大库。有人讨厌，有人喜欢。有一件事我可以肯定，如果你在 React 代码库中使用 redux，你会希望对它进行测试。如果你不这样做，它会削弱你自信地发布新特性的能力。在这篇文章中，我将描述一种简单而强大的方法来使用 [React 测试库](https://testing-library.com/docs/react-testing-library/intro/)测试 Redux 连接的 React 组件。

# 演示应用程序

为了设置一些背景，我准备了一个简单的演示应用程序。在代码示例中，我将使用来自`react-redux` lib 的 hooks API，因为这是现在[推荐的方法](https://react-redux.js.org/api/hooks)。

让我们从创建商店开始。这非常简单，它允许添加和删除列表中的项目。

请注意，我正在导出`createApplicationStore`函数。我将在以后的测试中使用它。

该应用程序本身只显示商店中的商品，并允许添加新商品以及删除现有商品。在现实生活中的应用程序中，你可能想把它分成更小的组件，但是为了演示的目的，它会工作得很好。

# 测试

有了所有的设置，让我们考虑测试方法。注意，`App`组件使用`useSelector`和`useDispatch`钩子来集成应用程序商店。这给了我两个选择:

*   嘲笑他们
*   使用`Provider`组件提供商店

我认为嘲笑`useSelector`函数是一个非常糟糕的主意，原因如下:

*   它不测试选择器功能
*   它不测试商店
*   每次一个新的`useSelector`调用被添加到组件测试中时都必须被更新
*   在添加了更多的`useSelector`调用之后，测试将会按照它们被执行的顺序进行

维护这样的测试将是一场噩梦，所以我选择第二种方法。

这个测试很容易阅读，它类似于一个真实的用户与应用程序的交互。

1.  查找新的项目输入
2.  键入一个名称
3.  单击提交按钮
4.  期望项目出现在列表中
5.  单击删除按钮
6.  预计该项目将消失

这个测试与实际的商店交互(注意，我调用了`createApplicationStore`)，所以我只用一个简单的测试就获得了很好的测试覆盖率。此外，测试根本不在乎我使用`useSelector`挂钩，我可以切换到[连接](https://react-redux.js.org/api/connect)特设在它仍然会工作，没有任何变化。

# 摘要

我希望这篇文章对你有用。这里有一些关于测试的更好的资源。如果你喜欢这篇文章，我强烈推荐你去看看。

*   [https://hacks . Mozilla . org/2018/04/testing-strategies-for-react-and-redux/](https://hacks.mozilla.org/2018/04/testing-strategies-for-react-and-redux/)
*   [https://www.youtube.com/watch?v=u5senBJUkPc](https://www.youtube.com/watch?v=u5senBJUkPc)