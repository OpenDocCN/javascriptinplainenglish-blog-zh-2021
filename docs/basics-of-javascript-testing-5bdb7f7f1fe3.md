# JavaScript 测试基础介绍

> 原文：<https://javascript.plainenglish.io/basics-of-javascript-testing-5bdb7f7f1fe3?source=collection_archive---------16----------------------->

![](img/72b2b640c61acfee16e9f379473443cc.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你可能会想:“等等，又一篇关于 JavaScript 测试的文章？”

是的，我愿意更多地谈论 JavaScript 测试基础的原因是，围绕这个主题的许多文章都是以非常相似的方式构建的——通过展示代码片段和工具来编写 JavaScript 测试。

本文将采用不同的方法来测试 JavaScript，以及如何构建像断言库或测试框架这样的工具。

本文中使用的例子来自[TestingJavaScript.com](http://testingjavascript.com)作者[肯特·c·多兹](https://medium.com/u/db72389e89d8?source=post_page-----5bdb7f7f1fe3--------------------------------)。

## 用普通 JavaScript 创建一个简单的测试

假设有一个`sum()`函数，它将两个给定的数字相加并返回结果。例如，3 + 7 将返回 10。

为了用普通的 JavaScript 测试这个`sum()`函数，我们可以简单地通过下面代码片段中的 4 个步骤:

Creating a simple test with plain JavaScript

1.  执行功能
2.  定义期望
3.  返回值
4.  比较
5.  利润！

到目前为止一切顺利。我们刚刚编写了第一个 JavaScript 测试。
如果你想执行你的测试，你可以简单地使用 Node.js 和 do
`node simple-test.js`。这将在您的本地终端中执行您的测试。

为了真正理解像 Jasmine 或 Chai 这样的断言库是如何工作的，接下来我们将自己创建一个。

## 抽象测试并创建您自己的断言库

上面我们写的测试看起来还不算太差，但是测试多了怎么办？如果我们总是自己用那个`if`语句对结果和预期进行比较，并在结果和预期不匹配时抛出一个错误，那么可能要写很多代码。

这就是断言库的由来。它将帮助您抽象断言:

Creating an assertion library with plain JavaScript

让我们看一下上面的代码片段。首先，我们看到我们做了与简单的 JavaScript 测试相同的事情，在第 3 行运行了`sum(3,7)`函数，并定义了一个期望值 10。之后，我们看到断言库开始运行(第 5 行)。

它的读法非常自然，符合常见的英语句子结构:We`expect`the`(result)`T7`(expected)`。

断言库所做的是，它提供了像`expect`或`toBe`这样的函数，让我们使用它们来编写更干净、更抽象的测试。正如您在第 16 行中看到的，它的源代码与我们简单的 JavaScript 测试没有太大区别。这只是一个函数，用所谓的“匹配器”(在我们的例子中是`toBe`)返回一个对象。这个语法最初在一个名为 [Jasmine](https://jasmine.github.io/index.html) 的库中使用，它现在是测试框架 [Jest](https://jestjs.io/) 的一部分。

进一步抽象我们的测试的下一步是创建一个我们自己的测试框架，非常类似于 Jest。

## 通过创建你自己的测试框架来抽象更多

你试过上面的代码吗？复制出来，粘贴到一个新的 JavaScript 文件中，使用 Node.js ( `node testfile.js`)执行。

完成了吗？当您执行终端并通过测试时，您会在终端中看到什么？

对于通过的测试，您现在看不到任何输出，这很遗憾。我们还想知道我们的测试何时成功执行，并得到一个漂亮的勾号，最好是可爱的绿色。

这就是测试框架出现的地方。测试框架将您的测试包装在一个函数中，这允许您在一个范围内执行测试。要了解不同变量范围的更多信息，请查看 Kevin Kononenko 的这个非常棒的代码类比:

[](https://medium.com/free-code-camp/how-javascript-variable-scoping-is-just-like-multiple-levels-of-government-d7ddabc49bf1) [## JavaScript 变量作用域就像多级政府

### 你有没有在一次又一次地得到一个未定义的值后沮丧地砸碎你的键盘，同时试图…

medium.com](https://medium.com/free-code-camp/how-javascript-variable-scoping-is-just-like-multiple-levels-of-government-d7ddabc49bf1) 

测试框架还提供了更好的测试结果日志。

Create a testing framework with plain JavaScript

正如你在上面的代码片段中看到的,`test(title, callback)`函数(在第 12 行)试图执行回调，如果能够执行的话，就注销一个。

否则(当它捕捉到错误时)，它将记录一个✕和相应的错误消息。

我们的`sum()`测试可以被包装在这个测试块中，在使用 Node.js 执行它之后，我们将获得适当的终端输出，无论测试是通过还是失败。

如果你仔细观察:这个例子中的第 1 到第 4 行和一个简单的[玩笑测试](https://jestjs.io/docs/getting-started)看起来完全一样。

我们不需要编写自己的测试框架，我们可以依赖 Jest 这样的稳定测试框架来测试我们的 JavaScript。

## 结论

正如你所看到的，编写一个 JavaScript 测试非常简单，你所使用的工具(比如 Jasmine 或者 Jest)的核心就是简单的 JavaScript 函数，这些函数抽象了你的测试。

鸣谢:Kent C. Dodds，他在“专业测试 JavaScript 课程”中的教学理念启发了我写这篇文章。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)