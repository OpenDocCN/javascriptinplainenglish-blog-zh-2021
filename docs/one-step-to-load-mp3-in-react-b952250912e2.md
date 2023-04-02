# 将 MP3 加载到 React 应用程序的一个步骤

> 原文：<https://javascript.plainenglish.io/one-step-to-load-mp3-in-react-b952250912e2?source=collection_archive---------2----------------------->

是的，你只需要执行这一步就可以在 React 应用程序中加载 MP3。

![](img/ca80d939cca203cf2b55d243a834a4cb.png)

Photo by [NeONBRAND](https://unsplash.com/@neonbrand?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 在后台

我正在开发一个帮助编辑音频文件的应用程序。我需要在我的 React 应用程序中加载音频文件。我谷歌了一下，得到了一堆加载 MP3 的包。尽管如此，我在静态文件夹中的 mp3 文件还没有导出或准备好使用。

# 概观

在谷歌搜索了将近一个小时后，我找到了答案。您只需要执行一个步骤就可以将 MP3 加载到 React 应用程序中。

让我们直接跳到例子。假设我们的 React 应用程序中有音频文件，我们需要加载所有的音频文件控件，比如播放按钮、暂停按钮、扬声器音量范围按钮等等。

React 应用程序的问题是，特别是当您使用 Next.js 时，它们在一个目录中提供静态文件(对于 Next.js 是公共的)，并且在服务器端从单个目录加载这些静态文件是困难的。

如果您不熟悉服务器端，那么服务器端渲染基本上是在服务器上运行应用程序，而不是在本地运行。

所以加载图像是非常容易的，并且在服务器端由 Next.js 轻松处理。

Next.js 只是在服务器上加载这些静态图像，在构建应用程序之后，这些图像是从 Next.js 自己创建的 Express 服务器上加载的。我们从来不把应用程序和图片捆绑在一起，只是为了一个性能上的原因。

# 问题

mp3 文件的主要问题是它们在服务器端不能被识别。音频支持是浏览器的功能，而不是服务器的功能。所以我们将面临在服务器端运行 MP3 的问题。

我们需要一个名为 url-loader 的 npm 包，它可以简单地处理 HTML 文件，并将它们转换成数据 URL base 64 编码字符串。就像你在浏览器上传一个 PDF 或者图片，把它们转换成 base 64 发送给服务器一样。

将 HTML 文件转换成数据 URL 是很重要的，因为数据 URL 很容易被服务器识别和理解。我们不需要在服务器上实时转换；相反，我们可以使用 webpack 来为我们做这件事。

# 解决办法

您只需遵循一个步骤来配置 webpack 并使用 npm 包来提供 mp3 文件。

一旦我们用 url 加载器包配置了 webpack，我们只需告诉 webpack 将 mp3 文件作为整个应用程序包中的数据 URL。Webpack 将简单地把我们的脚本和 mp3 文件捆绑到一个数据 URL 中，以便在浏览器中理解和加载。

我们使用的 npm 包是 url-loader。

```
[https://www.npmjs.com/package/url-loader](https://www.npmjs.com/package/url-loader)
```

# 编写代码

我将把所有基本的必要过程留给您，比如创建 Next.js 存储库和添加一些示例 mp3 文件的过程。

相反，我用的是现成的 [**例子**](https://github.com/shreyvijayvargiya/iHateReadingLogs/tree/main/TechLogs/NextJSArchitecture) **。**一旦克隆了存储库，使用 yarn 或 npm 安装 url-loader 包。

```
yarn add url-loader
```

现在加载 mp3 的唯一也是最重要的步骤是配置 webpack。在根目录中创建`**next.config.js**`文件，并添加以下几行。

next.config.js

添加到`**next.config.js**`文件后，我们就可以从公共文件夹导入 mp3 文件并使用它们了。

如果您查看我们提到的代码，比如 test，这是我们将使用的文件格式或文件扩展名。

# 结论

我们简单地使用 webpack 和外部加载器来捆绑和使用我们的 mp3 文件。我们可以为 webpack 配置提供更多的加载器来捆绑想要的文件，例如 SVG、js 或 png 或 handlebars 等等。我们甚至可以将 webpack 用于 Node.js 中的服务器应用程序。

请继续关注，我将在另一篇文章中完整介绍一个 webpack。

```
Until, next time. Have a good day, People.
```

[](https://medium.com/nerd-for-tech/flatlist-is-still-underrated-796130a8b8f2) [## Flatlist 仍然被低估了

### 也许你使用 Flatlist 的方式是错误的，这里有一些提示和技巧

medium.com](https://medium.com/nerd-for-tech/flatlist-is-still-underrated-796130a8b8f2) [](https://medium.com/nerd-for-tech/top-5-ui-libraries-for-react-native-2ce8a973bb1c) [## React Native 的前 5 个用户界面库

### 列出了前 5 个 React 原生 UI 库

medium.com](https://medium.com/nerd-for-tech/top-5-ui-libraries-for-react-native-2ce8a973bb1c) [](https://medium.com/nerd-for-tech/perfect-styling-library-for-react-native-9de410d9d5eb) [## React Native 的完美样式库

### 使用 React Native 处理顺风 CSS

medium.com](https://medium.com/nerd-for-tech/perfect-styling-library-for-react-native-9de410d9d5eb) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)