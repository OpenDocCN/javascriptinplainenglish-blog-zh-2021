# 在 2021 年发布一个类型脚本库

> 原文：<https://javascript.plainenglish.io/publishing-a-typescript-library-in-2021-751842afc10f?source=collection_archive---------17----------------------->

上一次想发布 npm 包是在 2018 年。它是一个 React 库，提供了创建表单的组件。当时发布这样一个库并不容易。你自己要处理的事情太多了，尤其是打字稿。

假设你已经熟悉了 webpack，你会想:哈，这应该很容易，我可以利用我的知识，把我的库和 webpack 捆绑在一起，就像我的 webapps 一样。但是后来你突然听说了这个新的产品:Rollup，它似乎在捆绑库方面做得更好。所以你必须学习一个新的捆扎机，而且你自己还有很多事情要做。

很好，我们现在快进到了 2021 年。镇上来了一个新玩家，让我们的生活变得更加轻松**。我给你介绍一下 [tsdx.io](https://tsdx.io)**

![](img/035e4d2baaa431ab73b3204ec53d560e.png)

# 用于 TypeScript 包开发的零配置 CLI

TSDX 的目标是消除我上面提到的所有痛点，让您专注于开发下一个库，而不是“在配置上再浪费一个下午”。哦，天啊，他们在这方面做得非常好。实际上，我找不到 TSDX 首字母缩写词的含义，但我认为它代表 TypeScript 开发人员体验——这无疑增强了很多。

TSDX 附带 Rollup under the hood，并为您提供开发和捆绑现代 NPM 包的最佳实践。它经过了很好的测试，TSDX 背后的团队是 [formium](https://formium.io/) ，他们也在开发流行的 React forms 库 [formik](https://github.com/formium/formik) ，它也利用了 TSDX 的功能。

TSDX 附带的最佳实践对于大多数项目来说应该是完美的。即使你需要做一些调整，这个过程也很简单。例如对于[我们的库](https://github.com/snappify-io/integration)，我们希望使用更少的代码，而不是编写普通的 css，稍后我将向您展示如何根据您的需求调整 TSDX 配置。

# 创建新的 TSDX 项目

用 TSDX 创建一个新的 TypeScript 库就像键入`npx tsdx create mylib`一样简单。该命令将引导您完成安装过程，之后您将看到一个打包的文件夹，您可以在其中开始开发您的新库。

TSDX 有三种不同的项目类型，您必须从中选择一种:

*   一个普通的 TypeScript 项目(我们这样做是因为我们不想包含任何外部库，也不依赖 React)
*   如果你想创建一个反应库，选择这个选项。TSDX 负责创建一个现成的 React 库所必须做的所有事情
*   `react-with-storybook` -与之前的选项相同，但包括故事书设置

## 开始

TSDX 使开发你的图书馆超级容易。你只需输入`npm start`，你的项目就会在观察模式下启动。您的库的入口点是`index.ts`(或者对于 React 项目是`index.tsx`)。因此，当你在相应的文件中进行修改时，TSDX 会检测到并为你重建库，从而实现超级平滑的开发过程。

## 运行测试

TSDX 还为您提供了 Jest 设置，因此您可以以`*.test.ts(x)`文件的格式编写测试，如果您键入`npm test`，Jest 将自动识别并执行它们。

## 在本地试试你的图书馆

当然，在将你的库发布到互联网上之前，你也想在本地试用一下。为此，npm 命令`npm link`非常方便。

1.  进入你的库文件夹`cd ~/projects/mylib`
2.  键入`npm link`创建库的本地符号链接
3.  切换到您想要包含您的库的项目文件夹`cd ~/projects/myproject`
4.  键入`npm link myproject`安装本地版本的库。如果您对您的库进行更改并重新构建它，这也将自动刷新(如果您在库项目中执行`npm start`，这将由 watch 命令自动完成)

确保使用 package.json 中的完整库名(不是文件夹名)执行 npm 链接。在我们的例子中，我们必须键入`npm link @snappify/integration`,因为我们的包包含在我们的 npm 组织中。

# 调整默认配置

现在您应该准备好开发您的库并测试它，直到您可以发布它。但是，如果默认的 TSDX 不能满足您的需求，您需要调整配置，该怎么办呢？

如果您想要调整构建配置，您必须在您的库文件夹的根目录下创建一个`tsdx.config.js`文件。在它们中，您将导出一个包含`rollup`函数的对象，该函数接收默认汇总配置作为第一个参数，并期望修改后的配置作为返回值。

在这里你可以看到我们的配置，我们增加了写得更少而不是 css 的可能性:

```
const less = require('rollup-plugin-less');

module.exports = {
  rollup(config) {
    config.plugins.push(
      less({
        insert: true,
        output: false,
      })
    );
    return config;
  },
};
```

# 添加有用的 GitHub 工作流程

对于一个严肃的图书馆来说，一套好的 GitHub 工作流是很有帮助的！例如，您希望在每次提交时执行测试或 linter，或者如果某个更改导致您的包大小大幅增加，您希望有一个大小限制机器人对您的 pull 请求进行评论。

自由地看一看[我们的 GitHub 工作流程](https://github.com/snappify-io/integration/tree/main/.github/workflows)，在那里我们为我们的开源库设置了所有这些。大小限制的配置可以在 [our package.json](https://github.com/snappify-io/integration/blob/main/package.json#L37) 中找到。

# 发布您的库

所以你知道一切都根据你的需要进行调整，有足够的时间来开发你的库并在本地试用。你确信:你的图书馆已经准备好被公众消费了！那么下一步是什么？在安装过程中，TSDX 确保在你的`package.json`中添加一个合适的`prepare`脚本。每次你执行`npm publish`的时候，准备脚本就会自动执行——所以每次你想发布一个新版本的包的时候。

TSDX 在发布之前所做的是创建一个新的 TSDX 版本，这也确保了在您发布新版本之前该版本不会失败。所以你基本上只需要运行`npm publish`(带有你想要的相应参数，例如，它是否应该公开发布)就可以了！

# 摘要

当我们想为我们的产品创建一个 npm 包时，我有点害怕，因为我记得几年前创建这样一个库的所有困难。我听说过 Timo Lins 的 react-hot-toast，并问他是否有一些开始创建 TypeScript npm 包的技巧。

他指给我 TSDX，我开始玩它，很快就迷上了。默认的最佳实践是可行的，正如网站所说:你可以专注于开发你的库，而不是试图找出正确的配置。

我要感谢 TSDX 背后的整个团队创建了这个令人敬畏的工具，并从创建 TypeScript 库的痛苦中解脱出来。🎉

*更多内容请看*[***plain English . io***](http://plainenglish.io)