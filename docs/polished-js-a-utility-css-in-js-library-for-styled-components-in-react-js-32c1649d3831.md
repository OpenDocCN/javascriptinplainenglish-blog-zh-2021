# polished . JS:react . JS 中样式化组件的实用 CSS-in-JS 库

> 原文：<https://javascript.plainenglish.io/polished-js-a-utility-css-in-js-library-for-styled-components-in-react-js-32c1649d3831?source=collection_archive---------8----------------------->

## 受 CSS-inJS 的 Sass 启发的样式实用程序

![](img/8a49ccd0f9064e6ea0559622abffa106.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

像`lighten()`、`darken()`、`complement()`、`invert()`这样的 Sass 函数相当有用。我想知道是否有适合样式组件的东西。嗯，我发现了很棒的库 [Polished.js](https://polished.js.org/) 。

这个库的好处在于，不管你是使用[样式化组件](https://styled-components.com/)、[情感](https://emotion.sh/)、 [jss](https://cssinjs.org/?v=v10.6.0) 、[阿芙罗狄蒂](https://github.com/Khan/aphrodite)、[镭](https://formidable.com/open-source/radium/)，还是只是 JavaScript 中的内联样式。它适用于所有人！

它是一个实用程序库，所以你只需要导入你需要的东西来为用户节省一些字节。打字稿需要打字吗？他们掩护你！

所以让我们深入了解一下如何使用 Polished.js。

# 装置

对于安装来说，运行熟悉的命令就足够了。

```
npm install --save polished
# or if you're using yarn
yarn add polished
```

# 进口

在 JavaScript、TypeScript 或 React 组件文件中导入您需要的实用函数。

```
import { cssVar, darken } from 'polished'
```

我最喜欢的函数是`lighten()`、`darken()`、`complement()`和`linearGradient()`，但是它们的文档中有更多的[函数](https://polished.js.org/docs/)。

# 使用

为了演示如何将 Polished.js 用于样式化组件，我们将为一个`<input>`字段创建一个组件。我将使用 CSS 变量使我的`<input>`字段的背景变得更暗。

我的 CSS 变量是在 public 文件夹的`global.css`文件中定义的。我目前正在 Next.js 项目中使用它。

`cssVar()`函数可以从根中提取变量，并将它们变成更深的颜色。

输出颜色变为`#eee`。所以我不用自己决定。

# 更好的用法

但是我认为在我的 React/Next 应用程序的根组件中将它定义为自己的颜色会更好。我有一个`<Layout>`组件作为我的根组件，所以最好在那里定义那些 CSS 变量。

因为我希望我的颜色在我的 JavaScript 中可用，所以我创建了一个包含所有颜色的函数。我已经将它添加到一个单独的文件中，以便将来重用。现在我可以将它赋给一个常量变量`root`，使它在组件中可用。

现在我们可以在`<Layout />`组件中使用`<GlobalStyle />`组件。现在所有的 CSS 变量在应用程序中都是可用的。

所以在我的`<Input />`组件中，我可以像其他组件一样使用 CSS 变量。

# 结论

我希望你从这篇文章中学到了一些新的东西。如果你为你的 CSS-in-JS 使用其他工具，请分享它们。我喜欢听他们说话！

*快乐编码*🚀

**延伸阅读**

[](https://betterprogramming.pub/how-to-build-and-deploy-a-jamstack-website-fast-with-next-js-a61df3c822f) [## 如何使用 Next.js 快速构建和部署 Jamstack 网站

### 为什么 Next.js 是明智的选择

better 编程. pub](https://betterprogramming.pub/how-to-build-and-deploy-a-jamstack-website-fast-with-next-js-a61df3c822f) [](https://betterprogramming.pub/how-promises-actually-work-in-javascript-1c80b1af7193) [## JavaScript 中承诺的实际工作方式

### 了解何时以及如何使用它们

better 编程. pub](https://betterprogramming.pub/how-promises-actually-work-in-javascript-1c80b1af7193) [](https://devbyrayray.medium.com/how-to-add-props-to-styled-components-in-react-js-with-typescript-1df49ef951bf) [## 如何用 TypeScript 在 React.js 中给样式化组件添加道具

### 在 React.js 中使用样式化组件编写可预测的代码

devbyrayray.medium.com](https://devbyrayray.medium.com/how-to-add-props-to-styled-components-in-react-js-with-typescript-1df49ef951bf) [](https://devbyrayray.medium.com/how-to-use-css-media-queries-with-styled-components-in-react-js-f5db5ffcc5f0) [## 如何在 React.js 中对样式化组件使用 CSS 媒体查询

### 在样式化组件中更智能地使用媒体查询

devbyrayray.medium.com](https://devbyrayray.medium.com/how-to-use-css-media-queries-with-styled-components-in-react-js-f5db5ffcc5f0) [](https://devbyrayray.medium.com/css-variable-with-styled-components-7e91d89f13f3) [## 带有样式化组件的 CSS 变量

### 在 Next.js/React.js 轻松使用它们

devbyrayray.medium.com](https://devbyrayray.medium.com/css-variable-with-styled-components-7e91d89f13f3)