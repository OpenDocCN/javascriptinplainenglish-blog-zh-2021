# 什么是 React 钩子以及如何使用它们？

> 原文：<https://javascript.plainenglish.io/what-are-react-hooks-and-how-to-use-them-b3c734b7ab80?source=collection_archive---------13----------------------->

![](img/f104972b5010e33abac5915e70b35847.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> 到目前为止，您应该听说过 React hooks。然而，您可能想知道这个技术术语是什么意思。好吧，我们在这里回答这个问题怎么样！

长话短说，React 挂钩不仅是一种让 React 类组件知道状态的方法，也是一种让 React 函数组件知道状态的方法。简单来说就是这样。

当您使用 React 组件时，您可以将它们指定为一个类或一个函数。唯一的问题是，在 React 挂钩出现之前，您不能向 React 函数组件添加状态，并且这些状态只对 React 类组件可用。

现在你已经了解了什么是 React 钩子，在 React 钩子介绍的下一部分，我们将看到如何使用 React 钩子。

## 如何使用 React 钩子？

在我们继续之前，React 钩子不能用在 React 类组件中。它们只在 React 函数组件中工作。这是因为 React 类组件已经有了自己管理状态的方式，所以它不需要钩子。

要使用一个钩子，你需要提供一个你想要持久化状态的属性，以及一个更新这个属性的函数。现在，如你所知，每次更新状态时，**都会重新呈现 React 中的**。同样的情况也会发生在有钩子的 React 函数组件中。

我知道这太酷了。

作为一个用法示例:

```
function YourCoolHookComponent () {
  const [skillLevel, updateSkillLevel] = useState(0);

  return (Did you learn something cool?  updateSkillLevel(skillLevel + 1)}>YesCurrent Skill Level {skillLevel})
}
```

我们将通过关注三个关键点来解释上述代码的含义:

*   使用状态()
*   对象析构(skillLevel，updateSkillLevel)。

## 什么是使用状态(参数)？

使用状态是这一切的中心。如您所见，它接受一个默认参数，在我们的例子中，它接受 0。这是因为为了安全起见，它接受的数据类型应该与它应该更新的数据类型相同。

它当然可以接受 1，2，甚至 100。这取决于您在组件初始化时如何处理水合作用。因此，它将返回一个值，以及应该更新这个值的函数，因此**对象析构**。

## 对象析构。

在我们的例子中，我们将从**使用状态**接收两个值，它们是**技能级别**和**更新技能级别**。这些可以是您想要的任何名称，**但是**的想法是应该有那个 ***值+ updateFunction*** 匹配。

现在，每当你点击 **YES** 按钮，更新方法将被调用，在我们的例子中，使用我们想要更新的新值。例如，用户每点击一次，他们的技能等级就会增加 1。

## 结论。

正如您所看到的，通过对 React 钩子的介绍，只要您理解 React 钩子背后的核心逻辑，您很快就可以拥有一个非常基本的钩子。

好了，简单的介绍就到此为止。

**快乐编码！**

> 你有兴趣学习**反应**吗？在我的网站上查看类似的精彩文章:[沉迷于代码>反应](https://bingeoncode.com/category/react)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)