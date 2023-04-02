# Node.js 的集成和单元测试

> 原文：<https://javascript.plainenglish.io/integration-unit-testing-for-node-js-5d44b588cd17?source=collection_archive---------10----------------------->

## 使用摩卡和柴☕️测试 Node & Express 项目的初学者指南

![](img/261c54ac61a45e2524cd57a9ca885f7a.png)

Photo by [Sincerely Media](https://unsplash.com/@sincerelymedia?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

软件测试验证我们的代码按预期工作，并且满足它需要的技术、功能和用户需求。测试是开发任何软件的一个重要部分，但是作为一个学习和发展他们技能的领域，它经常被新工程师忽略。通常情况下，很难找到好的教程、指南或博客文章来解释代码项目的不同类型的测试，以及如何实际编写这些测试。

首先，我想回顾一下在软件测试中经常出现的一些重要词汇，以及它们的含义:

## **单元测试**

单元测试是对程序的最小“单元”或组件的测试。在大多数情况下，被测试的最小单元是一个函数。因此，在这些情况下，我们正在测试以确保我们的单个功能按预期工作。

单元测试是在任何其他类型的软件测试之前执行的，通常开发人员有责任进行和编写这些测试。

## **集成测试**

集成测试是对提供给定功能的一组相关代码单元组合的测试。在这种情况下，我们正在测试单元之间的交互中可能出现的错误。

集成测试也可能是开发人员的责任，但是让独立的测试人员参与集成测试并不罕见。

在这个例子中，我们将检查一个节点的单元和集成测试。Js & Express API 项目。我们的示例项目的主要功能是用一个随机数响应 GET HTTP 请求，这并不太重要，因为主要的焦点是测试。

# 工具

## Node.js & Express🔥

我们将创建一个简单的 Node.js 应用程序，它使用 [Express.js](https://expressjs.com) 框架来创建一个迷你 API。这只是为了举例，将作为测试中的代码。

有关这两者的更多信息，请查看 [Node.js](https://nodejs.org/en/) 和 [Express.js](https://expressjs.com) 文档。

## 摩卡☕️

Mocha 是一个灵活的开源 JavaScript 测试框架，运行在 Node.js 上。它用于测试同步和异步代码，并很好地将测试结果记录到控制台。Mocha 既可以用于单元测试，也可以用于集成测试。

Mocha 可以与大多数[断言库](https://stackoverflow.com/questions/25678063/whats-the-difference-between-assertion-library-testing-framework-and-testing-e/25678226#25678226)(一个负责验证测试结果的工具)一起使用，但是与 Mocha 一起使用的最流行的 Node.js 断言库叫做 Chai。

## 柴&柴-http

Chai 是一个行为/测试驱动的设计断言库，在 Node.js 测试中经常与 Mocha 一起使用。Chai-http 是 Chai 的一个插件，它允许我们用 Chai 编写 http 集成测试。

以热饮为主题的两个人一起工作，创造了一个测试 Node.js & Express 项目的好方法。

# 该设置

需求: [Node.js 安装](https://nodejs.org/en/)。

为了最好地演示测试，我们需要一些代码来测试。

*(如果您使用本教程作为测试现有项目的指南，那太好了！您不需要创建这个项目，但是测试应该遵循相同的原则。)*

首先，创建一个新的 Node.js 项目(创建一个新文件夹并从那里运行`npm init`)。之后，继续使用`npm install express`安装 express。

接下来，我们将创建我们的`server.js`文件，它将保存我们的示例应用程序的所有逻辑:

我们的节点应用程序在`localhost:3000`监听，并公开一个返回随机数的端点`/random`。您可以通过运行您的应用程序(`npm start`)并在浏览器中导航到`localhost:3000`来尝试一下。

# 测试

现在是测试的时候了！

为了正确设置，我建议你创建一个`test`子文件夹来保存这个应用程序的所有测试文件。

接下来，我们需要通过运行以下命令来安装测试库:

```
npm install mocha chai chai-http
```

确保在我们的`package.json`中，我们已经将 Mocha 添加到我们的测试脚本中，如下所示:

```
...
  "main": "server.js",   
  "scripts": { 
    "start": "node server.js",
    "test": "mocha"
  },   
  "author": "",
...
```

这意味着现在我们只需要在想要运行测试时运行`npm test`。我们现在已经设置好了，准备编写我们的第一个单元测试。

## 单元测试

如前所述，单元测试就是测试单个的功能。在我们的示例代码中，我们将编写一个单元测试，检查我们的`getRandom`函数是否做了它应该做的事情，并生成一个 0 到 100 之间的随机整数。

我们首先需要 chai 和 chai.assert 来获取我们的断言库。然后，我们描述被测函数，调用该函数，并对结果进行断言。

这里，`describe`函数封装了我们的测试。第一个参数是一个描述我们正在测试的内容的字符串(为了举例，我称之为‘单元测试’，但是传递类似‘get random random number generation’这样的东西会更有描述性)。

传递的第二个参数是作为测试主体的函数。它以一个`it`函数开始，类似于`describe`函数，描述测试。这里，我们给出了我们正在测试的功能的一个小描述，或者预期的功能是什么。第二个参数是另一个函数，在这个函数中，我们实际上可以编写我们的测试代码。

在这个例子中，我们使用的是`assert`断言风格，但是 Chai 提供了其他风格的断言，比如`should`或者`expect`。你可以在[柴断言风格指南](https://www.chaijs.com/guide/styles/)中找到它们之间的区别。

当这个测试运行时，我们的`getRandom`函数被调用，测试对结果进行断言。我们断言(验证)返回的结果(`random`)不为空，是一个数字，至少为 0，但不超过 100。如果所有这些断言都通过了，那就意味着我们的代码按照预期的方式运行，并且我们的单元通过了单元测试。

## 集成测试

测试我们的 API 端点的功能构成了一个集成测试，因为我们正在测试当我们的`/random`端点被点击时，我们的程序的所有独立部分如何一起工作来发送一个响应。为了做到这一点，我们需要使用`chai-http`。这个包允许我们在测试期间向服务器发出 HTTP 请求。

由于使用了异步代码并承诺实现这一功能，我们不得不以稍微不同的方式对待这一代码的集成测试。我们在调用和测试我们的异步代码的`it`函数内部传递一个回调(和以前一样)。

`chai-http`允许我们通过传入应用程序来构造对应用程序的请求。这将自动打开我们的服务器来接收请求。然后我们可以使用`.get()`来调用我们的`/random`端点。然后使用`end`方法发出请求并断言响应。

因为`end`函数是一个回调函数，我们必须使用`done`回调函数来向 Mocha 表明我们的回调函数已经完成，断言已经准备好被验证。如果我们不这样做，测试将在断言被检查之前通过。

我们检查我们的响应包含一个成功的状态代码，并且响应返回的数字不为空，是一个数字，至少为 0 但不大于 100(没有变化)。

在这个集成测试中，我们不仅要确保从我们期望的 API 端点获得响应，还要确保我们的 API 在响应 GET 请求时，整体上表现得像预期的一样。这是在测试我们的应用程序的多个“单元”如何一起提供这种功能。

就是这样！我们已经完成了迷你 API 的单元测试和集成测试。

虽然这是一个简化的示例，但是您可以使用这些作为模板，继续测试您自己的更深入的 Node & Express 项目。实现保持不变，但是您可以进一步开发这些示例测试并复制它们，以便测试更大更复杂的程序。

下面我链接了 Node.js 中其他一些关于单元和集成测试的优秀指南，以及 Mocha & Chai 的官方文档。测试愉快！

## 资源

*   使用 Mocha & Chai 在 Node.js 中进行单元测试—[https://livecodestream . dev/post/Testing-in-nodejs-using-Mocha-and-Chai-part-1/](https://livecodestream.dev/post/testing-in-nodejs-using-mocha-and-chai-part-1/)
*   Node.js 与 Mocha & Chai 的集成测试—[https://livecodestream . dev/post/Testing-in-nodejs-using-Mocha-and-Chai-part-2/](https://livecodestream.dev/post/testing-in-nodejs-using-mocha-and-chai-part-2/)
*   使用 Mocha & Chai 进行 JavaScript 测试—[https://code burst . io/JavaScript-unit-Testing-using-Mocha-and-Chai-1d 97d 9 f 18 e 71](https://codeburst.io/javascript-unit-testing-using-mocha-and-chai-1d97d9f18e71)
*   Node.js 的单元和集成测试—[https://blog . log rocket . com/unit-and-Integration-Testing-for-node-js-apps/](https://blog.logrocket.com/unit-and-integration-testing-for-node-js-apps/)
*   摩卡—[https://mochajs.org](https://mochajs.org)
*   柴—[https://www.chaijs.com](https://www.chaijs.com)
*   柴-http—[https://www.chaijs.com/plugins/chai-http/](https://www.chaijs.com/plugins/chai-http/)

*更多内容看*[***plain English . io***](https://plainenglish.io/)