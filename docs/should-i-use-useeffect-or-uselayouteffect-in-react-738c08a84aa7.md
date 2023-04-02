# React 中应该用 useEffect 还是 useLayoutEffect？

> 原文：<https://javascript.plainenglish.io/should-i-use-useeffect-or-uselayouteffect-in-react-738c08a84aa7?source=collection_archive---------3----------------------->

## 理解这些 React 挂钩之间的核心区别

![](img/db90611542d66c51242d45a00f1ecc0b.png)

Photo by [Jason Strull](https://unsplash.com/@jasonstrull?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都必须熟悉使用 React 钩子。但是你有没有想过什么时候应该使用`useEffect`钩和`useLayoutEffect`钩？在本文中，我将解释这些钩子的正确用法的用例。

实际上，这两个钩子基本上做同样的事情，但是它们的用例略有不同。但是在讨论这些差异之前，让我们先了解一些术语。

*   **Render** —表示计算每个 DOM 节点的样式。
*   **画图** —表示在屏幕上显示/更新内容。

# 使用效果

大多数时候，你可能想使用`useEffect`钩。每当你重构你的类组件来使用钩子时，你可能会将任何代码从`componentDidMount`、`componentDidUpdate`或`componentWillUnmount`移到`useEffect`。

这在 React 渲染你的组件后运行，确保你的效果回调**不会阻塞**浏览器绘画。这与类组件中的行为不同，类组件中的`componentDidMount`和`componentDidUpdate`在渲染后同步运行。这样更有性能，这可能是你最想要的钩子。

# useLayoutEffect

`useLayoutEffect`在 React 执行完所有 DOM 突变后，立即同步运行**。如果您需要进行 **DOM 测量**(如果您要获取元素的滚动位置或其他样式)，然后进行 DOM 突变或通过更新状态触发同步重新呈现，这可能会很有用。**

**这与`componentDidMount`和`componentDidUpdate`的工作方式相同。DOM 更新后，您的代码会立即运行，但在浏览器有机会绘制这些更改之前(我们实际上直到浏览器重新绘制后才会看到更新)。**

# **独特的例外情况**

**当使用`ref`时，如果你想在任何其他代码运行之前更新`ref`的值，那么你应该使用`useLayoutEffect`而不是`useEffect`。例如:**

```
const ref = React.useRef()React.useEffect(() => {
  ref.value = 'some value'
})// then, later in another hook or something
React.useLayoutEffect(() => {
  console.log(ref.value) // logs old value as this runs first!
})
```

# **结论**

**简单地说，当你的组件在状态更新时看起来闪烁，因为回调在组件被绘制后对 DOM 进行了可视化的改变，你应该使用`useLayoutEffect`。**

**默认行为是让浏览器在 React 运行您的代码之前基于 DOM 更新重新绘制。这意味着您的代码不会阻塞浏览器，用户可以更快地看到 DOM 的更新。所以大部分时间坚持使用`useEffect`，除非有必要使用`useLayoutEffect`。**

**希望我能让你比现在聪明一点。注意安全。**

# **参考**

**[pubudu jayasanka](https://medium.com/u/723e34673c91?source=post_page-----738c08a84aa7--------------------------------) 的文章用图表给出了详细的解释。**

**[](https://pubudu2013101.medium.com/what-is-the-real-difference-between-react-useeffect-and-uselayouteffect-51723096dc19) [## 反应使用效果和使用输出效果之间的真正区别是什么？

### 如果您是一名 reactor . js 开发人员，您将会知道这些在进行前端时会被广泛使用

pubudu2013101.medium.com](https://pubudu2013101.medium.com/what-is-the-real-difference-between-react-useeffect-and-uselayouteffect-51723096dc19)**