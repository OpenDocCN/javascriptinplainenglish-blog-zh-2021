# 如何使用 React 片段以及为什么应该使用

> 原文：<https://javascript.plainenglish.io/how-to-use-react-fragments-and-why-you-should-d71a74f61a09?source=collection_archive---------13----------------------->

![](img/54ccaf31efe0f96676ccc6294b1aeaaa.png)

How to use React fragments and why you should!

> React 和 React Native 使用了视图在视图之上的简单思想，这就是 React 片段非常重要的原因。

# 好吧，在我们继续深入之前，你可能已经面临了**臭名昭著的**(是的，**臭名昭著的**)错误警告— **相邻的 JSX 元素必须用封闭标签**包裹起来。这就是 React 碎片派上用场的地方。

但是为什么会出现这个错误，React 片段如何帮助您以有效的方式解决这个问题呢？嗯， **React render 方法期望返回单个节点元素**。

嗯，你可能有过**绝妙的**想法，简单地将所有相邻的 JSX 元素包装在一个 div 或另一个包装器中并返回它们，但是这真的是最好的选择吗？嗯，老实说没有 ***但是*有效**，你可能会说，嗯，有效，*但是*还可以更好。

那么，为什么简单地将任何相邻的 JSX 元素包装在 div 或类似的 HTML 元素中不是一个好主意呢？嗯，它们**增加了 UI** 的额外开销。是的，在 HTML 上添加任何嵌套级别都意味着要花费额外的时间来呈现嵌套的 UI。

## 为什么避免额外的嵌套

为了了解这种无意的嵌套是如何成为一个问题的，我们先来讨论一下 React 本机片段。如果你曾经在 Android 上工作过，你可能会发现嵌套是非常不鼓励的，因为它会降低渲染 UI 的总时间。因此，**安卓**提倡**扁平的用户界面层次**，而不是**高度嵌套的层次**。

一般来说，根据经验，最好在 DOM 树中尽可能少地嵌套。

现在，让我们回到反应原生组件。当您的 React 原生应用程序构建完成后，您的组件，无论是**核心还是原生**，都将被转换到选择的目标平台中(在我们的例子中，我们使用 **Android** )。

现在，我们回到那些额外的**div**上来，这些 div 是你出于好心，为了修正我们之前提到的错误而无意添加的。

当**div**被转换成 **Android 原生视图**时，它们类似于**视图组**是什么。所以，现在你知道这是怎么回事了。你会有一个**工作但 UI 昂贵的代码**带在身边。所有的**div**都将被转换成**视图组**！你会问，如何解决这个问题？

## 你还在这里！

那么，如何解决嵌套问题呢？嗯，**输入 React 片段**！React 片段是 UI 包装器，它使得封装相邻的 JSX 元素成为可能，就像 divs，**一样，但是它的额外好处是没有向 UI 添加节点**！

好了，说了这么多，可以说这个话题已经结束了，但是，还没有，当使用 React 片段或 React 本机片段时，你需要知道一些事情，这取决于你正在构建什么。

## 如何使用 React 片段

让我们看看这段代码:

```
function aLetterToParentDiv() {
    return (
        <div>
            <div>Div, You are awesome</div>
            <div>Always remember that!</div>
        </div>
    )
}
```

嗯，这是对 **parentDiv** 这些年来为你的代码所做的工作的一种感谢。

然而，使用 **React fragments** 我们有两种方法来实现这一点。

第一种方法是反应片段较短的方法，我们有:

```
function aLetterToShorterParentFragment() {
    return (
        <>
            <span>ShorterParentFragment, You are awesome</span>
            <span>But additional support is needed!</span>
        <>
    )
}
```

还有一种更长的方法:

```
function aLetterToLongerParentFragment(itemId) {
    return (
        <React.Fragment> <span>ShorterParentFragment, You are awesome</span>
            <span>But additional support is needed!</span>        </React.Fragment> )
}
```

嗯，较短的方法和较长的方法基本上服务于消除**div**的相同目的，但是较长的方法**起作用。片段**更好，因为它支持 **keys 属性**，这是最重要的 React 和 React 本地组件属性之一！

## 关键外卖！

好了，这就结束了对 React 片段的简短介绍，也应该适用于 React 本地片段。

所以永远记住:

*   Div(以及封装相邻元素的类似方式)向 DOM 树添加了额外的和不必要的节点。这在 React native 中将是一项昂贵的任务。
*   反应片段是封闭相邻 JSX 元素的更好方法。
*   较长的方法比较短的方法好，因为它支持 keys 属性。

## 结论

好了，这就是这篇文章的内容。

直到下一个！

***快乐编码！***

> 你有兴趣学习**反应**吗？类似牛逼的文章在这里结账:[相关文章](https://bingeoncode.com/article/react/How%20to%20use%20react%20fragments%20and%20why%20you%20should%21#related-articles)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)