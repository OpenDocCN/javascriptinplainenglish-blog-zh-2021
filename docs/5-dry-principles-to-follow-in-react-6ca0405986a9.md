# 反应中要遵循的 5 条干燥原则

> 原文：<https://javascript.plainenglish.io/5-dry-principles-to-follow-in-react-6ca0405986a9?source=collection_archive---------0----------------------->

## 今天你可以使用的 5 个有用的技巧！

![](img/4c9bb7dbf292ad1d02731d9154caa675.png)

Photo by [Lucas Myers](https://unsplash.com/@unthunk?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/dry?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

编程通常被认为是一门手艺，而不是一份工作。这也有很好的理由。作为开发人员，我们应该始终努力实现我们编写的任何软件的最佳质量。作为蓝图，有一些令人敬畏的原则可以遵循。我最喜欢的一个是:**“干—不要重复自己”**

今天我将分享我个人用来避免项目中代码重复的 5 个技巧。

# 1.HTTP 呼叫

从一些远程存储中获取数据是任何现代 React 应用程序中最常见的任务之一。初学者在这方面会犯很多错误。下面是一个项目的一般演变

## **第一步。获取组件**内的数据

起初，人们试图在组件内部获取数据。(因为大多数教程向我们展示了这一点)

## **第二步。将逻辑抽象到某种存储中**

在这一步中，人们将组件外的逻辑取出，放入商店管理中(如 redux 或 context)。但是代码中还是有很多重复的地方。

## **如何“干燥”它**

**第一种方法:**尝试创建一个单独的`HttpUtility`类或者自定义的`useHttp`钩子来管理你所有的 HTTP 调用。您可以使用`axios`为您处理远程呼叫部分。但是检测加载状态和处理错误对您来说可能很棘手。

**更好的方法:**花点时间学习一些很棒的库`[react-query](https://react-query.tanstack.com/overview)`它为您提供了一些很棒的功能，对任何规模的应用程序都有用。

# 2.错误处理

以我的经验，我在很多地方都见过有人把这搞砸了。通常，在每个组件中调用祝酒词并不是一个好主意。有一些常见的场景，我们想给用户一些反馈。

## 1.HTTP 调用中的错误

中间件(它们在进入 redux 存储之前拦截任何动作)非常适合处理大多数错误。截取从 HTTP 调用返回的错误，并显示一个 toast。在我的 redux 设置中，我是这样做的

## 2.组件逻辑错误

我们可以实现`[ErrorBoundary](https://reactjs.org/docs/error-boundaries.html)`捕捉所有与组件加载问题相关的错误的想法。这样我们就不需要到处放空支票了。

## 3.合法性错误

我们希望向用户显示错误消息的另一个时候是当用户填写的表单验证出错时。

尝试使用某种形式的表单验证库(如`Yup`)来处理验证错误，并自动向用户提供反馈。或者你可以使用像`[react-hook-form](https://react-hook-form.com/)`这样的库来帮你做！

# 3.组件的组成

我想这是显而易见的。但是，开始使用 react 的人经常无法理解 React 最强大的特性。那就是**可复用组件**

总是试图**将组件分解成更小的部分**。它有多重好处。

1.  它提高了代码质量和可读性
2.  相同的 UI 组件不会在整个项目中重复

# 4.使用自定义挂钩

我个人是 hooks 的忠实粉丝，我认为新开发人员应该尽早了解这一点。

每当任何逻辑被复制，我们想抽象掉逻辑。React 为我们提供了类似 **HOC(高阶元件)**的解决方案

Example of HOC

虽然钩子通常用于同样的目的，但它们以一种更干净的方式实现这一目的。前面的代码可以这样重写！

Example of Hook

# 5.避免重复的样式

造型一直是我的一大痛。我相信这对于其他初学者来说也是一样的。对我来说，作为开发者的进化看起来是这样的。

## **第一步。**使用`.css`文件对组件进行造型。

正如我们所知，如果你不善于组织你的风格文件，你可能会迷失在重复的 CSS 逻辑中。

## **第二步。在这个阶段，我学会了 Sass**

它非常适合以模块化的方式编写 CSS。它提供了重用 CSS 代码的能力，并在 CSS 中引入了 mixin 和变量的概念。但是，我仍然觉得很难管理。也许这部分是我的错

**最后，**我遇到了`[styled-components](https://styled-components.com/)`，这是一个很棒的库，可以重用组件的样式。对我来说，这有助于创建更多可读的组件，并且在我的代码中不再有`className`！

下面是一个运行中的样式化组件的例子

# 结论

给你。为了遵循 React 中的 DRY 原则，您可以将这些技巧应用到您的项目中。这些不是防弹的解决方案，但是理解所有这些工作可以带你走很长的路。

如果您对高级最佳实践感兴趣，这里有另一篇文章适合您。

**有话要说？通过** [**LinkedIn** 联系我](https://www.linkedin.com/in/56faisal/)

[](https://betterprogramming.pub/the-7-traits-of-a-rock-star-react-developer-747fbb001c05) [## 摇滚明星 React 开发者的 7 个特质

### 造成差异的习惯

better 编程. pub](https://betterprogramming.pub/the-7-traits-of-a-rock-star-react-developer-747fbb001c05) 

祝您愉快！:D

**通过** [**LinkedIn**](https://www.linkedin.com/in/56faisal/) **或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**