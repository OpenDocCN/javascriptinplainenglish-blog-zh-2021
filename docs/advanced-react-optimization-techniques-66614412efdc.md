# 高级反应优化技术

> 原文：<https://javascript.plainenglish.io/advanced-react-optimization-techniques-66614412efdc?source=collection_archive---------0----------------------->

## 以及如何避免常见的陷阱

![](img/032514fe6799bf37418572028161647d.png)

Photo by [Fredy Jacob](https://unsplash.com/@thefredyjacob?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/memory?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

反应非常快。我是说非常非常快。这就是 React 的伟大之处。

但是如果你想进一步优化你的应用程序，有一些方法可以做到。

今天，我们将研究 React 本身提供的解决一些性能问题的最有用的两种技术。

## 1.让我们从简单的开始

举一个例子，我们有一个名为`Display`的组件，它除了显示一行文本之外什么也不做。

这个组件是`Controller`的子组件，它有一个按钮增加一个名为`count`的状态变量，并保存我们的`Display`组件。

The component where unnecessary rendering happens

注意，我们已经在我们的`Display`组件中添加了一个`console.log()`，以确定我们的组件是否正在重新呈现。

现在，当我们点击`Controller`组件的按钮并打开控制台时。

![](img/31d95bd05e49ddaa11f5f8d70b663aac.png)

虽然它与组件的视图无关，但是我们的组件`Display`是`Controller`的子组件，每次我们按下按钮，它都会被重新渲染。

这可不酷。如果我们在整个项目中使用这个`Display`组件会怎么样？

表演会受到影响。

## 2.你问什么是记忆？

记忆化是一种非常常见的技术，在很多地方都有使用。无非就是缓存。

维基百科的定义是

> *在计算中，* ***记忆化*** *或* ***记忆化*** *是一种优化技术，主要用于通过存储昂贵的* [*f*](https://en.wikipedia.org/wiki/Subroutine) *函数调用的结果并在相同的输入再次出现时返回缓存的结果来加速计算机程序。*

那么……如果记忆化是一种提高功能性能的技术，我们能为我们的功能组件做同样的事情吗？

是的，我们能做到。事实上，React 已经为我们提供了一个很好的特性，叫做`React.memo()`

现在我们将看看如何用它来解决我们当前的问题。

## 3.使用 React.memo()防止重新呈现

`React.memo()`需要两个参数。

*   第一个是我们要记忆的函数。
*   第二个是可选的比较功能，就像`shouldComponentUpdate()`一样。我们稍后会打电话给你。

所以现在如果我们把我们的`Display`组件传递到`memo()`中，这应该被记住。

让我们看看会发生什么，如果我们像下面这样重写我们的组件…

Display component with memoization

瞧啊。我们的组件现在不会在我们每次点击按钮时重新呈现。

## 4.让我们更进一步

好了，现在你有了一个有效的组件。但问题是 component 绝对是哑的。你想根据传递给它的一些道具来改变`Display`的内容。

我们现在将重写我们的组件以显示名称列表。

此外，当我们单击按钮时，它会为我们的状态添加一个新名称。

Updated Display Component to Show List of Names

所以每当我们点击`Add Name`按钮时，我们应该会看到`another name`被追加到名字列表中。

但是当我们这样做的时候，什么也没有发生。这是为什么呢？

## 5.可变与不可变

要解决这个问题，我们必须理解`Immutable`的概念。

在`newNames = names`一行中，我们认为我们将`names`赋给了一个新变量`newNames`，但实际上 javascript 中的`arrays`并不是这样工作的！

在后台，这一行所做的就是将`names`数组的引用分配给`newNames`。因此，尽管 names 数组的内容在变化，但引用却没有变化。

React 在这里做的是一个`shallow`检查。它只将 names 数组的前一个引用与新的引用进行比较。因为它没有改变，所以 react 认为没有必要重新渲染。

我们可以这样重写我们的`addNewName`函数来解决这个问题…

updated addName function

这个 spread 操作符返回一个全新的数组，该数组现在被指定为`newNames`。

现在，如果我们单击按钮，我们会看到我们的组件将重新呈现。

## 6.在 memo()失败的地方，useCallback()来拯救

我们再举一个例子。我们将创建一个类似于上一个组件的组件，每次单击按钮时，它都会添加一个新名称。

我们将有另一个组件来清除该列表。

现在，每当我们点击`Add Name`按钮时，我们的`ClearButton`就会一次又一次地重复渲染！

这意味着尽管我们记住了我们的`ClearButton`并且`clearNames`没有改变，但是我们的组件正在不必要地重新渲染。

为了解决这个问题，我们可以使用一个名为`useCallback()`的钩子。这个 useCallBack()钩子帮助我们避免重新计算`clearNames`。它是由 React 本身提供的，所以我们可以像…

```
import ***React***,{ useCallback} from 'react';
```

我们可以如下重写`clearNames`函数来解决我们的问题。

re-written clear name function with useCallback()

现在我们的问题解决了！

因此，这些是您可以用来提高应用程序性能的一些方法。但是每件好事都有它自己的陷阱。所以试着明智地使用这些技术来避免任何不必要的错误。

今天到此为止。编码快乐！

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**

[](/20-essential-parts-of-any-large-scale-react-app-ee4bd35436a0) [## 任何大型 React 应用程序的 20 个基本部分

### 如果您正在编写企业级代码，您需要了解这一点

javascript.plainenglish.io](/20-essential-parts-of-any-large-scale-react-app-ee4bd35436a0) [](https://betterprogramming.pub/the-7-traits-of-a-rock-star-react-developer-747fbb001c05) [## 摇滚明星 React 开发者的 7 个特质

### 造成差异的习惯

better 编程. pub](https://betterprogramming.pub/the-7-traits-of-a-rock-star-react-developer-747fbb001c05)