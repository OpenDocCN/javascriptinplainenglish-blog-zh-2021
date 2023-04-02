# 为什么我的 React 代码看起来不专业？

> 原文：<https://javascript.plainenglish.io/why-doesnt-my-react-code-look-professional-4caefdeabc0c?source=collection_archive---------3----------------------->

## 适合工作的工具——JavaScript 版本

![](img/fb6dcd7f4be093b6d63118e18a95ab46.png)

Photo by [Karim MANJRA](https://unsplash.com/@karim_manjra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

除了多年的实践，阅读[干净的代码](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)，然后阅读[干净的 Javascript 代码](https://github.com/ryanmcdermott/clean-code-javascript)，你可以*自动化*你的许多“麻烦”,至少关于你代码的整体“干净”。

如何编写看起来干净的代码是你最终会学到的东西，它是经验和知识的结合，可能不适合写在一篇简短的文章中。但是你可以直接做的是，结合使用 [ESLint](https://eslint.org/) 和[appellister](https://prettier.io/)这样的工具，采用规则、标准和最佳实践，这将迫使你写出更好、看起来更整洁的代码。

# 为什么我们需要 linters 和代码格式化程序？

我在这里假设，像我们大多数人一样，您已经使用了`create-react-app`来快速入门。接下来你要做的是开始实现一个 linter (ESLint 是目前最流行的选择)和一个 code formatter(这里更漂亮的是我们的选择)。linter 和代码格式化程序对你帮助最大的是与团队成员合作。一个被每个人的个人风格污染的代码库将很难维护——这就是为什么我们使用 linters 来消除潜在的有问题的实践，并使用 formatters 来保持风格的一致性。设置了一个通用标准，配置保存在项目的根中，以便每个克隆项目的人都可以使用，并且通常情况下，CI/CD 管道会在将代码合并到分支并触发构建之前检查这些标准是否得到遵守。

# ESLint & Airbnb

linter 可以以多种方式配置，它通常会有“标志”作为规则集，我们可以在其中指定我们想要遵守的规则——目前，ESLint 有许多规则可用，很难决定要遵守哪些规则，尤其是在您刚开始使用的时候。这就是为什么 Airbnb(是的，就是 Airbnb[的好伙伴们](https://www.airbnb.com/))已经推出了他们自己的[套基本规则](https://github.com/airbnb/javascript)，你可以利用这些规则进行开发——目前，大约有 670，000+的下载量，我想，至少有两倍的开发人员在遵循他们的风格指南。较新的 ESLint 版本允许你直接使用流行的风格指南。一旦你确定`eslint -v`带回了一个版本号，我们就确定 ESLint 工具是“全球”安装的，可以像任何其他常用工具(npm、npx、yarn 等)一样使用。

在项目的根目录下，运行`eslint --init`在控制台中启动一个初始化向导，选择适合你的选项。你将能够指定你的应用在浏览器中运行(与节点环境相比)，你正在使用 React，你想要遵循一个流行的风格指南，即 Airbnb(以及其他东西)。系统还会提示您安装对等依赖项——在早期版本的 ESLint 中，您必须手动安装，但现在只需选择“是”即可。

![](img/29e1c3370de79de6865ad4641d8933e1.png)

[https://prettier.io/](https://prettier.io/)

# 漂亮&埃斯林

安装更漂亮是非常简单的。按照本指南[和几个命令](https://prettier.io/docs/en/install.html)，你应该准备好了。

`yarn add --dev --exact prettier`

创建一个空的`.prettierrc.json`文件，只是为了让其他工具知道 Prettier 在这里(您可以稍后编辑这个文件来引入您想要的规则)。此外，添加`.prettierignore`，它的作用与`.gitignore`完全一样，并概述了该工具应该忽略哪些文件和文件夹。

现在，linters 和代码格式化程序的共同点是它们处理代码的风格。由 linter 执行的一些规则可能[与](https://prettier.io/docs/en/comparison.html)重叠，甚至与由一个简单的代码格式化程序执行的规则冲突，看两者如何能够成为独立的工具(考虑到不同的目标)。为了解决这个问题，您可以从安装以下 dev 依赖项开始:

`yarn add --dev eslint-config-prettier`

编辑您的`.eslintrc.json`文件以使用这个配置:

```
{
  "extends": [
    "some-other-config-you-use",
    "prettier"
  ]
}
```

这将确保任何与更漂亮的规则冲突的 ESLint 规则被关闭。这些重叠都与风格有关，因此在等式的一边关闭它们不会对最终产品质量产生任何有意义的影响。

**注意** : *你可能选择了其他格式来存储你的 ESLint 配置，上面的例子处理的是 JSON 格式。*

# 结论

现在你知道了。您现在可以使用类似于`npx ESLint yourfile.js`的东西来 lint 您的代码，并且您可以使用`npx prettier --write`来格式化您的代码。不过，我要指出的是，**一个更好的选择**是通过许多官方插件之一将这些工具集成到您的 IDE 中，并在保存时自动运行这些命令。随着时间的推移，你甚至不会注意到这种情况的发生，你将能够编码得更快(更好)。

这些工具执行的许多样式和代码质量规则将使您的代码看起来更好，并避免常见的(可能的)陷阱。这些规则通常是由意见和经验形成的，因此，虽然您的代码可能在不遵守这些规则的情况下完美地工作，但是您正在避免一个“站在巨人的肩膀上”的好机会。开发社区是一个巨大的知识来源，世界各地的开发人员分享他们的经验(和观点),他们相信这将使您的代码更容易阅读、维护和扩展。今天就开始使用 linter，仔细阅读这些规则，了解它们存在的原因，避免忽略它们(*你可以在代码中加入特殊的注释，偶尔绕过林挺规则*，让你的代码库立刻变得更好。

*此外，如果你认为你有一些我可能遗漏或误解的见解，请在评论中自由讨论——这个主题很广泛，可以用无数种方式来处理。如果你想拓展人脉或者只是扩大人脉——你可以在*[*Twitter*](https://twitter.com/SNimcevic)*和*[*LinkedIn*](https://www.linkedin.com/in/sini%C5%A1a-nim%C4%8Devi%C4%87-5b438996/)*上找到我。*

# 资源

*   [https://www . Amazon . com/Clean-Code-Handbook-Software-craftness/DP/0132350882](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)
*   [https://github.com/ryanmcdermott/clean-code-javascript](https://github.com/ryanmcdermott/clean-code-javascript)
*   [https://ESLint.org/](https://eslint.org/)
*   [https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)
*   [https://prettier.io/docs/en/comparison.html](https://prettier.io/docs/en/comparison.html)

*More content at* [***plainenglish.io***](http://plainenglish.io/)