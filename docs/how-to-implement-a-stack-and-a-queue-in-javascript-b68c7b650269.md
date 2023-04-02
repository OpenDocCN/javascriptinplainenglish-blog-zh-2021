# 如何用 JavaScript 实现一个栈和一个队列？

> 原文：<https://javascript.plainenglish.io/how-to-implement-a-stack-and-a-queue-in-javascript-b68c7b650269?source=collection_archive---------12----------------------->

![](img/f1a69348d3935898c4835b43f9058d80.png)

Photo by [Dan Counsell](https://unsplash.com/@dancounsell?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

堆栈和队列是我们可以在 JavaScript 程序中使用的基本数据结构。

堆栈允许我们向其中添加项目，最后添加的项目是第一个可以删除的项目。

队列允许我们向其中添加项目，添加的第一个项目也是可以删除的第一个项目。

在本文中，我们将研究如何用 JavaScript 实现堆栈和队列。

# JavaScript 堆栈方法

JavaScript array 带有内置的方法，使它们像一个堆栈一样工作。

`push`方法让我们将项目添加到数组的末尾。

而`pop`方法让我们从数组中移除最后一项。

例如，我们可以通过编写以下内容来创建堆栈:

```
const stack = []
const pushed = stack.push(1, 2)
console.log(stack)
const popped = stack.pop()
console.log(stack, pushed, popped)
```

`push`方法让我们将作为参数传入的项目追加到`stack`数组中。

它返回最后一个添加到数组中的项目。

因此，`pushed`是 2。

`pop`方法让我们从数组`stack`中移除最后一项。

并返回弹出的项目。

所以`popped`是 2，这就是从数组中移除的内容。

所以从第一个控制台日志记录时,`stack`是`[1, 2]`。

第二控制台日志将记录`[1]`为`stack`的值。

# JavaScript 队列方法

JavaScript 数组还附带了一些方法，让我们可以将它们用作队列。

我们使用`push`方法将条目添加到队列中，就像我们处理堆栈一样。

我们可以使用`shift`方法删除数组中的第一项。

例如，我们可以写:

```
const queue = []
const pushed = queue.push(1, 2)
console.log(queue)
const shifted = queue.shift()
console.log(queue, pushed, shifted)
```

因此，第一个控制台日志将`[1, 2]`记录为`queue`的值。

而在第二控制台日志中，`queue`就是`[2]`。

`pushed`为 2，`shifted`为 1。

`shift`返回添加到数组开头的元素。

# 大小

要获得任一数据结构的大小，我们可以使用`length`属性。

所以我们可以分别记录`stack.length`和`queue.length`来得到它们的大小。

# 结论

我们可以通过使用原生数组方法用 JavaScript 实现一个堆栈或队列。

我们用属性`length`得到它们的大小。

*更内容于* [*简单明了的*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*