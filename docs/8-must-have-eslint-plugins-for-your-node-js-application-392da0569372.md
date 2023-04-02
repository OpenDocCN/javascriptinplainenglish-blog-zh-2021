# Node.js 应用程序的 8 个必备 ESLint 插件

> 原文：<https://javascript.plainenglish.io/8-must-have-eslint-plugins-for-your-node-js-application-392da0569372?source=collection_archive---------9----------------------->

![](img/f1183e70196386ba472fc2b130abeb81.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

2021 年 6 月 23 日发布

在您的项目中使用 ESLint 是一种从您的 pull 请求中减少那些低价值、主观的代码风格注释的简单方法。

它还将通过静态分析来防止 TypeScript 和 JavaScript 中的真正错误。

我将解释为什么在你的应用程序中使用 ESLint 如此重要，我将描述我总是添加到每个新 Node.js 应用程序中的插件。

# 为什么我在每个项目中都使用 ESLint

我在所有的专业工作中使用 ESLint，以确保整个团队的一致性，并确保我们正在编写某种程度上标准的 TypeScript/JavaScript。

我也在我所有的个人项目中使用它，因为它就像是在我每次提交代码时有一个额外的高级开发人员在背后看着我。

这是我在所有项目中使用的插件列表，我添加了一些关于我觉得没用的插件的附加说明。

# 消除主观争论

大多数 ESLint 规则是主观的代码风格的类型规则。一旦你锁定了一个设置，ESLint 就会执行它。这是这些类型的风格规则的主要好处。如果你在 PRs 中得到很多“nit”类型的评论，只需添加一个 ESLint 规则来阻止它们。

如果有人不同意某条规则，那没问题——事实上，这应该受到欢迎，因为这表明他们关心代码库。要解决这些规则更改请求，只需让团队投票，如果投票成功，想要更改规则的人可以继续，但他们也必须使所有现有的代码符合要求。

这通常不是 ESLint 自动修复或者只是搜索和替换的大问题。

在你的代码库中保持这样的一致性对于可读性、质量和新开发人员的加入是非常重要的。所使用的特定代码风格并不那么重要，大多数开发人员在跨越代码库时会在几天或更短的时间内进行调整。但是对于特定的代码库，它们应该是一致的。

# 防止客观代码气味

除了风格和代码的一致性，这些 ESLint 插件中的一些会客观地改进你的产品，防止真正的 bug。它们对特定的库执行静态分析，即使像 TypeScript 这样的工具也检测不到。sonar 插件特别有一些有趣的代码气味检测，值得一试。

这些类型的规则通常在客观上是有益的，并且应该被使用，除非它们是多余的，因为像 typescript 这样的东西已经覆盖了它们，它们过于严格(付诸表决)，或者它们与您的代码不相关。

# 学习和跟上时代

当你激活我在这里列出的所有插件时，你将在每次林挺运行中对你的代码进行 100 次测试。您可以有效地让专业的 JavaScript 开发人员与您结对编程，在您构建软件时建议编写软件的最佳方式。

期望一个工程师知道所有这些东西并记住应用到每个提交中是不现实的。

最棒的是，这些插件正在积极开发中，因此它们将随着行业的学习和改进而更新。

将这些 ESLint 插件添加到您的项目中所获得的价值相当于为您的团队添加了一个额外的 dev 和一个额外的 QA。

# 8 个必备的 ESlint 插件

# 1.eslint-插件-独角兽

独角兽真是太棒了！这是一个帮助 JavaScript 项目的各种规则的列表。例如，如果你正在处理一个字符串列表，Unicorn 会提醒你使用`array.includes`而不是`some`或`find`。有太多令人敬畏的规则在这里一一列出，所以检查他们的文件。这个插件是必备的！

Unicorn 会定期更新，这是一个了解 Javascript 世界最新动态的好方法。例如，我最近了解到关于从 Unicorn 导入节点库的更加明确的`node:`方案。

```
import fs from 'fs'

// Vs

import fs from 'node:fs'
```

在 unicorn 中有一些规则，我会像缩写一样禁用或更改。如果你使用 NestJS 或 Express，你将在你的控制器上使用缩写。以下是我的一些残疾人独角兽规则。

```
"unicorn/no-fn-reference-in-iterator": "off",
  "unicorn/no-array-for-each": "off",
  "unicorn/no-null": "off",
  "unicorn/consistent-destructuring": "off",
  "unicorn/no-array-reduce": "off",
  "unicorn/prefer-spread": "off",
  "unicorn/no-array-callback-reference": "off",
  "unicorn/consistent-function-scoping": "off",
  "unicorn/no-useless-undefined": "off",
  "unicorn/prevent-abbreviations": [
      "error",
      {
          allowList: { Param: true, Req: true, Res: true },
      },
  ],
```

明白了:【https://github.com/sindresorhus/eslint-plugin-unicorn】T4

# 2.eslint-插件-导入

如果你对模块导入做了任何粗略的操作，这个插件会警告你。如果使用 TypeScript，请确保添加了 TypeScript 的推荐规则，以免发生冲突。

```
extends: [
        "plugin:import/errors",
        "plugin:import/warnings",
        "plugin:import/typescript", // this one
    ],
```

另外，设置 TypeScript 的解析器选项。

```
settings: {
        ["import/parsers"]: { "@typescript-eslint/parser": [".ts", ".tsx"] },
        ["import/resolver"]: {
            node: {
                extensions: [".ts"],
            },
        },
    },
```

TypeScript 将会为你找到任何未解决的模块，但是这个插件对于防止错误仍然是有用的。

明白了:[https://github.com/benmosher/eslint-plugin-import](https://github.com/benmosher/eslint-plugin-import)

# 3.@ typescript-eslint/eslint-plugin

如果你在你的项目中使用 TypeScript，这个插件是必须的。只要确保按照自述文件中的说明正确设置了 TypeScript 解析器。

这里有 50 多条规则，所以你必须自己阅读文档。默认的推荐规则集非常好，但是如果您将它添加到一个现有的项目中，您可能会有太多的错误。暂时禁用最坏的规则，努力重构问题。

您应该为您的项目和组织配置一个命名约定规则。熟悉这条规则并设置它而不是关闭它是值得的。这里有一个例子:

```
"@typescript-eslint/naming-convention": [
            "error",
            {
                selector: "default",
                format: ["camelCase"],
            },
            {
                selector: "variable",
                format: ["PascalCase", "UPPER_CASE"],
                types: ["boolean"],
                prefix: ["is", "should", "has", "can", "did", "will"],
            },
            {
                selector: "variableLike",
                format: ["camelCase", "UPPER_CASE", "PascalCase"],
            },

            {
                selector: "parameter",
                format: ["camelCase"],
            },
            {
                selector: "memberLike",
                modifiers: ["private"],
                format: ["camelCase"],
                leadingUnderscore: "forbid",
            },
            {
                selector: "typeLike",
                format: ["PascalCase"],
            },
            {
                selector: "property",
                modifiers: ["readonly"],
                format: ["PascalCase"],
            },
            {
                selector: "enumMember",
                format: ["UPPER_CASE"],
            },
        ],
```

获取:[https://github . com/typescript-eslint/typescript-eslint # readme](https://github.com/typescript-eslint/typescript-eslint#readme)

# 4.eslint-插件-eslint-注释

这是一个 meta ESLint 插件，但是非常有用。这将有助于您获得描述 ESLint 指令的优秀注释，如:

```
/*eslint-disable no-undef */
```

特别是，它会在您重构某个东西之后或者当您忘记重新启用某个规则时发现无用的忽略。这非常值得添加到您的项目中。

您可能希望允许对整个文件禁用规则。我发现阻止完全文件规则忽略太严格了。

```
"eslint-comments/disable-enable-pair": [
     "error",
     { allowWholeFile: true },
 ],
```

获取:[https://github . com/mystic ea/eslint-plugin-eslint-comments # readme](https://github.com/mysticatea/eslint-plugin-eslint-comments#readme)

# 5.eslint-plugin-sonarjs

这个插件检测代码闻起来像重复的函数，重复的字符串用法，或者带有太多条件的 switch 语句。

SonarJS 中一个非常有趣的规则是试图防止代码块表现出太多的认知复杂性。这是一种基于圈复杂度的特殊声纳测量。这里有更多的细节:【https://www.sonarsource.com/docs/CognitiveComplexity.pdf】T2

在这个规则集中有太多的规则需要浏览，但是 sonar 的 js 插件非常有用，你应该去看看。

明白了:【https://github.com/SonarSource/eslint-plugin-sonarjs】T4

# 6.eslint-插件-jest

jest ESLint 插件是一个非常值得添加到你的代码中的插件。没有它，我在考试中会犯很多错误。例如，您知道应该返回异步期望吗？

```
expect(myResult).resolves.toEqual(expected) // this is wrong
return expect(myResult).resolves.toEqual(expected) // this is correct
```

如果你不返回，你会得到一个悬挂的运行，这将减慢一切。

有时我会不小心这样做我的断言:

```
expect(myResult === expected)
```

这不会导致错误，但是它根本不会像预期的那样断言您的测试用例。你会拿到通行证的！

jest ESLint 插件将防止这些非常危险的错误和更多。

明白了:[https://github.com/jest-community/eslint-plugin-jest](https://github.com/jest-community/eslint-plugin-jest)

# 7.eslint-plugin-nestjs-typed

无耻的塞在这里，因为我写了这个插件。我在我所有的后端 web 项目中使用 NestJS，所以我总是把这个插件添加到我的项目中。

eslint-plugin-nestjs-typed 将提醒您模块中没有提供的任何可注入服务。它将静态地这样做，而不是等待 NestJS 运行时。

如果您使用 swagger，它会提示您为大多数场景应用正确的装饰器，以确保您在 swagger 上运行的任何代码都能生成正确的模型。

如果你用 NestJS 的话就去看看吧！

获取:[https://github . com/darraghoriordan/eslint-plugin-nestjs-typed](https://github.com/darraghoriordan/eslint-plugin-nestjs-typed)

# 8.eslint-插件-承诺

这个插件至少对一个规则有用。它迫使你总是从一个承诺或`then()`返回一个值。TypeScript ESLint 插件已经涵盖了该插件提供的许多其他规则。TypeScript 和 Unicorn 涵盖了这里的大多数其他规则，所以您可能不需要这一条。我还是推荐。

这里还有另一个规则，强制使用 async/await 或 then()/catch()。这在项目开始时强制使用其中一个或另一个是很有用的。

明白了:[https://github.com/xjamundx/eslint-plugin-promise](https://github.com/xjamundx/eslint-plugin-promise)

# 额外收获:针对特定项目的有趣的 ESlint 插件

# eslint-plugin-lodash

如果您的项目中有 lodash，则使用 lodash 的规则。我最近很少使用 lodash，所以我不使用这个插件。如果我开始更频繁地使用 lodash，我肯定会再次使用这个插件。

明白了:[https://github.com/wix/eslint-plugin-lodash](https://github.com/wix/eslint-plugin-lodash)

# eslint 插件无秘密

这个插件检测看起来像是秘密的字符串。这是一个非常聪明的插件，但我发现它非常敏感，我不能正确配置它，所以我删除了它。不过，你可能会有更好的体验。

如果秘密永远不出现在你的应用程序中对你来说很重要，那就值得一试。

明白了:[https://github.com/nickdeis/eslint-plugin-no-secrets#readme](https://github.com/nickdeis/eslint-plugin-no-secrets#readme)

# eslint-插件-html

这个插件可以将 JavaScript 内嵌到你的 HTML 中。如果我有很多内联 JavaScript，我只会添加这个。这在现代 JavaScript 应用程序中不太可能。

明白了:[https://github.com/BenoitZugmeyer/eslint-plugin-html](https://github.com/BenoitZugmeyer/eslint-plugin-html)

# eslint-插件-降价

这个插件将解析你的减价文件中的代码。如果您正在创建技术文档或类似文档，这将非常有用。

我的博客上到处都是代码片段，但我仍然不再使用这个插件，因为 VSCode 现在在 markdown 中格式化我的代码。

明白了:[https://github.com/eslint/eslint-plugin-markdown](https://github.com/eslint/eslint-plugin-markdown)

# 要避免的 ESlint 插件

# eslint-插件-节点

我没有发现这些规则的巨大价值。

明白了:[https://github.com/mysticatea/eslint-plugin-node](https://github.com/mysticatea/eslint-plugin-node)

# eslint-plugin-json

我不使用这个插件，因为 VSCode 的 JSON 语言特性已经涵盖了大部分规则。我建议用你的 IDE 代替这个。

如果你的大多数开发人员将使用某种 IDE，你也许可以跳过这个插件。如果您的开发人员正在使用文本编辑器编写 JSON，那么将它添加到您的 CI 中。

明白了:[https://www.npmjs.com/package/eslint-plugin-json](https://www.npmjs.com/package/eslint-plugin-json)

如果你有任何问题，你可以在推特上联系我！

![](img/bd99d17ef43db1156313e9710f665317.png)

【https://www.darraghoriordan.com】最初发表于[](https://www.darraghoriordan.com/2021/06/23/best-eight-8-eslint-plugins-nestjs-node-application/)**。**

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*