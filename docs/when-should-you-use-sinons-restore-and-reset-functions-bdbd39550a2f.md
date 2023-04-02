# 什么时候应该使用 sinon 的恢复和复位功能？

> 原文：<https://javascript.plainenglish.io/when-should-you-use-sinons-restore-and-reset-functions-bdbd39550a2f?source=collection_archive---------5----------------------->

## 在本文中，我们分析了 sinon 中的 restore、reset、resetHistory 和 resetBehaviour 函数的区别，以及它们的行为取决于我们的 sinon fakes 是匿名的还是包装了现有的属性。

正如他们自己的文档中的[所示，在与 sinon 合作时，一个非常常见的方法是调用函数`restore`作为 Mocha 的`afterEach`钩子的一部分。](https://sinonjs.org/releases/latest/sandbox/)

```
afterEach(function () {
    // completely restore all fakes created through the sandbox
    sandbox.restore();
});
```

这应该足以确保在新的测试开始时一切都恢复正常，并且它们不会相互影响，对吗？嗯，**有时候不是这样**。

让我们看看下面的例子:

看起来`restore`做得很好，除了`log.info`间谍的呼叫计数。作为第二个单元测试的一部分，我们期望它只被调用一次，但是结果是前一个单元测试的调用计数没有被正确地重置，并且间谍的`callCount`的值是 **3** 。

# 为什么 sinon.restore 不能像我预期的那样工作？

如果我们看一下 sinon spy 的`restore`函数的文档，我们会读到以下内容:

> 用原来的方法代替间谍。**仅在间谍替换现有方法**时可用。

重点强调的句子是关键。sinon **中的`restore`函数只对替换现有方法**的间谍和存根起作用，我们的间谍被创建为匿名(独立)间谍。

因此，`restore`不会重置调用计数，随着 spy 函数在后续测试中被调用，调用计数将继续增加。

我们如何让它发挥作用？

# 介绍复位和复位历史功能

如果我们查看文档，我们会发现间谍和存根具有以下一些功能:

*   `resetHistory`:对于**间谍**，复位状态；对于**存根**，它重置历史调用。对于**沙箱**，它重置沙箱中创建的所有存根的历史。
*   `resetBehavior`:仅适用于**存根**和**沙箱**，它重置存根的原始行为。
*   `reset`:对于**存根**，重置行为和历史；对于**沙箱**，重置沙箱中创建的所有内容的内部状态。

在我们的例子中，我们可以使用`resetHistory`函数来确保 spy 的调用计数在第一次测试后被重置，这样它的执行就不会与第二次测试冲突。我们可以将此作为摩卡`afterEach`钩子的一部分:

```
afterEach(() => {
    sandbox.restore();
 **log.info.resetHistory();**
});
```

请记住:在`afterEach`挂钩中添加`sandbox.reset()`不会有帮助，但是如果我们将它添加到第一个单元测试的末尾，它是有效的——仍然没有弄清楚为什么会发生这种情况。

# 或者只是避免使用匿名间谍

这将是另一种选择。不使用匿名间谍:

```
const log = {
    info: sandbox.spy(),
    error: sandbox.spy()
};
```

有一个通用的日志模拟对象，并在其上安装间谍:

```
const log = {
    info: function () { /* Do nothing */ },
    error: function () { /* Do nothing */ }
};sandbox.spy(log, 'info');
sandbox.spy(log, 'error');
```

![](img/d09e795ee0c81f4db5e33b0364ab1128.png)

Photo by [Bernard Hermant](https://unsplash.com/@bernardhermant?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)