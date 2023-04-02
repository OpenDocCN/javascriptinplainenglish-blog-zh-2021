# useResponsive:编写自己的 React 钩子来处理响应显示尺寸

> 原文：<https://javascript.plainenglish.io/useresponsive-writing-your-own-react-hook-for-handling-responsive-display-sizes-5fe36cc0c067?source=collection_archive---------4----------------------->

![](img/61c2938a42c0d60c8a94f3cec39eb4f2.png)

Photo by [Christian Kaindl](https://unsplash.com/@christiankaindl?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

虽然大多数响应式设计都是使用 CSS 中的媒体查询来实现的，但通常有些部分必须使用 JavaScript 来实现。

使用 React，这并不总是像看起来那样简单，而且每当调整屏幕大小时，很容易陷入使用太多函数调用的陷阱。

诚然，用户在站点访问期间调整大小是一个比大多数开发人员认为的要少得多的问题，所以这不是一个很大的实际问题，但是我认为使用这个场景是一个很好的机会，可以有效地创建自定义的 React 挂钩。

给出的代码示例将使用 TypeScript，但是因为只使用了相对简单的 TypeScript 特性，所以将其移植到 JavaScript 应该没什么问题。

还要注意，我们假设**屏幕尺寸**和**显示尺寸**在本文中有稍微不同的含义:**屏幕尺寸**将是用户的实际窗口尺寸，而**显示尺寸**指的是一组预先确定的尺寸。**用户的显示尺寸将是最接近其屏幕尺寸的尺寸，向下取整。**

让我们从打基础开始。

## DisplaySize.enum.ts

我们希望有预先确定的显示尺寸设置为灵活的可用性枚举。

我们还手动设置它们的数值，以匹配适用于每个尺寸的最小屏幕宽度。以下是我使用的定义(多年来我发现的共同价值观的组合)，所以请随意使用相同的或定义你自己的。

DisplaySize.enum.ts

## determineddisplaysize . ts

接下来，我们想要一个函数，给定一个特定的屏幕尺寸，它将返回相应的`DisplaySize`。对于这种逻辑，我们认为从一个阈值开始的值直到但不包括该范围内的下一个值。例如，`320`、`380`和`420`的屏幕尺寸都应该被认为是`MobileS`，而`425`应该是`MobileM`。

热切的算法艺术家可能已经知道，对于给定的屏幕尺寸，确定显示尺寸的最有效方法是使用二分搜索法(半间隔搜索)。因为所有的大小都是已知的，所以我冒昧地将整个搜索算法输入如下:

determineDisplaySize.ts

最大深度为 3，最小深度为 2。在变化的`DisplaySize` 定义的情况下，键入一个二分搜索法可能是优先的，只要记住我们是通过至少等于显示大小阈值的值**对节点分类进行分类。**

## 用户响应. ts

好了，终于有人反应过来钩子的动作了！

我们希望钩子传递给使用它的组件的是组件应该适应的当前显示大小。也就是说，组件根本不关心实际的屏幕大小，只关心屏幕显示大小类别。

此外，我们不希望钩子在必要的时候触发重注册。我们将使用`useMemo`来限制钩子的输出，但是，没有办法在每次调整窗口大小时重新计算显示大小。

我们具体实施`useResponsive` 如下:

useResponsive.ts

这是怎么回事？让我们从头开始，一路走来。

首先，我们使用`useState`来跟踪我们已经计算过的当前显示大小，我们从启动挂钩时根据窗口大小立即计算显示大小开始。

到目前为止，逻辑应该相当简单。

然后我们使用`useEffect`做两件事:

1.  在使用我们的钩子挂载任何组件时，我们设置了处理程序和侦听器。我们正在收听窗口大小调整，我们通过用新的计算值更新`currentDisplaySize` 状态字段来作出反应。我们通过使用空数组作为依赖列表来实现装载时的计时。
2.  在卸载时，我们删除事件侦听器。我们通过让它成为`useEffect`返回的一个函数来实现这一点。

换句话说，根据我们上面的定义，我们已经设置了一个保存当前显示大小的值，以及一个在调整窗口大小时自动更新该值的系统。

最后，我们返回用 useMemo 包装的`displaySize`，其`dependencyList`仅由`displaySize`组成。这样，我们确保钩子只在计算出的`displaySize`值实际改变时通知组件，而不会在屏幕尺寸调整没有导致设置新的`DisplaySize`时通知组件。

换句话说，这种挂钩是在任何给定时间确定当前显示大小的一种性能化和反应性实现。

![](img/d12aca7ce3e07277c0ea5da1ee7603cf.png)

Photo by [Charles Deluvio](https://unsplash.com/@charlesdeluvio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 使用

在组件中，我们像大多数其他钩子(不是数组)一样实例化:

```
const displaySize = useResponsive();
```

使用它来确定要返回的内容:

```
if (displaySize < DisplaySize.MobileS) {
  return <div>Size not supported</div>;
}
```

在 JSX 直接使用:

```
<div>
  { displaySize >= DisplaySize.MobileM
    ? <div>BIG TEXT!</div>
    : <div>small text :( </div>
  }
</div>
```

由于我们将枚举值设置为预定的阈值，因此在计算中使用`displaySize`作为数字是没有问题的。

**但要注意的是** `displaySize !== screenSize` **！**

实际屏幕尺寸值始终等于或大于`displaySize`！这是因为我们返回的数字总是立即低于我们的`DisplaySize`列表中的屏幕尺寸。

还可以通过确定当前显示大小是否在两个阈值之间的函数来扩展用法，但是这种用法有点超出了本文的范围。请随意在评论中分享其他巧妙的用法！:)

*更内容于*[T5](http://plainenglish.io/)