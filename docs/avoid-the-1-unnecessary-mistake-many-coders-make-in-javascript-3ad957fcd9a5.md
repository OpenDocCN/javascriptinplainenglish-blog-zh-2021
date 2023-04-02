# 避免许多程序员在 JavaScript 中犯的 1 个不必要的错误

> 原文：<https://javascript.plainenglish.io/avoid-the-1-unnecessary-mistake-many-coders-make-in-javascript-3ad957fcd9a5?source=collection_archive---------5----------------------->

## 检查如何以无点样式使用处理函数

![](img/052fb43f43e92ee405f18b424794c4a7.png)

Photo by [Nigel Tadyanehondo](https://unsplash.com/@nxvision?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

每当您使用承诺并将响应链接到函数调用时:

*本代码多余。但是为什么呢？*

共同点是您从远程 URL 获取数据，当这个地址返回数据时，会调用另一个函数。在这种情况下`res`是数据，`processResponse(...)`是函数调用。

> 到目前为止似乎是合法的，也很常见，对吧？

事实上，这段代码中有一个错误。再次检查执行顺序。

1.  您可以访问远程网址。
2.  你等待回应。
3.  您处理响应。
4.  *调用另一个函数来处理响应。*

第四点就是问题所在。这是多余的。您已经处理了回复。

# 让它变得更好

只需使用隐含的参数来调用处理函数，并通过这样做来转换代码:

你会得到和以前一样的答案，但是更快更简单。

这样的工作方式被称为*无点*或*默契。*它的主要特点是从不为每个函数应用程序指定参数。

此外，作为开发人员，它帮助您思考函数本身及其含义。也是代码的未来读者。

您可以省略低级别的工作，传递数据并使用它。

在代码的较短版本中没有无关或不相关的细节:如果你理解被调用的函数的作用，你就理解了完整代码的含义。

# 使用方法时要注意

当你调用一个对象的方法时，你应该处于警报模式。如果您的原始代码类似于此:

您不能只将代码转换为以下内容并期望它能够工作:

原因很简单。调用方法的原始代码绑定到一个对象。在这种情况下，交给`anObject`。当你现在把代码转换成缩小版本时，它只是一个自由的函数。

但是您可以通过`bind()`很简单地解决这个问题:

这是一个普遍的解决方案。当你处理一个方法时，你不能简单地分配它；你必须使用`bind`。只有到那时，正确的上下文才可用。

必须更改为:

这看起来相当笨拙，也不太优雅，但这是必需的，这样方法才能与正确的对象相关联。

即使这段代码看起来不太好，每当你必须处理对象的时候(记住，我们并没有说我们会尝试完全用 FP 代码，如果其他的构造让事情更简单的话，我们会接受)，你必须记住在把它们作为一级对象传递之前，以无点的方式绑定方法。

获取 26 份备忘单，只研究你真正需要的东西，以获得你的第一份网络开发工作！

![](img/227a060a3bfa55f41fa795d5990e6032.png)

[Arnold Code Academy 26 Web Developer Cheatsheets](https://arnoldcodeacademy.ck.page/26-web-dev-cheat-sheets)

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)