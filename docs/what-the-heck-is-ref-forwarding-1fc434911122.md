# Ref 转发是什么鬼东西？

> 原文：<https://javascript.plainenglish.io/what-the-heck-is-ref-forwarding-1fc434911122?source=collection_archive---------2----------------------->

## 理解反应

## 将引用传递给子组件

![](img/00664fe7936fe0f72ce2697bcd9f5d1f.png)

Image by [Nina Garman](https://pixabay.com/users/billithecat-7996303/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=4070337) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=4070337)

与 React 框架的其他部分相比，refs 肯定有点古怪。React 利用声明式设计模式，不鼓励直接操作`DOM`，但是对于一些用例——例如聚焦或选择输入字段——直接的命令式代码是必要的。这就是引用的用武之地，它允许我们访问一个节点，并根据需要强制性地修改它。

*(* ***先不说*** *:如果你之前没有 React 参考经验我推荐你先阅读* [*这篇文章*](/whats-a-ref-anyway-2a6979ad173f) *再继续)*

# (不完整的)例子

首先，让我们研究一个引用转发可能会派上用场的场景。下面我们有漂亮的文本输入，还有一个按钮，单击它可以选择输入的值。不幸的是，下面的例子坏了。

( ***先不说数字二:*** *尽管我尽了最大的努力 CodeSandBox 和/或 Medium 似乎有意默认向您显示* `*App*` *文件。请务必查看* `*FancyInput.js*` *文件，了解不同实现之间的差异*

A broken implementation :(

如果我们更新我们的`FancyInput`组件并尝试通过`props`访问 ref 会怎么样？这次我们将在实际的`input`元素上声明一个`ref`属性，并尝试通过`props.ref`从父组件传递`ref`。

This doesn’t work either :(

又坏了？怎么回事？

让我们来看看控制台输出:

```
Warning: FancyInput: `ref` is not a prop. Trying to access it will result in `undefined` being returned. If you need to access the same value within the child component, you should pass it as a different prop. ([https://reactjs.org/link/special-props](https://reactjs.org/link/special-props))
    at FancyInput ([https://54gtm.csb.app/src/FancyInput.js:24:41](https://54gtm.csb.app/src/FancyInput.js:24:41))
    at div
    at App ([https://54gtm.csb.app/src/App.js:26:38](https://54gtm.csb.app/src/App.js:26:38))Warning: Function components cannot be given refs. Attempts to access this ref will fail. Did you mean to use React.forwardRef()?

Check the render method of `App`.
    at FancyInput ([https://54gtm.csb.app/src/FancyInput.js:24:41](https://54gtm.csb.app/src/FancyInput.js:24:41))
    at div
    at App ([https://54gtm.csb.app/src/App.js:26:38](https://54gtm.csb.app/src/App.js:26:38))
```

从错误消息中可以看出，试图通过 props 将 ref 传递给子组件是行不通的。谢天谢地，我们得到了使用`React.forwardRef()`的有用建议。

## 检查文档

如果我们按照第一个警告中提供的[链接](https://reactjs.org/warnings/special-props.html)，我们会看到`ref`是 React 内部使用的特殊属性/关键字，这意味着**任何作为** `**ref**` **传递给元素的值都不能通过** `**props**`访问。作为`key`属性传递的任何值也是如此。

> JSX 元素上的大多数属性都被传递给组件，但是，有两个特殊的属性(`ref`和`key`)被 React 使用，因此不会被转发给组件。—特殊道具警告

换句话说，React 在内部利用`ref`和`key`属性，防止它们所属的组件通过`props.ref`或`props.key`访问这些值。

> 如果您需要在子组件中访问相同的值，那么您应该将它作为一个不同的属性来传递(例如:`*<ListItemWrapper key={result.id} id={result.id} />*`)。虽然这看起来有些多余，但将应用程序逻辑与协调提示分开是很重要的。— [特殊道具警告](https://reactjs.org/warnings/special-props.html)

这是否意味着我们可以通过给子组件一个不同的名字来传递一个`ref`给它？嗯，是也不是。虽然*是*可能的，但是将一个引用作为一个值传递给一个唯一的属性被认为是不好的做法。这是为什么呢？

# 不恰当的解决方法

无论何时设计软件，记住 [***低耦合和高内聚***](https://medium.com/codex/low-coupling-and-high-cohesion-af77df4cc005) 的原则是很重要的。你的程序应该保持一个适当的关注点分离 : *父组件不应该需要对它们的子组件的结构有深入的了解，它们的子组件也不应该需要对父组件有全面的了解才能正常工作。*

Do not do this

虽然上面的代码有效，但它导致了紧密耦合的组件，充其量也就是模糊的内聚性，这与良好的设计实践完全相反。当您第一次创建`FancyInput`组件时，可能很容易记住使用`innerRef`，但是如果该组件在您的应用程序中被重用了呢？如果您决定在未来的项目中回收该组件，该怎么办？当不同的开发人员在一年或更长时间后进行维护时会发生什么？

当我看着这些代码时，我所能想到的就是那些不幸维护、更新或以其他方式与这些代码库进行交互的人将来会遇到的所有麻烦。不太好。

# 首选解决方案:React.forwardRef()

谢天谢地，React devs 已经为我们的问题提供了一个解决方案。通过将我们的功能组件包装在`React.forwardRef()`中，我们可以传递第二个参数`ref`，此外还有`props`，它可以在子组件中以任何必要的方式使用。

This is the correct way

通过将`FancyInput`包装在`React.forwardRef()`中，我们可以获取从父组件传递来的`ref`并在内部使用它。这将两个文件解耦，有效地分离了关注点，使我们的代码更加模块化。我们的父组件现在可以强制性地修改其子组件，而不需要详细了解子组件的内部`DOM`结构。

# 类别组件

React 文档声明*“您也可以将引用转发给类组件实例。”*但遗憾的是没有提供任何示例代码。在仔细阅读了 StackOverflow 之后，我找到了一个可行的解决方案。

诀窍是在导出语句期间**在** `**React.forwardRef()**` **中包装你的类的一个实例。`React.forwardRef()`接受一个回调函数并传递给它两个参数，`props`和`ref`。您可以编写一个快速助手函数来接收这两个参数，并将`ref`传递给唯一的`prop`(在本例中为`innerRef`)。**

Forwarding refs using class components

虽然类似于前一个(坏的)例子，但是这个策略与*的不同之处在于父组件不需要知道任何关于子组件内部结构的事情*。使用这种方法，从父类的角度来看，类或功能组件之间没有区别，这是一件好事。

为什么父组件应该关心子组件是类还是函数？这在抽象层次上有必要吗？也许有一些边缘情况需要这种信息，但是一般来说，子节点是函数还是类*应该*与父节点中发生的逻辑无关。低耦合，高内聚。

# TL；速度三角形定位法(dead reckoning)

*   您不能像传递其他值一样将`ref`传递给子组件(即通过普通的旧`props`
*   要将一个`ref`传递给一个子组件(要*转发*它)，必须将子组件包装在`React.forwardRef()`中
*   `React.forwardRef()`接收一个函数作为参数，并提供两个参数`props`和一个`ref`
*   功能组件可以直接接收这些参数，并在需要时使用它们
*   类组件需要一个助手函数，将`ref`映射到一个唯一的`prop`，允许类在内部使用它。

你以前在自己的项目中使用过转发引用吗？你在哪里见过它们，用于什么目的？欢迎在下面的评论中分享你的个人经历。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)