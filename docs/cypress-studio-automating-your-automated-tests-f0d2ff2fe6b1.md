# 使用赛普拉斯工作室自动化您的自动化测试

> 原文：<https://javascript.plainenglish.io/cypress-studio-automating-your-automated-tests-f0d2ff2fe6b1?source=collection_archive---------9----------------------->

![](img/3b1a56a34a2bd708e7c1799f60934ef2.png)

我从事网络开发已经有一段时间了，我反复面临的一个难题是前端自动化测试。我使用过 Jest 和 Mocha，虽然它们很有用，但它们不会让人觉得我的应用程序测试得不够好

幸运的是， [Cypress](https://docs.cypress.io/guides/overview/why-cypress.html#In-a-nutshell) 已经在最近上市，提供了一个端到端测试的解决方案。什么是端到端测试？简而言之，赛普拉斯会为你点击你的网络应用程序，如果你愿意，会将实际的网络请求发送到你的服务器或数据库，并等待响应。太神奇了。

写了几个柏树测试后，我对我的结果很满意，但是注意到编写测试设置来点击我的用户界面仍然很麻烦。**然后我找到了 Cypress Studio，这是一种自动化(大部分)自动化测试编写的方法。**

# 赛普拉斯工作室

[赛普拉斯工作室](https://docs.cypress.io/guides/core-concepts/cypress-studio.html#Extending-a-Test)是赛普拉斯的一项实验性功能，可以帮助您为自己编写测试。[通过最少的配置设置](https://docs.cypress.io/guides/core-concepts/cypress-studio.html#Using-Cypress-Studio)、**柏树工作室将允许你点击你的界面，它将为你生成元素选择器。**

例如，我编写了一个测试，以确保当我单击一个按钮时，会出现一个特定的模式。[遵循 Cypress Studio 文档](https://docs.cypress.io/guides/core-concepts/cypress-studio.html#Extending-a-Test)后，我编写了一个测试外壳，并单击了 UI 中的保存按钮。在完成我的命令后，我回到我的测试中，发现赛普拉斯已经为我生成了选择器代码！(它还会生成这些注释分隔符)。

**我所需要做的就是写断言语句，我完成了。(**如果有一天我们不需要编写自己的断言，我们可能需要开始寻找网络开发人员的新工作)

这是一个简单的例子，选择器不是很复杂，但是它为我节省了一些击键和脑力，只需点击 UI 中的按钮，而不是写出整个设置。如果您有多个命令，Cypress 会将它们全部记录下来，所以您可以单击多个按钮，让它为您生成选择器。

# 结论

自动化测试已经取得了长足的进步，虽然还有很多工作要做，但赛普拉斯已经取得了巨大的进步，赛普拉斯工作室就是其中的佼佼者。享受让你的电脑帮你写自动化测试吧！

*阅读更多在*[***plain English . io***](https://plainenglish.io/)