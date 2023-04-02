# 如何使用 Jest 编写 JavaScript 单元测试

> 原文：<https://javascript.plainenglish.io/how-to-write-javascript-unit-tests-using-jest-422b3c4e050f?source=collection_archive---------12----------------------->

## 用 Jest 编写单元测试的初学者指南

![](img/42a7ed98ae59a17b757da0a2238c30ae.png)

Photo by [Ferenc Almasi](https://unsplash.com/photos/EWLHA4T-mso) on [Unsplash](https://unsplash.com/s/photos/jest)

当我第一次开始编码时，我做的每个项目都需要手工单元测试。这意味着每当我编辑代码时，我都必须坐下来手动测试我能想到的所有用例。你可以想象这是一个可怕的策略！我会经常错过测试用例，遇到许多意想不到的错误(当错误发生在演示过程中时，情况会糟糕一百万倍)。

从那以后，我试着积极努力去写单元测试。希望本指南可以帮助你开始单元测试。

# 设置

在我们开始之前，用下面的文件结构创建一个目录。

```
\testing
   \src
      index.js
   \test
      index.test.js
```

接下来，从根目录在终端中编写命令`npm init`。这将把这个目录初始化为节点开发环境。在终端中，会提示您填写一些关于该项目的信息。重复点击`enter`可以跳过这一步。

接下来，运行命令`npm install --save-dev jest`。这将把 Jest 作为开发依赖项添加到这个项目中。

运行完上面的所有命令后，您的文件结构应该如下所示:

```
\testing
   \node_modules
   \src
      index.js
   \test
      index.test.js
   package-lock.json
   package.json
```

最后，在我们的 package.json 中，我们将修改脚本。在脚本对象内部添加`"test": "jest"`。您的 package.json 最后应该是这样的:

添加这个脚本将允许您在终端中运行命令`npm run test`，并自动测试您在测试目录中编写的所有测试。

# 写作测试

现在是激动人心的部分，编写测试。在本指南中，我将介绍 Jest 的基本知识，但是，我强烈建议您访问他们的网站[这里](https://jestjs.io/)，了解他们的一些更高级的功能。

现在，在我们开始编写测试用例之前，我们必须在`index.js`中编写一些函数。在`index.js`文件中添加以下代码。我们将针对这两个流行的 leet 代码问题创建单元测试，[硬币变化 2](https://leetcode.com/problems/coin-change-2/) 和[斐波那契数](https://leetcode.com/problems/fibonacci-number/)。

接下来，我们可以在`index.test.js`中编写我们的测试用例。我们将首先从描述程序块开始。描述块是对几个相关测试进行分组的代码块。使用我们上面写的代码，我们想为`change`函数和`fib`函数分别创建一个描述块。您的`index.test.js`文件应该如下所示:

接下来，在每个`describe`块中，你将在`test`块中编写你想要的单元测试。你可以写尽可能多的单元测试。以下是我写的测试案例:

在我的例子中，我将只写几个来展示这些测试块的样子。所有测试块通常遵循相同的模式。你可能会初始化一些常量，调用一些函数，但最终，你总会期望某些东西等于某些东西。

在我的测试用例中，我将总是使用函数`expect(value).toEqual(value)`，然而，有许多不同的函数供您使用。完整列表请访问[文档](https://jestjs.io/docs/expect)。

最后，在编写完所有测试用例后，您可以在终端中从根目录运行`npm run test`,并让 Jest 运行您编写的所有单元测试。

Jest 运行所有测试后，您将在终端中收到重要信息，例如哪些测试通过了，哪些测试失败了。失败的测试还将显示更详细的信息，例如失败发生的原因和地点。

希望这个指南是有帮助的。下次见。编码快乐！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)