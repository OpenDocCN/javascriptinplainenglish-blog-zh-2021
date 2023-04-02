# React 中样式化组件的 4 种不同方式

> 原文：<https://javascript.plainenglish.io/4-different-ways-to-style-components-in-react-9299d12ffae2?source=collection_archive---------15----------------------->

React 在你如何设计它方面是非常开放的。我将在 React 中找到我认为最流行的造型方法。

![](img/584518fb9e6bcf9f611a9445461eaf5e.png)

React 中有许多不同的样式，尽管它们都非常不同，但仍然非常相似。相似之处在于 CSS 是驱动它们的驱动力。如果你懂 CSS，你可以随心所欲地使用它。

# **1。普通 CSS**

这是一种屡试不爽的方法，似乎贯穿了互联网的整个生命。许多人认为你会立即抓住下面我将要谈到的解决方案之一，但事实并非总是如此。如果小心处理，常规 CSS 可能就是您需要的解决方案。

# 2.CSS 模块

类似于常规的旧 CSS，CSS 模块有相同的语法。区别在于它是如何实现的。CSS 模块本质上会生成一个将在 HTML 中使用的唯一的类名。CSS 模块试图解决的问题是组件中的命名冲突和作用域。

我的意思是。比如说，你有一个 CSS 文件(姑且称之为 **css-file-1.css** )，在这个文件里面，你有一个类名(姑且称之为 my-class)。这很好，除非我们再创建一个 CSS 文件，否则我们不会看到任何问题。让我们把这个文件叫做 **css-file-2.css** ，在这个文件里面，我们将创建一个同名的类。问题是在普通的 CSS 中，你不会得到想要的结果。由于 CSS 的全局性质，试图拥有相同名称的类是一个坏主意。然而，由于 CSS 模块的工作方式，即使 CSS 文件可能具有相同的类名，浏览器生成和使用的类名是完全不同的。

下面是一些解释如何在不同流行的 React 框架中使用 CSS 模块的链接。

[](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/) [## 添加 CSS 模块样式表|创建 React 应用程序

### 注意:此功能适用于[电子邮件保护]和更高版本。这个项目支持 CSS 模块以及常规…

创建-反应-应用程序.开发](https://create-react-app.dev/docs/adding-a-css-modules-stylesheet/) [](https://nextjs.org/docs/advanced-features/customizing-postcss-config#css-modules) [## 高级功能:自定义 PostCSS 配置| Next.js

### Next.js 使用 PostCSS 为其内置的 CSS 支持编译 CSS。开箱即用，无需配置，Next.js…

nextjs.org](https://nextjs.org/docs/advanced-features/customizing-postcss-config#css-modules) [](https://www.gatsbyjs.com/docs/recipes/styling-css#using-css-modules) [## 菜谱:使用 CSS 设置样式

### 有很多方法可以给你的网站添加风格；盖茨比几乎支持每一个可能的选择，通过官方…

www.gatsbyjs.com](https://www.gatsbyjs.com/docs/recipes/styling-css#using-css-modules) 

# 3.SCSS

SCSS 是众所周知的 CSS 预处理器，这意味着它将编译和构建 SCSS 文件，并在运行前将它们转换成 CSS 文件。这是 SCSS 最精彩的部分。如果你知道如何写 CSS，那么你就知道如何写 SCSS。SCSS 是 CSS 的超集，这意味着它有相同的语法，但有自己的附加语法。

以下是 SCSS 文档的链接。你会注意到，文档称之为 SASS，但不必担心，因为 SCSS 只是一个更新的，更容易接受的 CSS 语法。功能集保持不变。

 [## Sass 基础

### 在使用 Sass 之前，您需要在您的项目中设置它。如果你只是想在这里浏览，请继续，但我们…

sass-lang.com](https://sass-lang.com/guide) 

大多数 React 框架也使得使用 SCSS 非常容易。下面是一些解释如何在不同的流行 React 框架中实现它的链接。

[](https://create-react-app.dev/docs/adding-a-sass-stylesheet/) [## 添加 Sass 样式表|创建 React 应用程序

### 注意:此功能适用于[电子邮件保护]和更高版本。通常，我们建议您不要重复使用…

创建-反应-应用程序.开发](https://create-react-app.dev/docs/adding-a-sass-stylesheet/) [](https://nextjs.org/docs/basic-features/built-in-css-support#sass-support) [## 基本特性:内置 CSS 支持| Next.js

### js 支持包含 CSS 文件作为全局 CSS 或 CSS 模块，使用“styled-jsx”作为 CSS-in-JS，或任何其他…

nextjs.org](https://nextjs.org/docs/basic-features/built-in-css-support#sass-support) [](https://www.gatsbyjs.com/docs/recipes/styling-css/#using-sassscss) [## 菜谱:使用 CSS 设置样式

### 有很多方法可以给你的网站添加风格；盖茨比几乎支持每一个可能的选择，通过官方…

www.gatsbyjs.com](https://www.gatsbyjs.com/docs/recipes/styling-css/#using-sassscss) 

使用 SCSS 的另一个好处是它们也可以像 CSS 模块一样工作。这在上面的链接中有更详细的解释。

# 4.CSS-in-JS

Styled-Components 就是所谓的 CSS-In-JS 库。这听起来很可怕，但实际上这意味着你在用 JavaScript 迂回地编写你的风格。在设计 React 组件时，样式化组件是我的首选解决方案。在我看来，是两全其美。它利用 CSS 模块中存在的能力，并将其与类似 SCSS 的语法相结合。由于能够利用 JavaScript，您还获得了编写高度动态样式的额外好处(这可能是好事也可能是坏事，取决于如何处理)。

在不同的 React 框架中设置样式化组件的难度会有所不同，这取决于您使用的是哪一种框架。

当与 Create-React-App 或任何其他常规模块捆绑器一起使用时，它就像安装在您的项目中一样简单。

```
npm install styled-components
```

或者

```
yarn add styled-components
```

在 Gatsby 中，你可以参考他们文档中的这个链接来了解如何设置它。

[](https://www.gatsbyjs.com/docs/how-to/styling/styled-components/) [## 样式组件

### 在本指南中，您将学习如何使用 CSS-in-JS 库样式的组件建立一个站点。样式组件允许…

www.gatsbyjs.com](https://www.gatsbyjs.com/docs/how-to/styling/styled-components/) 

最后，在接下来，你可以参考这个链接，了解如何设置它。

[](https://styled-components.com/docs/advanced#nextjs) [## 样式组件:高级用法

### 主题化、引用、安全性、现有 CSS、标记模板文字、服务器端呈现和样式对象

styled-components.com](https://styled-components.com/docs/advanced#nextjs) 

# 结论

希望在阅读完这篇文章并看到一些不同的 React 组件样式后，这将为您的下一个项目提供思路。如果你认为我错过了什么或者想分享你在 React 中最喜欢的风格，我很乐意听听你的想法。

*更多内容看*[***plain English . io***](https://plainenglish.io/)