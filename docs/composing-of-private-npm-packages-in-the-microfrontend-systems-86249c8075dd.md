# 如何为微前端编写 NPM 包

> 原文：<https://javascript.plainenglish.io/composing-of-private-npm-packages-in-the-microfrontend-systems-86249c8075dd?source=collection_archive---------1----------------------->

在以前的文章中，我描述了如何以 [ts-modules](https://podumaihorosho.medium.com/npm-packages-in-ts-modules-format-7f64aa87591) 格式发布 NPM 包，并在整个系统中使用[统一国际化](https://podumaihorosho.medium.com/npm-i18n-internationalization-25da8201b3b8)。今天，我将分享关于哪些其他 NPM 包在微前端中有用以及如何管理它们的信息，以及在大型系统中开发私有 NPM 包的细微差别。

![](img/2d8349764166241b351c53a29327c9f4.png)

Photo by [Xavi Cabrera](https://unsplash.com/@xavi_cabrera?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## NPM 套餐的级别

在全球范围内，我根据抽象级别对 NPM 包进行分类。从最抽象、稳定的，到更多变的，越来越接近系统的业务领域。通常，三个级别就足够了:

1.  **具有基本定义的级别**。例如，DOM 的实用程序、一组 css 变量、Webpack/esLint 的配置以及整个系统的文档。这个级别的包尽可能的独立，通常根本不需要依赖。
2.  **常见业务实体级别**。例如，用于 GoogleAnalytics 的实用程序，一组用于 microfrontends 的常量，一些用于授权/文件/错误处理的业务实用程序。
3.  **成熟业务模块的级别**。例如，组件库、客户端授权模块或反馈模块。也就是说，这是一个特定的成品特性，可以完全集成到任何微前端中，但其本身不是微前端。

注意，**只允许从一般到特定**的导入，因此将遵守 **ADP** 原则。对了，我推荐在这里用[的建包原则来看](https://medium.com/@andrewMacmurray/package-principles-850d89da5e5b)。

## NPM 的责任范围-包

具体来说，我根据 **CRP** 和 **CCP** 原则来划分 NPM 包:我将业务所有权置于技术亲和力之上。比如 utilities:可以全部收藏在一个`utils`包里，也可以分成`utils-users`、`utils-documents`等。好处是，当`users`实用程序改变时，我们不会触及其余的实用程序——实用程序的发布周期将是独立的。

**有时**需要从最新版本的 NPM 软件包中导入一个更新的特性，但是当这个软件包发布时，不仅这个特性发生了变化，而且其他十个相邻的特性也发生了变化。11 个实体没有时间进行调整，因为只对业务计划进行了一次修订。发生这种情况的原因是，在设计 NPM 系统时，数据冗余的起始点确定不正确。

## NPM 包装的命名

包名中的第一件事是**作用域**。它通常相当于系统缩写。它需要支持节点的语义和对它们的调用(导入)。

不幸的是，NPM 在发布时只允许一层嵌套。也就是:`@scope-name/level1/package-name1`和`@scope-name/level1/package-name2`——是同一个名为`level1`的包。

为了实现语义分层，我使用了**烤肉串盒** : `@scope-name/1-docs`或`@scope-name/1-esLint`，或`@scope-name/2-utils-amount`。数字名称，可以根据您的判断更改为更有意义的名称。

例如，如果在第一层，有几个实用程序包，那么我们这样命名它们:`@scope-name/1-utils**-amount**`、`@scope-name/1-utils**-account**`、`@scope-name/1-utils**-user**`。从而在节点树(`node_modules`)中，它们彼此相邻。

![](img/c19f29006b4238be1ab49962ef9e1ff7.png)

Photo by [Steve Johnson](https://unsplash.com/@steve_j?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## NPM 包的依赖性

> 它禁止创建 NPM 包的循环依赖，如果你不能没有它们，那么最好复制部分功能。

我们上`peerDependencies`。但是首先，您需要从`dependencies`中移除所有相关的私有 NPM 包，然后在`devDependencies`和`peerDependencies`中复制它们。这是必要的，首先是为了 NPM 制度内部的一致性。其次，为了“减轻”最终的 js 文件，因为没有人希望在他们的包中存储同一个包的两个版本。

> 当然，您不应该盲目地从`dependencies`中删除所有依赖项。这个过程需要单独分析。但是现在，我先不说了。

我们通过一个固定的主要版本来描述我们的 NPM 软件包的所有版本，例如:`@scope-name/1-utils-dom: “2.x”`，因为我们不想遍历所有的 NPM 软件包并手动提升这些“无害的”版本。但是为了保持版本的一致性，我们必须使用 SEMVER。

> 在进行了数百次采访后，我注意到，只有少数人知道`dependencies`和`devDependencies`的区别。通常大家只记得语义成分。
> 
> **首先**，只有当涉及到将在 NPM 发布的 NPM 包时，这种差异才会显现出来。那些不使用他们自己的 NPM 包并将他们的`index.js`嵌入到 HTML 页面中的人，是的，可以将他们自己限制在这些指令的语义差异上。**其次**，如果发布的包有`dependencies`，那么在安装父包时，来自该指令的依赖项也会被安装，这将导致包重复和数据不一致。
> 
> 因此，我们将依赖项转移到`peerDependencies`，以便从外部系统中提取它们。

## 语义版本控制

考虑`@scope-name/1-utils: “A.B.C”`模块，其中:

**C** —是“幕后”的补丁或修订版，不影响功能，也不需要在“母”系统中进行调整。

**B** —是次要版本，仅意味着添加新功能，或者，例如，扩展当前常量或接口。与补丁一样，它不会影响外部系统，也不需要对自身进行调整。

**A** —是一个主要版本，它对外部系统进行了**突破性的改变**，并要求其适应新版本。

之前我说过我们只冻结主版本，这意味着`npm i`会把这些包更新到最新的次版本。通常，主要版本是在整个系统中集中提出的(由大多数团队提出，而不是单独提出)，例如，当系统被重新设计时。

## 微前端 NPM 封装的组成

在上一篇文章中，我谈到了使用私有 NPM 包的想法，就像云中的常规目录一样。现在这个想法将特别具有启发性，因为我们将不得不公布诸如:`.less`、`.svg`、`.ts/x`、`.png`、`.json`、`.md`等来源。

![](img/6574260b9492fc3f986a161d32fb7a39.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 第一级:

1.  对于系统文件- `@scope-name/1-docs`。好的做法是在项目本身中记录项目，而不是在维基中的某个地方。你也应该把 **style-guid** 放到这个包里。
2.  用于开发工具- `@scope-name/1-tools`。这里是配置文件`.tsconfig`、`.npmrc`、`.browserslist`、esLint 规则、用于测试的酶设置，也可能是 Webpack 配置的一部分。
3.  对于音译和普通文本- `@scope-name/1-translations`。所有通用的国际化系统都以 **ts-constants** 的形式出现。[我的上一篇文章](https://podumaihorosho.medium.com/npm-i18n-internationalization-25da8201b3b8)就是专门写这个包的。
4.  对于全局样式- `@scope-name/1-styles`。这个包包含了所有的全局变量(颜色，大小，缩进)和通用的系统样式。该包被发布为`.less`文件。
5.  对于图标和图像- `@scope-name/1-graphics`。这里收集了系统的所有通用图形:`.svg`、`.png`等。顺便说一下，通过类比，您可以通过为字体创建一个单独的包来处理字体。
6.  常用工具- `@scope-name/1-utils`
7.  DOM 树实用程序- `@scope-name/1-utils-dom`
8.  base64 转换实用程序- `@scope-name/1-utils-base64`
9.  文件实用程序- `@scope-nam/1-utils-files`
10.  等等…

## 第二级:

1.  分析功能- `@scope-name/2-analytics`。这包含了谷歌分析的所有助手功能
2.  【产品】常量- `@scope-name/2-consts-products`
3.  【单据】常量- `@scope-name/2-consts-documents`
4.  运行时错误处理实用程序- `@scope-name/2-logger`
5.  商业公用事业- `@scope-name/2-utils`
6.  等等…

## 第三级:

1.  组件库- `@scope-name/3-components`
2.  用户授权模块- `@scope-name/3-authorise`
3.  评级模块- `@scope-name/3-rating`
4.  等等…

## NPM 的基础设施设置-包

我将只讨论设置和 devops 的一些方面:

*   所有私有的 NPM 包必须在 Bitbucket (或其他地方)合并成一个单独的项目，这样开发者就可以看到整个画面。
*   主应用程序和每个微前端也应该在自己的项目中。因为通常每个这样的项目都有后台存储库和基础设施。记住 NPM 包的划分，根据它们的责任区域，有存储库——同样的方式。
*   对于每个 NPM 包，你需要通过 **Jenkins** (或类似的)创建一个组装和发布的作业，或者最好在`master`分支挂一个合并 PR 的钩子，这样作业就可以自己开始了。
*   对于 NPM 封装，大多数情况下一个`master`分支就足够了。但是有些情况下，开发者想要“非法地”改变一个已经发布的版本，而不影响当前的版本。为此，您可以使用**版本键** : `@scope-name/1-utils: “3.4.0**-release-2021–03–29**”`，而当前版本为`“4.0.0”`。这种情况下，除了`master`分支，还会有`release-2021–03–29`。
*   每个包的发布脚本必须从构建/类型检查开始，并运行 linters 和测试。
*   发布的凭证必须存储在 **Jenkins** 基础设施的上下文中，例如，该基础设施在自己的作业中修改项目根目录中的`.npmrc`文件，在那里添加具有正确值的`_auth`指令。这个参数的值通常是这样的:`base64 ([login]: [pass])`。
*   带有 NPM 包的存储库中的所有提交应该看起来像这样:`@scope-name/package-name@4.1.0 — a brief description of the update`，维护这样一个存储库的实践表明，这是很方便的。

## NPM 系统的社会组成部分

![](img/8832e6cecd0871f900b271cf074f64ca.png)

Photo by [Vlad Hilitanu](https://unsplash.com/@vladhilitanu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在这篇文章中，我们看了很多微前端中 NPM 包形成和支持的原则和规则，但是我们没有触及最重要的因素，是的，**人的因素**。

对大型 NPM 系统的支持很大一部分用于社会部分。我将试着告诉你主要的方面:

## 专业知识和责任

理想情况下，创建一个**核心团队**，全职处理 NPM 软件包，并在顶层负责系统中的所有软件包。分配本地职责也是一个好的实践，例如，专门为系统组件库创建一个团队。

当遵循这些指令时， **devops** 在 **Bitbucket** 中实现了一个插件，该插件自动将标签放入 pull 请求中，该请求只有在标签组的成员批准后才能显示为绿色。

因此，如果一个新的开发人员进入项目并输入 PR，例如，`@scope-name/2-consts-documents`，他将看到对于合并，他需要来自以下组的批准:`core_team`、`bussiness_expert_team`、`expert_team`。也就是说，首先，他将收到团队中一位专家的批准，然后是一位业务级专家的批准(第二位，我们在本文开始时谈到过)，最后是 NPM 系统主要专家的最终批准。

因此，代码库仍然受到可靠的保护，审查将由负责可修改模块的人员进行。在实践中，我发现如果一个专家同时审查几个他不熟悉的不同上下文的项目，他就变成了一个“聪明的过客”,这并不能提高拉请求的效率。

## 通知和维护发布

当提交对 NPM 包的变更时，开发者必须创建一个描述当前变更的`.md`文件。要让它出现在公版里，像 as: `@scope-name/2-consts-documents/docs/release-notes/4.x.x/4.4.5.md`。和这个操作必须重复在每一个 NPM 包与每一个变化。

在一个 NPM 软件包的主要发布之前，负责这个变更的团队必须提前通知公司的所有员工(软件开发部门)他们的意图。通过公司电子邮件或在一些普通的聊天中群发邮件效果很好。

此外，在主要版本发布后，该团队应该向每个人发送一份摘要发布说明，甚至可以是演示文稿，最重要的是，从以前的版本到新版本的预定逐步过渡。如果他们也在故事点中提供自己的评估，那就更好了。毕竟，系统中有很多微前端，每个微前端的产品负责人在阅读邮件列表时，应该了解即将到来的过渡的劳动力成本。

但例如，对于次要版本和补丁，一个开发人员可能不会引起这样的公众注意，而只是通知其他开发人员(不是所有员工)他们的更改。正规的一般开发者聊天就很好的做了这个工作。

> 当一个新的开发人员入职时，他只需要去`@scope-name/1-docs`库为他学习一个新系统的所有规则、原则和基础。

## 来自作者

这篇文章对我来说非常重要，因为它组织了多年来收集的大量经验。我想触及所有的话题，同时不去探究次要的细节。感谢您花时间和精力阅读它。

**附言**在下一篇文章中，我将告诉你如何使用 **System.js** 创建一个微前端，最重要的是，我将告诉你如何逐步实现一个微前端，拥有一个大型遗留单项目。

我经常在文章中提到“大型项目/系统”这个词。在这里，我指的是 200-300 万个文件+80-150 个团队的代码库。

不要从字面上理解收到的信息，试着理解主要的思想/情感，并根据你的要求进行调整。就我个人而言，我总是试图首先在情感层面上感受信息，然后才将其转化为有形的世界，所以我怀疑，我呈现的信息也是如此。