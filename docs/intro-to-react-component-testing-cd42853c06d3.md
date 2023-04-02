# React 组件测试简介

> 原文：<https://javascript.plainenglish.io/intro-to-react-component-testing-cd42853c06d3?source=collection_archive---------7----------------------->

## 工具、标准和最佳实践

![](img/4497771cc2dc2d15940290554da6428b.png)

Photo by [Glenn Carstens-Peters](https://unsplash.com/@glenncarstenspeters?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](/s/photos/checklist?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 拥抱测试的力量

测试驱动开发是一种流行的实践，这是有原因的。在开始编写更多代码之前，通过为单个函数添加和运行测试，从一开始就将测试作为优先事项有助于避免将来引入难以发现的错误。

测试的标准流程很容易记住…安排、行动和断言。首先，安排代码(包括所需的道具或其他参数)，调用一个动作(单击一个按钮，给出虚假的用户输入等)。)，并做出断言(注入你的假设)。请记住，我们的目标是模拟该应用程序在生产中的使用方式。

## 从哪里开始

在开始之前，请记住，我们不一定需要测试所有内容。这里有一些我们在构建测试文件时做的和不想关注的事情。

务必为您已经创建的方法、隔离单元、条件输入和预期呈现编写测试。

不要关注第三方库，复杂的连接比如 React props 是否传递给孩子，或者不影响最终用户功能的东西比如全局变量。

总是用标准的约定命名你的测试文件:file_name_here.test.js。否则，当你运行你的应用程序的测试脚本时，它将不知道测试文件在哪里。

当您想要运行一个单独的测试时(假设您已经安装了必要的库)，只需键入 yarn 或 npm test，后跟文件名。

## 单元、集成和电子对电子

有 3 种通用类型的测试:单元测试、集成测试和端到端测试。

编写单元测试是为了验证小块代码的预期功能。这些用于单一方法。

集成测试旨在检查应用程序的不同部分(或组件)是否如预期的那样协同工作。

端到端测试将较小的单元测试和集成测试封装成一个在模拟浏览器中进行的大型测试。例如，您可以使用 E-to-E 测试，从收集用户查询数据库或 API 的输入开始，查看用户是否得到了正确的身份验证。

## 测试 React 组件的常用工具

React 自带测试库，方便地称为 React-Testing-Library。它因一些有用的内置方法而受到称赞，如 afterEach(cleanup ),该方法在测试和查询 getByText 等方法后卸载组件。另一个主要卖点是，我们可以使用像 useReducer 这样的挂钩，它在使用 actions 和 Reducer 时测试组件的行为，并使用 Context 测试子组件是否可以更新其父组件的上下文状态。

另一个广泛使用的测试程序是 Jest。如果您使用 create-react-app，它可能已经在您的 package.json 文件中了。然而，Jest 不仅仅局限于反应。这是一个 JavaScript 测试框架，可用于 Babel、Angular、Vue 等。

我们还需要一些测试实用程序，让我们能够将组件安装到一个假 DOM 上，并对它们进行遍历。最流行的工具是酶。它基于 React 的 DOM 渲染器来测试模拟 DOM 中的各个组件。它还允许我们包装对象并将它们打印到控制台，以便更深入地了解我们的功能中正在发生的事情。

## 快照测试

我们可以用酶做的事情之一是实现快照测试。这些测试允许我们看到一个组件自从我们上次测试以来是如何变化的。第一次运行它时，会自动生成一个 snapshots_folder 和 test.js 文件，其中包含被测试函数的快照，以便将来进行比较。

如果有问题的代码完全没有变化，我们只能通过测试。失败时，结果将包含“差异”以显示哪些代码行发生了更改。如果由于某种已知的原因，被测试的代码发生了更改，您可以从命令行键入-u 标志来更新快照。

一些人认为这种类型的测试应该谨慎对待，因为如果函数调用中有拼写错误或者 CSS 类被重新命名，它可能会对功能完整的应用程序产生假阴性。所以要注意这些情况。

## 浅与安装

在单元测试中，很容易看到关键字 shallow。这就是我们如何明确声明我们只想测试有问题的组件，而忽略它的任何子组件。这有助于利用隔离测试的原则。

Mount 通常用于集成测试，有点像 shallow 的反义词。在这种情况下，我们会仔细检查组件的子组件，并希望在模拟浏览器中执行被测试的代码。但是，不会有真实的渲染。

请记住，使用挂载的测试确实运行得较慢，因为您运行的是一个几乎完全没有 UI 的实时应用程序。在这种情况下，您需要在运行这个测试之后包含一个卸载或清理的方法。

## 嘲弄的

当我们谈到模拟一个真实的应用程序时，是时候引入模拟测试，也就是“间谍”了。这些是测试 API 请求的好方法。

测试这个功能可能是至关重要的，但是发出一个真正的 API 请求会降低我们的测试速度，并且可能会导致我们的数据库被意外操纵。使用模拟函数，我们可以在测试环境中调用 API，而无需实现函数的实际逻辑。

## 工装连体服

在部署之前，一般目标是测试 80–100%的代码。在进行了一些测试之后，您可能想知道在被覆盖的代码量中是否还有缺口。这就是工作服派上用场的地方。

Coveralls 生成一个报告，显示当前正在测试的应用程序的百分比。超级好用。你只需注册，将它同步到你的 GitHub 账户，然后在“添加回购”标签中搜索你的回购名称就可以打开它。

通过将 cypress 和 coverage 标志添加到 package.json 文件中的脚本，将 repo 配置为使用连体工作服:

```
"cypress": "node_modules/.bin/cypress open,
"test": "react-scripts test --coverage"
```

## 新找到的自信

测试增强了您对应用程序的信心，并通过发现错误显示了改进的机会，从而防止了进一步的复杂化。它们提供了对正在运行的进程的更透明的观察。刚开始可能会有点吓人，但是在确认你的假设后，你会对你的工作质量感觉好很多。

## 深潜

我强烈建议阅读上面提到的库和工具的文档。以下是一些有助于入门的资源…
[https://github.com/testing-library/react-testing-library](https://github.com/testing-library/react-testing-library)
[https://jestjs.io/](https://jestjs.io/)
[https://enzymejs.github.io/enzyme/](https://enzymejs.github.io/enzyme/)
[https://www . npmjs . com/package/@ wojtekmaj/enzyme-adapter-react-17](https://www.npmjs.com/package/@wojtekmaj/enzyme-adapter-react-17)
[https://kentcdodds.com/blog?q=testing](https://kentcdodds.com/blog?q=testing)
[https://www.freecodecamp.org/news/testing-react-hooks/](https://www.freecodecamp.org/news/testing-react-hooks/)
[https://medium . com/@ wyattsweet/testing-react-components-using-the-the](https://medium.com/@wyattsweet/testing-react-components-using-the-new-context-api-a1c553edc2fa)