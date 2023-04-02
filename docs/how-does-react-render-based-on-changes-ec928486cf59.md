# React 如何基于变化进行渲染？

> 原文：<https://javascript.plainenglish.io/how-does-react-render-based-on-changes-ec928486cf59?source=collection_archive---------6----------------------->

## React 中每次渲染时是否检查所有道具？

![](img/a636056e24006d91c39810d7bc0144ab.png)

React Profiler Figure

先从一些常识说起。我们了解到，在决定渲染每个纤维之前，会检查所有道具。

> 可以说纤程是树的一个组成部分或一个节点。在本文中，我们互换使用它们。

这样对吗？抛开这一点，它真的没有告诉我们太多，前。它的起点和终点。它也没有告诉我们道具和状态之间的区别。

我们用一个例子来说明这件事。在上图中，其中一个组件(第一个彩色块)的状态已经改变。它定义了这个组件，如下所示。

```
const Title = () => {
  const [count, dispatch] = useState(0)
  const onClick = () => { dispatch(1) } return <Child onClick={onClick} count={count />
}
```

这是一个非常简单的组件，它将一个`state`传递给它的子组件。在某一点上，我们点击它，因此增加状态到一个新的值。让我们称这个纤程为动作开始的源纤程。

## 在到达源光纤之前

让我们写一些伪代码来看看这是如何工作的。为了方便起见，我们将光纤分成两个阵营，一个是到达源光纤之前的光纤，一个是源光纤之下的光纤。

当 React 收到一个更新请求时，它从树的最顶端开始遍历。在到达源纤程之前，沿途的每个纤程都通过克隆前一场景中的纤程来保释，如以下伪代码所示。

```
function beginWork(fiber) {
  if (!anyWorkOnFiber) {
    return bailoutOnAlreadyFinishedWork(fiber)
  }
}
```

在我们的侧写图中，深灰色表示紧急援助。这些纤维代表了在儿童中没有工作但包含一些工作的纤维。React 标记它们，以便它知道如何到达源纤维。紧急救援通过重用以前协调的子对象跳过渲染。

同样的紧急情况也适用于剖面图中的浅灰色点状颜色。那些纤程代表不在源纤程的祖先分支中的纤程。所以他们没有任何工作，也没有任何工作在它的任何一个孩子身上。

## **下源光纤**

好了，现在我们到了源光纤。因为这个纤维有工作要做，它需要一个新的渲染。

```
function beginWork(fiber) {
  let didReceiveUpdate const children = renderFiber(fiber)  if (!didReceiveUpdate) {
    return bailoutOnAlreadyFinishedWork(fiber)
  } reconcileChildren(fiber, children)
  return fiber.child
}
```

如果它是一个功能组件，它调用函数并返回被调和成纤程的子元素。在所有子纤维准备好之后，它返回第一个子纤维以继续渲染工作。这基本上就是`beginWork`所做的。

在渲染之前创建了一个标志`didReceiveUpdate`，它最初是假的，在渲染过程中，如果检测到状态变化，任何钩子都可以把它改成`true`。渲染之后，如果这个标志仍然是假的，那么我们知道在这个纤程中没有任何改变。因此它可以在渲染后被保释出来。无论有没有紧急援助，渲染都需要按照 Profiler 图中的颜色块所示进行。

## 渲染从源纤维开始

所以我们有两个版本的`beginWork`用于纤程，在源纤程之前和之下。React 如何在两者之间切换？当然，React 实际上有许多其他途径，但本文试图将其过度简化，这样我们至少可以理解主要途径。

```
function beginWork(fiber) {
  let didReceiveUpdate if (oldProps !== newProps) {
    didReceiveUpdate = true
    beginWorkBeforeSourceFiber()
  } else {
    beginWorkUnderSourceFiber()
  }
  ...
}
```

在`beginWork`开始的时候，它检查了这个纤维在前一个和当前之间的道具。如果它改变了，它实际上认为纤维在源纤维下面？哇！？注意严格的等号运算符`!==`。它不是检查里面的每个道具，而是检查整个道具对象。

这一行翻译过来就是**如果一个父元素被渲染，一个子元素会得到一个新的道具，因此它也需要被渲染**。

当一个子体被调和成一个纤程时，它创建一个带有`newProps`的纤程。只要一个父渲染，它就进入所有子和孙的新道具和新渲染的政权。有可能打破这种制度的是一个子纤维与`didReceiveUpdate`渲染后为假。

## 道具是被动的东西

道具真的是一个被动的东西，就像一个函数的参数一样。它总是和组件在一起。如果它不是一个渲染，假设至少有一个道具是从状态变化中派生出来的(或与状态变化相关联)，它就不能为它的子对象获得新的道具。

如果一个组件没有被渲染，道具永远不会被更新以反馈给子组件，因此道具本身在理论上不能作为一个原因进行改变。更有趣的是，整个道具(而不是道具内部的每个单独的道具)用于检查是否应该执行渲染。

所以状态和道具有点鸡和蛋的关系。这么说吧，

```
React.render(<App />, ...)
```

也许只有当我们第一次调用渲染时，props 才会变得活跃，但是在前面的代码中，我们倾向于为 props 放置`{}`。因此大多数时候道具根本不是驱动新渲染的力量。

那么为什么有时我们说我们可以跳过不变道具的渲染呢？也许“跳过”的意思也不是主动时态，它只是意味着道具可以从一些渲染中过滤掉，比如在`React.memo`的例子中。

## 结论

在状态改变时，道具被用来通过新的渲染发送更深层次的信息。然而，是否对纤维执行新的渲染是由该状态改变而不是任何单独的属性改变来确定的。

*更多内容请看*[***plain English . io***](http://plainenglish.io)