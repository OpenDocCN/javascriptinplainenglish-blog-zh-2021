# 6 JavaScript UI 测试您需要避免的反模式

> 原文：<https://javascript.plainenglish.io/6-javascript-ui-testing-anti-patterns-you-need-to-avoid-f77f9902ef9e?source=collection_archive---------2----------------------->

## 探索最常见的不良实践以及如何实施正确的解决方案。

![](img/571370034e99dda6a91f69f502e544dd.png)

Photo by [Ruben Mishchuk](https://unsplash.com/@ruben244?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

随着越来越多的公司寻求为手工测试提供程序化的解决方案，测试自动化开始流行起来。

以美元计算，测试自动化领域预计将从 2019 年的 126 亿美元飙升至 2024 年的 288 亿美元。五年内增加了 100%以上。这种天文数字的增长将带来大量的机会。

不幸的是，新的机会也会导致不良测试实践的增加。在本文中，我们将介绍该领域中六种最常见的 JavaScript 测试自动化反模式，以便新手可以主动避免它们。

# 等待中…

现代的自动化框架，如 Cypress 和剧作家，使用隐式和显式等待，直到页面加载完毕，元素可见，或者元素可以被交互。通过给浏览器时间加载到可测试状态，这确保了测试不那么古怪和容易失败。一旦加载完成，测试可以继续执行。

一个正确使用等待的例子:

A comparison of waiting for selectors using Cypress and Playwright.

最常见的等待反模式是等待代码执行之间的显式超时。这样做会停止执行，然后在超时结束后继续执行。这最终会延迟测试的执行，并减慢整个测试的运行速度。

一个不正确使用等待的例子:

Comparing timeout waits using Cypress and Playwright.

不要编写上面的代码，而是使用内置的等待策略，比如等待元素或响应。考虑在上面的例子中点击“newHeadingButton”分派一个请求。我们可以等待请求完成，然后再采取下一步行动。

Proper waits using Cypress and Playwright.

# 把 UI 测试看得太重了

如果您或者您的工程师正在使用 UI 设置测试状态，您可能正在参与一个糟糕的测试实践。通过 UI 生成测试状态很麻烦，并且会导致测试失败。相反，利用现有的应用程序实现来创造密封的用户旅程。

当测试一个全新用户的应用程序登录时，不要通过 UI 构建一个新用户，然后尝试登录。您的测试不再是密封的，因为它现在测试两个用户旅程:

1.  新用户注册
2.  应用程序登录

相反，使用应用程序的 API 为新用户创建一个请求，然后尝试使用新构建的凭证登录。使用 Cypress 的内置请求库和别名可以毫不费力地做到这一点。

A Cypress request with a response alias.

使用 JavaScript HTTP 库的剧作家可以使用类似的模式，比如 [Requestify](https://www.npmjs.com/package/requestify) 。

A Playwright request using the Requestify NPM package.

# 独立于 CI 的测试

测试自动化中一个非常常见的反模式是独立于持续集成运行测试。直接的结果是失败的测试没有直接的影响。当在 CI 中运行时，一个失败的测试可以阻止一个构建被合并，从而避免潜在的失败到达验证或生产环境。此外，一个失败的测试可以作为一个开发团队将他们的注意力转向失败的号召。

测试工程师应该与站点可靠性或基础设施工程师一起工作，以确保自动化测试在每个构建或每个合并的基础上运行。如果一个工程团队决定采用这样的工具，当使用像 [Pre-Commit](https://pre-commit.com/) 这样的包时，测试甚至可以在提交或预推送时运行。

我个人建议团队使用预提交，在预提交时运行林挺/格式化，然后在预推送时运行单元测试。由于 UI 测试需要更长的时间，我会使用 Github Actions 或 Jenkins workflow 之类的东西在每次构建或每次合并的基础上运行它们。

# 行为驱动开销

我曾经是行为驱动开发(BDD)的大力支持者，以至于我为我过去工作过的两家公司编写了最佳实践标准。然而，我已经不再使用 BDD 了，因为我已经得出结论，这个过程提供了很少甚至没有价值，同时也是重构痛苦的来源。

像 Cucumber 这样的行为驱动的开发工具非常适合在梦幻场景中使用，在这种场景中，整个公司都已经接受了 BDD 的艺术。然而，经常是测试团队用小黄瓜写作，而业务的其他方面要么忽略实践，要么不做贡献。在这种情况下，BDD 失去了作为部门间协作工具的价值。这种做法没有使产品管理、开发和 QA 更加紧密，反而疏远了 QA。

移除 BDD 的另一个原因是编写和重构测试所涉及的开销。考虑一个用户旅程，其中一个普通用户导航到一个登录页面，提交有效信息，并检查是否成功。我们可以把它写在特写里。

```
// login.featureFeature: Application Login
    As a user,
    I would like to login to the application Scenario: Login with valid information
        Given we visit the login page
        When we submit valid credentials
        Then we should redirect to our profile page
```

现在我们需要一个 steps 文件。

Steps file for both Cypress and Playwright automation frameworks.

如果登录工作流不再重定向到个人资料页面会怎样？

现在，您必须分两步进行重构，而不是在没有 BDD 的情况下在一个位置进行重构:步骤和特性。BDD 最明显的痛点是这样一个事实，小的重构比完全不使用 BDD 要花两倍的时间来完成。您的测试旅程没有单一的真实来源，而是有两个独立的模块，它们必须保持同步才能正常工作。

你应该写更多的声明性用户旅程，而不是使用 BDD。

Declarative testing using Cypress and Playwright.

上面的旅程对读者(无论是测试人员、产品经理还是开发人员)来说都是足够明确的，测试需要一个用户，输入有效数据，并成功提交。不需要任何步骤、特性或复杂的开销，只需要简单的 JavaScript。

# 情况

测试工程师应该尽可能地从测试中删除条件逻辑，以减少错误。条件测试会产生不确定的测试，这些测试很难排除故障并放心运行。

我为一家需要测试第三方集成的公司工作。该测试的一部分是通过第三方登录，然后重定向到他们的应用程序。由于测试的古怪性质，验证状态被证明是不可预测的。他们实现了条件逻辑，试图在 before 步骤中处理它。

*   如果用户已登录，注销，然后登录
*   如果用户未登录，请登录

由于这种条件逻辑，测试是非常不可靠的。有时他们会通过，尽管大多数时候会彻底失败。在拆卸步骤中，我选择移除条件逻辑，支持 API 注销方法。用户总是必须登录(除非测试执行被手动中断)，这使得测试在运行时更加可靠。

工程师不应该使用条件逻辑流，而是应该尽可能地使用 API 来构建测试状态，无论是通过发出请求还是模仿响应。

让我们考虑一个正在进行 A/B 测试的示例应用程序。这个应用程序是一个书店，为 A 组显示一本书，为 b 组显示另一本书。

Response mocks with Cypress and Playwright.

现在，我们的测试是确定的和可靠的，因为我们使用 API 而不是试图通过 UI 来构建测试状态。

# 选择错误的选择器

通常，使用正确的选择器标准是一项困难的任务。测试自动化中一个常见的反模式是在构建页面对象或编写测试时使用非常脆弱的选择器。脆弱的选择器是那些可能由于实现重构而改变的选择器。不适当的选择器标准是使用非唯一的 id 和类，或者 Xpath。

Cypress 通过采用 JQuery `.first()`和`.last()`方法，以及用于 DOM 遍历的方法，如`.sibling()`和`.parent()`，特别减轻了一些痛苦。

```
// Cypress
cy.get('.chat-message').last();
```

建议通过添加定制的选择器来强化您的选择器方法，而不是依赖这些选择方法(除非您无法访问源代码)。

在大多数情况下，测试工程师应该与他们的开发团队同步，以确保唯一的选择器被添加到代码库中。这些包括选择器，如`data-id`、`data-test-id`、`data-cy`或它们的任何变体。它们可以像自动化框架中的任何属性一样使用。

Proper selector criteria using Cypress and Playwright.

# 摘要

我们现在可以识别并避免 JavaScript 测试自动化中最常见的六种反模式。请记住，这些并不是自动化测试世界中唯一的反模式。当你继续在这个行业工作的时候，你会注意到在灌输好的测试实践的时候要避免的其他模式。

# 资源

1.  "自动化测试市场."*市场研究公司*，[www . Market and markets . com/Market-Reports/automation-testing-Market-113583451 . html .](http://www.marketsandmarkets.com/Market-Reports/automation-testing-market-113583451.html.)
2.  "条件测试." *Cypress Documentation* ，2021 年 2 月 15 日，[docs . Cypress . io/guides/core-concepts/conditional-testing . html # Definition](http://docs.cypress.io/guides/core-concepts/conditional-testing.html#Definition)。
3.  “最佳实践。” *Cypress Documentation* ，2021 年 2 月 15 日，[docs . Cypress . io/guides/references/best-practices . html # select-Elements](http://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements)。

**乔纳森·汤普森**高级质量工程师，专注于测试自动化。他目前居住在北卡罗来纳州的罗利，与他的妻子和一个名叫温斯顿的戈德多德尔(Goldendoodle)住在一起。您可以通过 [LinkedIn](https://www.linkedin.com/in/jonathanmnthompson/) 与他联系，也可以通过 [Twitter](https://twitter.com/jacks_elsewhere) 或 [Github](http://github.com/ThompsonJonM) 关注他。