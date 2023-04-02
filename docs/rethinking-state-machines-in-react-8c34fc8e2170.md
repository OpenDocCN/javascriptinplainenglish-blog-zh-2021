# React 中状态机的再思考

> 原文：<https://javascript.plainenglish.io/rethinking-state-machines-in-react-8c34fc8e2170?source=collection_archive---------11----------------------->

![](img/81185b08b6a739866f85fa8387a780cf.png)

Illustration Credit: [Careerfoundry](https://careerfoundry.com/en/blog/ux-design/what-are-user-flows/)

我认为状态机非常适合前端开发，一年多来，它们一直是我工具箱的一部分。有很多很好的 FSM 实现，比如 [xstate](https://github.com/davidkpiano/xstate) 和 [Robot](https://thisrobot.life/) ，它们可以很好地与 React 应用一起工作，使得复杂的用户流更容易实现。然而，最近我对将它们引入工作流变得更加犹豫，没有足够有力的理由，因为它们似乎用额外的样板文件膨胀了代码，并经常干扰我对接口的推理方式以及它们在用户与应用程序存储/状态的交互中所起的作用。

## 1.错误并不总是全局状态

我发现越来越多的问题是，上述实现中失败的转换会迫使您改变整个机器的状态或上下文。当我们考虑用户界面和用户交互时，一个可纠正的错误不应该导致整个机器进入失败状态。从状态 A 调用转换的组件应该能够报告发生了错误，并列举可以采取的纠正问题的步骤，而不需要整个应用程序在新的失败状态下重新呈现。想象一下服务器端验证阻止了某个更新的发生，但这并不意味着转换是完全不可能的。

转换是将机器从状态 A 转换到状态 b 所需的一系列操作。如果任何操作失败，那么机器可能会保持在相同的状态 A，而不会被迫转换到状态 c。

调用转换的组件知道如何处理错误:它可以选择向用户弹出一条消息，改变它的行为或者将机器转换到不同的状态。在机器内部处理错误会导致失败的去上下文化——无论是改变机器状态还是在机器上下文中存储错误都无法帮助用户在他们正在执行的操作的上下文中处理错误。

## **2。未决转换不应需要中间状态**

与错误类似，正在进行的转换不应该要求状态机改变其状态。挂起的转换要么成功导致新的状态和上下文变化，要么未能将机器保持在具有相同上下文的相同状态，以防止不必要的重新呈现和大量样板文件来说明 UI 中的加载状态。

正在进行的过渡是一种承诺，它应该与悬念和其他异步策略一起很好地工作，以向用户提供反馈。当点击一个按钮开始一个转换时，你想简单地在按钮上显示一个微调器，而不是重新呈现一个新的加载状态，它的框架既不匹配上一个屏幕也不匹配下一个屏幕。

## 3.状态管理不应该成为瓶颈

React 钩子已经提供了高效状态管理和反应所需的一切。使用发布/订阅与 React 组件之外创建的机器进行通信会创建一个新的存储层，需要保持同步。如果您已经在使用状态管理库 a-la 反冲，那么您会感到有点头疼，维护多个不兼容的存储机制。

当每个承诺都被当作可以影响整个机器状态的子机时，将本地状态与服务器同步也变得越来越困难。

## 用本土的解决方案解决问题

所以，我一直在考虑这些问题和想法，并提出了一个精简的状态机实现，没有数学状态机的所有复杂性。让我带你走一遍。

让我们假设我们想要构建一个允许我们向服务器发送消息的应用程序，但是每当我们做出更改时，都会在本地存储中保留一个草稿。

您可以这样理解:当在`writing`状态下执行`send`转换时，调用一系列处理程序，如果都成功，则传播目标状态和上下文。

如您所见，每个处理程序将接收状态机上下文和有效负载作为参数。

让我们创建一个上下文，作为我们机器的真实来源。

现在，让我们创建一个钩子工厂，它将允许我们根据它的名字创建一个转换处理程序。在这个例子中，我使用了`react-async-hook`，但是你可以把它换成你现有应用中已经使用的任何实现。

因此，我们正在创建一个异步处理程序，它将链接我们为转换定义的所有处理程序。在所有处理程序都成功解析之前，状态机上下文不会发生变化。`useAsyncCallback`的结果是一个对象`{ execute, error, loading, result }`。因此，我们可以使用特定的有效负载调用转换处理程序，并对调用它的组件中的错误/加载状态做出反应。

现在，让我们稍微修饰一下我们的状态，以便于访问。

现在，我们可以很容易地访问机器的上下文和状态，使用树中任何组件的一些帮助函数。

让我们也创建一些助手组件。`<Transition>`可用于通过 JSX 过渡机器(类似于 react 路由器的`<Redirect>`)。并且`<State>`将允许我们检查当前状态来决定我们是否应该渲染组件。这将消除我们 JSX 中的条件句。

现在，让我们构建我们的应用程序。

我们的`<ComposerView>`将是一个受控组件，用机器状态作为真理的来源。

最后是显示已发送消息的`<MessageView>`。

## 结论

就是这样。我们现在有了一个基本的状态机，它执行转换时不需要中间状态改变或上下文突变。你可以用定制的钩子来扩展这一点，比如推送或者替换浏览器状态。您还可以轻松地将它与任何其他 React 库和钩子系统集成在一起。您还可以在处理程序中使用钩子，例如访问当前用户的 JWT，以避免无休止地将机器上下文与执行转换所需的所有数据同步。

期待大家的评论。