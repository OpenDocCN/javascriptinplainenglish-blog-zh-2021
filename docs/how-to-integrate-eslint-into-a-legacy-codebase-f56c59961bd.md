# 如何将 ESLint 集成到遗留代码库中

> 原文：<https://javascript.plainenglish.io/how-to-integrate-eslint-into-a-legacy-codebase-f56c59961bd?source=collection_archive---------11----------------------->

![](img/1e93f0e8ec8eaba5f4c9deab78558deb.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

对于一个新的 JavaScript 项目，我通常做的第一件事就是设置和配置 [ESLint](https://eslint.org/) 。ESLint 是一个静态代码分析器。它很棒，有两个原因:首先，它帮助你在一个开发团队中或作为一个单独的开发人员实施一致的编码风格——这不仅仅是关于代码美学，而是关于使代码更具可读性。第二，它可以在你写代码的时候发现代码中的错误，这样就不用花太多时间去绞尽脑汁、调试和挖掘堆栈跟踪了。软件开发是复杂的，ESLint 是可以让你的生活变得更简单的工具之一。但是 ESLint 是我首先设置的东西之一的主要原因是，随着你向项目中添加每一行代码，它变得越来越困难。

我最近不得不将 ESLint 整合到一个两年前的项目中，这是返回的报告:

```
✖ 5549 problems (3726 errors, 1823 warnings) 
  3130 errors and 1472 warnings potentially fixable with the `--fix` option.
```

简而言之，我的脑海中闪过一个想法:不值得花力气去整合 ESLint。当然，我不想花几个小时手动检查代码来修复一切。我本可以忽略这些错误，希望能够随着时间的推移一点一点地清除它们。但我无法忍受屏幕上的红色曲线，不确定团队中的每个人是否都会像我一样下定决心与它们抗争，尤其是在没有 CI 对它们指指点点的情况下。

我需要一种方法来确保代码风格会随着每次新的提交而逐渐改进。如果我能确保我们接触的每个文件都被清理干净呢？当然，有一种方法，在 Git 的帮助下，这是可能的:

```
git diff main --name-only --diff-filter=ACM \
  | grep -E '\.(vue|js)$' \
  | xargs node_modules/.bin/eslint
```

该脚本将只 lint 主分支中已更改的文件。让我们一行一行地研究这个命令:

*   将列出所有与主文件相比被添加、复制或修改的文件的名称。
*   `grep -E '\.(vue|js)$'`将过滤列表中以`.vue`或`.js`结尾的文件。您必须对此进行调整，以匹配您在 ESLint 设置中定义的文件模式。
*   最后，`xargs node_modules/.bin/eslint`将把文件作为参数传递给 ESLint。

我将此作为脚本保存在`package.json`文件中，并将其添加到 [Github Actions](https://github.com/features/actions) 的工作流中。现在，每当有人接触项目中的文件时，他必须在它通过 CI 之前清理它。随着时间的推移，我们正在实施积极的变革！

*原载于 2021 年 9 月 18 日*[*https://stricker . digital*](https://stricker.digital/posts/integrating-eslint-into-a-legacy-codebase/)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)