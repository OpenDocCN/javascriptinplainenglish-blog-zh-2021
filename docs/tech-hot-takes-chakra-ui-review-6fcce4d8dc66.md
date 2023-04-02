# 技术热点:查克拉用户界面审查

> 原文：<https://javascript.plainenglish.io/tech-hot-takes-chakra-ui-review-6fcce4d8dc66?source=collection_archive---------7----------------------->

## 一个简单、快速、完整的用户界面库

![](img/ab734e6b9ba1300a3ae565827ec2fe84.png)

# 什么是查克拉 UI？

> “Chakra UI 是一个简单、模块化和可访问的组件库，为您提供构建 React 应用程序所需的构建块。”
> 
> — [查克拉 UI](https://chakra-ui.com/)

通俗地说，Chakra UI 就是为 React 打造的一体化 UI 库。它允许开发人员快速构建生产就绪的 React 应用程序，同时保持其可访问性、主题化和可组合性。该库受到了[主题 UI](https://theme-ui.com/) 的极大启发，并遵循了[系统 UI 规范](https://system-ui.com/theme)。此外，向所有的动漫迷大喊——查克拉用户界面实际上是以受欢迎的动漫火影忍者命名的😆。

![](img/19dd18b8b60b5cdebe93a2d439933e96.png)

Founder Segun Adebayo’s Twitter post about the origin of the library name

# 特征

Chakra UI 提供了大量的特性，使库可定制、可扩展且易于访问。以下是一些让我印象深刻的例子:

## 主题

光明和黑暗的主题最近获得了很多流行的牵引力，它并没有被忽视。Chakra UI 有一个默认主题[由一个现代调色板组成，每种颜色有 9 种不同的变体。作为一个在前端创意和选择的悖论中挣扎的人，它为我节省了几个小时寻找应用程序颜色主题的灵感。对于那些对自己的 UI 品味有信心的人来说，这个库允许你完全定制多个版本的主题。您可以使用](https://chakra-ui.com/docs/theming/theme)[提供的挂钩](https://chakra-ui.com/docs/features/color-mode#usecolormode)切换到任何设定的主题。这个功能使得主题更新像黄油一样流畅(这里有 BTS 军队吗？).

*热提示:*[*Themera*](https://themera.vercel.app/)*是一个为 Chakra UI 生成可导出颜色预设的伟大工具。*

## 风格道具

Props 是 React 中传递或冒泡函数或值的主要方式。查克拉 UI 组件能够传递[风格道具](https://chakra-ui.com/docs/features/style-props)给他们，作为创建风格组件的一种速记。此外，Chakra UI 确保缩写属性名，这样它们就不会使你的代码混乱。但是——他们也为喜欢更明确的开发人员保留了更详细的选项。这个特性与 VSCode IntelliSense 配合得非常好，这反过来大大加快了我的开发速度。

对于最初迁移到 Chakra UI 的开发人员来说，使用纯 CSS 的`[sx](https://chakra-ui.com/docs/features/the-sx-prop)` [prop](https://chakra-ui.com/docs/features/the-sx-prop) 可能更容易。`sx`和`__css`属性通常适用于响应样式，但是样式属性也可以接受不同样式断点的一组值。

*热门提示:道具优先级是* `*sx*` *>风格道具>* `*__css*`

## CSS 变量

CSS 变量可能感觉像是现代 UI 库中的必备组件。然而，我仍然想给予他们应有的信任。开发人员可以在 style props 中直接使用 CSS 变量，并在任何其他样式输入中使用语法`var(--chakra-path-name)`，以轻松访问存储的样式。

## RTL 支持

由于 Chakra UI 是基于[情感](https://emotion.sh/docs/introduction)的，你可以使用类似的机制来设置 [RTL(从右到左)支持](https://chakra-ui.com/docs/features/rtl-support)。这有助于全球化您的应用程序，并提供视觉上更合适的体验。

## 成分

这是迄今为止我最喜欢的关于 Chakra UI 的部分。该库提供了无数的组件，从布局组件(例如，容器、Flex、框等)到覆盖组件(例如，菜单、模态、工具提示等)。我还没有设计任何按钮或文本块的用例。每个组件都有自己的风格道具，并且可以根据你的需要用`sx`道具完全定制。这些组件还与脉轮主题以及内置的可访问性支持很好地集成在一起。我已经探索了许多组件库，如材料 UI 和主题 UI，我还没有找到一个像 Chakra UI 组件那样完整和对开发人员友好的。

## 查克拉工厂

与使用其他 UI 库类似，开发人员最终会适应并熟练使用 Chakra UI 风格的道具。在极少数情况下，Chakra UI 不包括供您使用的组件模板，或者如果您喜欢在代码中使用现有的 React 组件，那么使用不同的样式语法会很不方便。Chakra UI 思考并创建了这个名为 [Chakra Factory](https://chakra-ui.com/docs/features/chakra-factory) 的包装器。这允许开发人员将 Chakra UI 风格的道具转发到工厂内包装的任何组件中。这将可定制性提升到了一个全新的层次。

## 钩住

Chakra UI 不仅在 UI 相关的特性上表现出色，而且它还提供了许多钩子来完善浏览器交互。我最喜欢的是 [useClipboard](https://chakra-ui.com/docs/hooks/use-clipboard) ，这是一个定制的钩子，用于将内容复制到剪贴板。这是文档站点中的必备组件，也是任何现代站点的重要补充。

# 我的热门话题

我不是那种通常对 CSS 赞不绝口的人，事实上，如果可能的话，我会避免使用它。然而，Chakra UI 使得前端开发变得更加令人愉快，因为它使令人头痛的、乏味的样式部分变得可以理解和有效。另外，这个社区也很有趣，很有帮助！他们甚至有自己的[不和谐服务器](https://discord.com/invite/chakra-ui)，用户在那里积极地互相帮助，并自豪地展示和分享他们的工作。到目前为止，我还没有遇到任何使用 Chakra UI 的问题，它让我看到了一个网站在正确执行时是多么简单和令人满意。

**功能:10/10🚀文件:2010 年 9 月🔥
开发者体验:9/10👨🏻‍💻
社区:8/10🕺🏻**

*更多内容请看*[*plain English . io*](http://plainenglish.io/)