# 带 JavaScript 的 Monorepo

> 原文：<https://javascript.plainenglish.io/monorepo-with-javascript-9605f8354b11?source=collection_archive---------9----------------------->

## “全栈”JavaScript 项目的开发策略

![](img/2933a4405ce20c3d2ad74f733caf5319.png)

Photo by [Gabriel Heinzer](https://unsplash.com/@6heinz3r?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

管理多个存储库可能会令人沮丧，尤其是当您涉及到这些存储库的时候。例如，**回购 A** 和**回购 B** 在业务逻辑上可能有 30%的相似性。当你需要修理或改变它的时候，你需要做两次。

在我们开始之前，您可能需要看看这篇文章，以便有一个更清晰的思路:

[](https://betterprogramming.pub/3-libraries-i-use-in-most-javascript-frontend-projects-555387be69c) [## 我在大多数 JavaScript 前端项目中使用的 3 个库

### 提升您的 web 应用程序的性能

better 编程. pub](https://betterprogramming.pub/3-libraries-i-use-in-most-javascript-frontend-projects-555387be69c) 

# 什么是 monorepo？

与多回购不同，单回购是存储多个项目代码和资产的单一存储库。允许您在不同的项目之间共享业务逻辑。

想象一下使用全栈 JavaScript: *桌面* — ElectronJS、*后端* — NodeJS、*移动应用* — React Native、*管理门户* — ReactJS、 *Web 应用* — SvelteJS。您只需要一个存储库来存储所有这些项目。

文件夹结构如下所示:

```
apps/
├── admin
│   └── package.json
├── api
│   └── package.json
├── desktop
│   └── package.json
├── mobile
│   └── package.json
└── web
    └── package.jsonpublic/
├── styles
│   └── global.css
├── images
│   └── a.png
|   └── b.png
└── favicon.icoshared/
└── utils
    └── index.ts
```

目前有 [lerna](https://lerna.js.org/) ， [pnpm](https://pnpm.io/) ， [Bazel](https://bazel.build/) 等。，是 JavaScript monorepo 的构建工具。然而，在本文中，我将仅使用`pnpm`作为示例。

# 谁在使用 monorepo？

1.  **像谷歌、脸书、推特、微软等大公司。正在使用 monorepo，他们的代码库非常庞大。**
2.  开源库通常使用 monorepo 作为文档站点和插件等。然而，有时也可能是多次回购。

# 优点和缺点

Monorepo 很好，但有时会适得其反。

## 优势

1.  **代码一次—** 同样的业务逻辑不用多次编写。编写一次代码，在同一个存储库中的多个项目之间共享。
2.  **简化的依赖管理** —在多回购中，你可能需要多次下载同一个第三方依赖，多次发布包；Monorepo 允许您在一个地方一次性管理依赖性。
3.  **原子变化** —你可以改变一段代码，影响多个项目。例如，当重构一个**共享的**函数时，它也会影响其他项目。

## **缺点**

1.  **访问控制** —用户可以对所有项目进行读取、写入和删除。例如，John 是前端 Web 开发人员，他应该只为 React web 应用程序工作，但是他也可以访问后端、桌面等。
2.  **需要更多存储空间** —它适合从事大多数项目的全栈开发人员。然而，如果在 monorepo 中有五个项目，而你只做一个，那么其他四个项目就是在浪费你的存储空间。
3.  **原子变化**——是的，这可能既是优势也是劣势。重构一段代码要么成功，要么彻底失败。你可能会搞砸别人的项目。
4.  **IDE 的自动导入**——总是仔细检查你的 IDE 的自动导入。有时它会从其他项目中导入模块，这些模块不会包含在产品中。请不要依赖 IDE 的智能重构，因为 JS 不是类型安全的语言；这会制造一场噩梦。
5.  **版本控制—** 当您有一个大团队参与其中时，跟踪提交日志将会非常困难。

不要盲目跟风。如果上面提到的优势是你所寻找的，你应该考虑转投 monorepo。否则，坚持使用多重回购。

点击查看 Github repo [示例。](https://github.com/OysterD3/js-monorepo-example)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)