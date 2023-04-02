# 如何用 Jest 模拟模块中的单个函数

> 原文：<https://javascript.plainenglish.io/how-to-mock-a-single-function-from-a-module-with-jest-8f9994bf9410?source=collection_archive---------3----------------------->

## 用 Jest 嘲笑整个模块很容易。但是，如果您只想模仿模块中的一些功能，该怎么办呢？

![](img/13aa8bd539062173b7f543dca2a3e7ff.png)

Photo by [Thought Catalog](https://unsplash.com/@thoughtcatalog?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Jest 是一个很好的 JavaScript(或 TypeScript)测试框架。它提供了许多功能和大量关于如何使用它们的指南(有例子)。

想要创建一个模拟函数并将其作为回调传递给正在测试的组件吗？当然可以！如果愿意，您甚至可以给它一个定制的模拟实现。

需要模拟整个模块或库吗？这只需要一行代码。您还可以为这些应用程序提供定制的模拟实现。您甚至可以为一个对象的特定方法创建模拟。

但是，当指南中有 50 个不同的例子似乎涵盖了天底下除了您正在寻找的用例之外的所有内容时，您知道那种感觉吗？好吧，这可能有点戏剧性的解释，但你得到了要点。

如果您不想模拟整个模块或库，该怎么办？如果你只想模仿它的一个功能呢？还是几个精选的？

我花了相当长的时间来整理正确的谷歌查询。因此，这里有一个简短的指南，以防你最终陷入同样的困境。(是的，一旦我知道要找什么，我也设法在官方文档中找到了一个例子。)

# 模仿单一功能

有三个简单(也有点混乱)的步骤，只模仿一个模块的一个函数，将其余的函数保留为默认实现。

1.  为整个模块创建一个模拟。
2.  告诉模仿者对所有事情都使用实际(非模仿的)实现。
3.  模仿模仿者想要的功能。

有点绕口令，不是吗？但是语法非常简单，每个步骤只需要一行代码。

首先，使用`jest.mock`函数创建一个模块的模拟。与`import`语句一样，`mock`函数接受一个字符串，该字符串表示本地模块的路径或您想要模仿的库的名称。在示例中，我将把它称为`path`。

然后，使用`jest.requireActual`函数告诉 mock 使用模块中所有东西的真实实现。您应该传入在`mock`函数中传递的表示路径或名称的相同字符串。

在您传递实际实现的需求之后，您可以覆盖您想要模仿的函数的实现。您只需列出函数名，并给它赋值`jest.fn()`。

`jest.fn()`将创建一个空的实现，但是您可以覆盖它以获取参数并拥有一个自定义的返回值。

下面是您需要在测试中编写的三行代码，以使它正常工作。

在 Jest 的新版本中，您可能需要将`jest.requireActual`的结果存储在一个变量中，然后使用 spread 运算符，如下所示。

这就是全部了。感谢您的阅读！

# 资源

*   来帮忙的 StackOverflow 问题(我终于找到了):[https://stack overflow . com/questions/59312671/mock-only-one-function-from-module-but-leave-rest-with-original-functionality](https://stackoverflow.com/questions/59312671/mock-only-one-function-from-module-but-leave-rest-with-original-functionality)
*   笑话文档:【https://jestjs.io/ 
*   包含此示例的`requireActual`的 Jest 文档:[https://jest js . io/docs/jest-object # jestrequirectalmodulename](https://jestjs.io/docs/jest-object#jestrequireactualmodulename)

*更多内容请看*[***plain English . io***](http://plainenglish.io)