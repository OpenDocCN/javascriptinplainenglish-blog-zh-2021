# 为什么永远不应该在 CI/CD 管道中使用“npm install”

> 原文：<https://javascript.plainenglish.io/why-you-should-never-use-npm-install-in-your-ci-cd-pipelines-da0b89346d8d?source=collection_archive---------2----------------------->

用非常简单的术语解释何时使用`npm ci`和`npm install`。

![](img/4a1b75d3e6e7c9cc65178f83ba0c0cd6.png)

Photo by [Cookie the Pom](https://unsplash.com/@cookiethepom) on [Unsplash](https://unsplash.com/)

当开始一个新项目或克隆一个现有项目时，大多数人运行`npm install`或简写版本`npm i`，这很好。但是很有可能你已经无意中发现了一个叫做`npm ci`的类似命令。

我经常在常规的 CI/CD 管道中看到`npm install`命令。起初听起来不错的东西可能会导致相当多的问题。`npm ci`命令中的`ci`代表“*全新安装”*或者如果对您有帮助，您也可以使用*“持续集成”*。因此，很明显，在您的管道中应该优先使用`npm install`。但是在你盲目听从我的建议，在你所有的管道中使用`npm ci`之前，让我们快速检查一下有什么不同。

尽管下面的定义并不完全符合 NPM 的官方文档，我还是试图用包含最常见用例的超级简单的术语来解释它们。

## npm 安装

它用于向您的`package.json`和`package-lock.json`添加依赖项，从而修改您的依赖项并将其安装到您的机器上。这对于开发来说绝对没问题，但是它不应该在您的管道中发生。你**不想在你的管道中添加/修改任何文件。**

## npm ci

该命令仅依赖于`package.json`和`package-lock.json`中列出的依赖定义，并安装它们。但是它不会对你的文件做任何修改。另外，如果两个 JSON 文件中的定义没有 100%一致，这个命令会抛出一个错误，这也意味着**锁文件必须存在**。因此，请务必将它添加到您的 VCS 中。除此之外，顾名思义，它会进行“全新安装”，这意味着任何现有的`node_modules`文件夹都会被删除。

## 好吧，但是为什么这很重要？

其实挺简单的。每当您启动 CI/CD 管道时，您都不希望由于不匹配的`package*.json`文件而导致任何不一致，这可能会导致与您本地的代码库不同。此外，您不希望在使用已经填充的`node_modules`文件夹时出现任何副作用。

想象一下，如果你的开发人员只提交了`package.json`而没有提交`package-lock.json`会发生什么。如果 JSON 文件不再对齐，管道将不能确定现在使用哪个包。此外，管道可能会突然使用开发人员本地机器上没有的一些包，因此典型的*“但它在我的机器上工作”*可能会再次出现。

您在 CI/CD 管道中想要的是不受任何副作用影响的高度一致、可重复的步骤。因此，运行特定管道的频率并不重要。当提供相同的参数(可选)时，它应该总是产生相同的结果，不管它是林挺、构建、测试还是部署您的软件。

## 结论

我希望我能向您展示为什么在您的管道中使用`npm ci`命令和使用“普通”`npm install`引用是如此的重要。

总结一下:

*   当你在本地机器上工作并想要安装/添加/修改依赖项时，使用`npm install`。
*   当您在 CI/CD 管道上运行并希望提供可重复步骤的一致性时，请使用`npm ci`。

感谢您花时间阅读我的文章。

## 你想联系吗？

如果你想联系我，请在 LinkedIn 上联系我。

另外，请随意查看我的书籍推荐📚。

[](https://mr-pascal.medium.com/my-book-recommendations-4b9f73bf961b) [## 我的书籍推荐

### 在接下来的章节中，你可以找到我对所有日常生活话题的书籍推荐，它们对我帮助很大。

mr-pascal.medium.com](https://mr-pascal.medium.com/my-book-recommendations-4b9f73bf961b) [](https://mr-pascal.medium.com/membership) [## 通过我的推荐链接加入 Medium—Pascal Zwikirsch

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

mr-pascal.medium.com](https://mr-pascal.medium.com/membership)