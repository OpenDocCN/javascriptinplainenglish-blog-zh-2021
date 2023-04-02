# 了解如何使用 Cypress 编写端到端自动化

> 原文：<https://javascript.plainenglish.io/learn-how-to-write-end-to-end-automation-using-cypress-ed2f6bcbdba1?source=collection_archive---------11----------------------->

![](img/5b25c65dc0acebb8188c5f4d63542694.png)

Photo by [Paul Hanaoka](https://unsplash.com/@plhnk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 问题是

自动化测试是高质量软件开发的关键部分。每一级别的自动化测试都有一些该做和不该做的事情，以及优缺点。

如果您不熟悉自动化的不同层次，您可以从测试一个代码单元(例如一个类)，来测试这些单元的集成(例如多个类)，到整个系统。测试是关于风险和选择正确的妥协。考虑到这一点，您应该尝试拥有一个相当平衡的测试套件，这样您就不会以连续几天运行自动化而告终，并且您可以拥有一个快速可靠的反馈循环。

在这篇文章中，我将重点介绍一个测试框架，该框架目前有助于从 web 浏览器测试整个系统。这些类型的测试通常被称为 UI 测试、端到端测试或系统测试。虽然系统测试很棒，因为它们是从用户的角度来测试系统的，但是也有一些问题。

*   可靠性:这些类型的测试往往会失败很多，因为你需要启动整个系统，而且非常脆弱。任何轻微的停顿，没有正确的重试级别，都可能导致测试失败。
*   **排除故障成本高昂**:如果没有适当的日志记录和监控，这些类型的测试可能很难排除故障。举个例子，一个登录页面不起作用。确切的问题是什么？会不会是前端问题？网络问题？或者，后端问题？
*   **持续时间**:因为他们需要一个 UI 和后端工作，可能会有复杂的设置和长时间运行的任务。在许多情况下，这可能导致每次测试需要几分钟。
*   可维护性:对于这些类型的测试，你倾向于使用 CSS 选择器。选择错误类型的选择器可能会导致测试失败，即使功能上没有任何问题。

在这篇文章中，我将介绍一个叫做 Cypress 的 UI 测试框架。Cypress 是一个非常易用的端到端测试框架。如果你以前用过基于 Selenium 的测试框架，Cypress 不使用 Selenium。他们还声称它“与应用程序运行在同一个运行循环中”

根据我到目前为止的经验，使用 Cypress 编写我的端到端自动化已经产生了易于编写、易于调试、快速和更可靠的测试。最后，没有一个 UI 测试框架是防弹的，在选择自动化什么、测试的前提条件是什么以及应该多长时间运行一次这些测试时，你应该真正尝试做出负责任的选择。

## 设置项目

让我们从运行这些测试所需的设置开始。在这篇文章中，我们将创建一个全新的项目，只包含这些测试。

你要做的第一件事是创建一个全新的 npm 项目并安装 Cypress。

```
npm init
npm install --save-dev cypress@latest
```

现在，你的项目结构应该有一个`package.json`文件、一个`package-lock.json`文件和一个`node_modules`文件夹。

下一步是创建 cypress 配置文件。在项目的根目录下，添加一个名为`cypress.json`的文件，其内容如下。

```
{
  "integrationFolder": "tests",
  "defaultCommandTimeout": 15000,
  "pageLoadTimeout": 30000,
  "video": true
}
```

让我们先来看看这些值分别代表什么。

1.  `integrationFolder`:这是你所有测试的文件夹。在这里，我们希望所有的测试都在项目根目录下的`tests`文件夹中。您可以输入任何值，只要确保该文件夹存在并且包含您的测试。
2.  `defaultCommandTimeout`:这是特定命令失败所需的时间(毫秒)。例如，如果你点击一个元素，如果这个元素没有出现在屏幕上，它会在这段时间内不断重试。
3.  `pageLoadTimeout`:这是测试框架等待页面成功加载所需的时间(毫秒)。
4.  `video`:将此项设置为 true 将启用所有测试的视频记录。

寻找更多的配置标志？你可以在这里找到更多信息[https://docs . cypress . io/guides/references/configuration . html](https://docs.cypress.io/guides/references/configuration.html)

## 编写您的第一个测试

![](img/317bf1e410817199303316b88763ac4e.png)

Photo by [James Pond](https://unsplash.com/@jamesponddotco?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用 Cypress 编写测试非常容易。首先，在`tests`文件夹中创建一个新的 JavaScript 文件(或者在`integrationFolder`文件夹中设置的任何文件夹)。

每个测试都由一个`describe`块包装，这些块中的测试由`it`块包装。

```
describe('my first test suite`, () => {
    it('my first test', () => {

    });
});
```

现在，在编写我们的第一个测试之前，让我们复习一下最基本的命令。这些 Cypress 命令将帮助您完成编写 UI 测试自动化时需要完成的大部分任务。

## 访问特定的 URL

几乎所有测试的第一步都是访问一个特定的 URL。这将负责打开浏览器并导航到您提供的 URL。为此，您将使用`visit`命令，并将要访问的 URL 作为参数传递。

```
cy.visit('url to visit...');
```

## 检索元素

如果您想对 DOM 中的元素执行操作，您总是需要首先从 DOM 中检索元素。例如，如果您的 HTML 页面如下所示:

```
<div id="the-item">Text goes here</div>
```

您将需要通过 ID 进行选择。这将产生一个选择器`#the-item`。

Cypress 提供了一种从 DOM 中检索元素的方法。这个方法叫做`.get`,你提供一个 CSS 选择器作为参数来惟一地标识这个元素。

在本例中，您将使用下面的代码来检索元素并在测试中对其执行操作。

```
cy.get('#the-item')
```

## 对 DOM 元素的操作

如果您想要验证一个元素是否可见，您将想要使用`should`命令并传入以下参数之一:

1.  当你想验证一个元素对用户是否可见时的`'be.visible'`参数。
2.  `'not.be.visible'`参数，用于验证一个元素是否对用户不可见。

```
cy.get(selector).should('be.visible');
cy.get(selector).should('not.be.visible);
```

您还可以使用 Cypress 执行其他基本任务。这些是在输入元素上键入、验证元素是否包含特定的文本或点击元素。

如果你想在一个输入元素上打字，你将需要首先得到这个元素，然后使用`type`函数。作为`type`函数的一个参数，您需要传递想要在元素上输入的文本。

```
cy.get(selector).type(text);
```

为了验证一个元素是否包含文本，您需要使用`contains`方法。您需要将想要验证元素包含的文本作为参数传递。

```
cy.get(selector).contains(text);
```

最后，如果你想点击一个元素，你需要调用`click`方法，它不需要你为这个动作传递任何参数。

```
cy.get(selector).click();
```

## 将一切联系在一起

到目前为止，您可能已经意识到，您的测试自动化将由命令的组合组成，而不是单一的命令。

例如，您可能希望访问一个页面，在表单上键入一些内容，单击 submit 按钮，并验证屏幕上元素的文本。这个简单的场景将按以下方式编写:

## 运行测试

我们将讨论的最后一个主题是，如何运行您的测试？作为 package.json 文件的一部分，向`scripts`对象添加以下脚本。值`cypress.json`是您之前创建的配置文件。

```
"test" : "cypress run --config-file=cypress.json"
```

如果您想要利用 Cypress 的用户界面，并且能够运行特定的测试并查看测试运行的细节，那么添加这个脚本。

```
"test:open”: “cypress open -C cypress.json”
```

希望您已经对这个伟大的测试自动化框架有了更好的理解。尽情享受吧！

**资源**

[](https://www.cypress.io/how-it-works/) [## 端到端测试框架

### 我们觉得是时候解决它了。选择一个框架，选择一个断言库…

www.cypress.io](https://www.cypress.io/how-it-works/) 

*在* [***获取更多内容***](https://plainenglish.io/)